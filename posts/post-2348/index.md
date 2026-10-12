---
title: "Install Ubuntu linux on Windows using WSL"
date: 2024-05-23T11:15:25+09:00
source: https://gotocloud.co.kr/?p=2348
categories: []
tags: []
---

## WSL(Windows Subsystem for Linux)

When you want to run Linux-specific programs or develop in a Linux environment, there are times when you need Linux hardware. However, if you only have a computer with Windows installed, in the past, you would have to install Linux through #Dual booting or even set up a dedicated Linux machine. To avoid this hassle and use Linux on Windows, Microsoft provides WSL (What is Windows Subsystem for Linux | Microsoft Learn).

This article summarizes how to install Ubuntu Linux using #WSL and configure a basic WSL distribution that can be used for various purposes.

## Install Ubuntu 22.04 base image

In Windows, you run the command prompt and check if there are any WSL distributions installed with the command wsl –list. If there are no previously installed WSL distributions, a message will be displayed indicating that nothing is installed.

C:\Users\gotocloud>wsl --list
Linux용 Windows 하위 시스템에는 설치된 배포판이 없습니다.

'wsl.exe --list --online'을 사용하여 사용 가능한 배포판을 나열하고
'wsl.exe --install <Distro>'를 사용하여 설치하세요.

배포판은 Microsoft Store
(https://aka.ms/wslstore)를 방문하여 설치할 수도 있습니다.
Error code: Wsl/WSL_E_DEFAULT_DISTRO_NOT_FOUND

You can check the available Linux distributions for installation with the command wsl –list –online.

C:\Users\gotocloud>wsl --list --online
다음은 설치할 수 있는 유효한 배포판 목록입니다.
'wsl.exe --install <Distro>'를 사용하여 설치합니다.

NAME FRIENDLY NAME
Ubuntu Ubuntu
Debian Debian GNU/Linux
kali-linux Kali Linux Rolling
Ubuntu-18.04 Ubuntu 18.04 LTS
Ubuntu-20.04 Ubuntu 20.04 LTS
Ubuntu-22.04 Ubuntu 22.04 LTS
Ubuntu-24.04 Ubuntu 24.04 LTS
OracleLinux_7_9 Oracle Linux 7.9
OracleLinux_8_7 Oracle Linux 8.7
OracleLinux_9_1 Oracle Linux 9.1
openSUSE-Leap-15.5 openSUSE Leap 15.5
SUSE-Linux-Enterprise-Server-15-SP4 SUSE Linux Enterprise Server 15 SP4
SUSE-Linux-Enterprise-15-SP5 SUSE Linux Enterprise 15 SP5
openSUSE-Tumbleweed openSUSE Tumbleweed

Begin by installing and starting Ubuntu 22.04. During the installation, set up the default user account and password. In this article, the default user account is set to ‘gotocloud’. Enter the desired username.

C:\Users\gotocloud>wsl --install Ubuntu-22.04
Ubuntu 22.04 LTS을(를) 시작하는 중...
Installing, this may take a few minutes...
Please create a default UNIX user account. The username does not need to match your Windows username.
For more information visit: https://aka.ms/wslusers
Enter new UNIX username: gotocloud
New password:
Retype new password:
passwd: password updated successfully
작업을 완료했습니다.
Installation successful!
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

Welcome to Ubuntu 22.04.3 LTS (GNU/Linux 5.15.146.1-microsoft-standard-WSL2 x86_64)

* Documentation: https://help.ubuntu.com
* Management: https://landscape.canonical.com
* Support: https://ubuntu.com/advantage


This message is shown once a day. To disable it please create the
/home/gotocloud/.hushlogin file.
gotocloud@DESKTOP-SNMQ2D4:~$
Update Linux OS and install basic packages

$ sudo apt-get -y update
$ sudo apt-get -y install vim nano net-tools iputils-ping csh gnome-terminal
Install development packages

$ sudo apt-get install -y build-essential flex zlib1g-dev libgmp-dev libmpfr-dev texinfo cmake

## Export WSL distribution image for reuse

To avoid installing the necessary WSL image every time, and to reuse a distribution that has been configured with the basic packages and development environment, you perform an export. This exported distribution can be used to configure the desired WSL image, and it can be moved to another computer or shared.

Before exporting, you stop the running WSL image and then execute the export. You export the Ubuntu-22.04 WSL distribution with the filename Ubuntu22.04-base.vhdx.

C:\Users\gotocloud>wsl --shutdown Ubuntu-22.04
C:\Users\gotocloud>wsl --terminate Ubuntu-22.04
C:\Users\gotocloud>wsl --export Ubuntu-22.04 Ubuntu22.04-base.vhdx --vhd
내보내기가 진행 중입니다. 이 작업은 몇 분 정도 걸릴 수 있습니다.
작업을 완료했습니다.

The Ubuntu22.04-base.vhdx file has been created as follows. You can import this file to create a new WSL distribution.

C:\Users\Bosung Lee>dir Ubuntu22.04-base.vhdx
C 드라이브의 볼륨에는 이름이 없습니다.
볼륨 일련 번호: 3C96-7739

C:\Users\Bosung Lee 디렉터리

05-22 오후 12:15 2,797,600,768 Ubuntu22.04-base.vhdx
1개 파일 2,797,600,768 바이트
0개 디렉터리 183,857,647,616 바이트 남음


When you want to remove an installed distribution, you use the wsl –unregister command.

C:\Users\gotocloud>wsl --unregister Ubuntu-22.04
등록 취소 중입니다.
작업을 완료했습니다.

## Install new WSL distribution using import

The exported vhdx file is imported to create a new WSL distribution as follows. “MyUbuntu-22.04” is the name of the newly created WSL distribution, and the period (.) denotes the current directory, which is where the base disk for the WSL image, ext4.vhdx, will be stored. If you specify a desired directory name here, the base disk will be created in that directory. When creating multiple WSL distributions, the ext4.vhdx should be stored in different directories.

The imported distribution is run with the user account “gotocloud” that was set up during image creation. The -d option specifies the name of the distribution to run.

```
C:\Users\gotocloud>wsl --import MyUbuntu-22.04 . Ubuntu22.04-base.vhdx --vhd
C:\Users\gotocloud>wsl ~ -u gotocloud -d MyUbuntu-22.04
gotocloud@DESKTOP-SNMQ2D4:~$
```
