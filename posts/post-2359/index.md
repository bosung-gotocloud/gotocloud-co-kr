---
title: "Azure Ubuntu 22.04 virtual machine kernel update"
date: 2024-10-19T14:44:35+09:00
source: https://gotocloud.co.kr/?p=2359
categories: []
tags: []
---

When registering a Ubuntu-based virtual machine on the Azure Marketplace, there are times when the process cannot proceed further due to an email indicating an issue with the operating system’s security verification.

Even after using the Ubuntu image provided by Azure to install the necessary software and then publishing the image, warnings occur because the previously registered image had no security issues at the time of registration. However, if a new OS image is registered without applying security patches that occurred after the registration, it will not pass the security verification.

Even if you perform apt update or apt upgrade on the OS image, if the patch is still not applied, you need to update the kernel. To update the kernel of an Azure Ubuntu virtual machine, follow these steps in the terminal after running the Ubuntu 22.04 virtual machine:

- update and upgrade packages

```
$ sudo apt update 
$ sudo apt upgrade
```

- Install the kernel with the security patch applied. You can find the kernel version according to the patch number included in the Marketplace inspection. For example, the patch for USN-7076-1 can be found at https://ubuntu.com/security/notices/USN-7076-1. Use the following command to install the kernel. Here, we are installing version 5.15.0-1072-azure as an example

```
$ sudo apt install linux-{image,headers}-5.15.0-1072-azure
```

- Check kernels installed

```
$ sudo awk -F"--class" '/menuentry/ && /with Linux/ {print $1}' /boot/grub/grub.cfg | awk '{print i++ " : " $5,$6,$7,$8}' | sed -e "s/'/ /g"
0 : 6.5.0-1025-azure
1 : 6.5.0-1025-azure (recovery mode) 
2 : 5.15.0-1072-azure
3 : 5.15.0-1072-azure (recovery mode) 
4 : 5.15.0-1066-azure
5 : 5.15.0-1066-azure (recovery mode)
```

- Change the grub configuration to boot using the new kernel

```
$ sudo sed -i 's/GRUB_DEFAULT=.*/GRUB_DEFAULT=saved/g' /etc/default/grub 
$ grub-set-default "Advanced options for Ubuntu>Ubuntu, with Linux 5.15.0-1072-azure"
```

- Check the grub update and reboot

```
$ sudo grub-editenv list
saved_entry=Advanced options for Ubuntu>Ubuntu, with Linux 5.15.0-1072-azure 
$ sudo update-grub 
$ sudo reboot
```

- After reboot, check the new kernel is applied

```
$ sudo uname -r 
5.15.0-1072-azure
```
