---
title: "VirtualBox Network Topology"
date: "2024-01-04T00:13:35+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=2304"
---

VirtualBox is a powerful x86 and AMD64/Intel64 virtualization software(VBox for short), which can be used
to construct kinds of debug or test network environments. Sometimes, for the sake of security, some
virtual hosts run parallely on the same physical platform to isolate each other, decrease complexity.

### Network Adapter

VirtualBox provide 8 PCI network adapter for each virtual machine. 4 of them can be conﬁgured with
GUI, and all 8 adapters can be conﬁgured through command.

![](/gotocloud-co-kr/posts/post-2304/images/image-300x219.png)

### Network Types

VirtualBox supports diﬀerent types of network conﬁguration similar to physical network conﬁguration.

- NAT(Network Adress Translation)

NAT is a default option when VirtualBox is installed. VirtualBox provides a NAT router and DHCP
service for every virtual machine.
The same IP address 10.0.2.15 is assigned to all virtual machines from the DHCP in the VirtualBox
and the default gateway address is 10.0.2.2.
All virtual machines can access to the pyhsical network through the NAT provided by the virtualBox.
But access to VM from the outside is not allowed.

![](/gotocloud-co-kr/posts/post-2304/images/NAT-300x204.jpg)

- NAT Networking

All virtual machines are connected to the virtual switch and can access to the physical network
through the NAT like a wiﬁ router at home.
Diﬀerent from NAT, each virtual machine has diﬀerent IP address but shares the same gateway in the
VirtualBox. Each virtual machines can connect to each other.

![](/gotocloud-co-kr/posts/post-2304/images/NAT_Netwok-300x204.jpg)

 

- Bridged Networking

All virtual machines and host machine are bridged in the same ethernet segment. In other words, all

virtual machines are connected to the physical network directly.

In this networking, all virtual machines are accessible from the outside network.

![](/gotocloud-co-kr/posts/post-2304/images/Bridged_Netwok-300x204.jpg)

- Internal Networking

All virtual machines are connected to the virtual switch and can access each other but isolated from

the host machine and outside network.

All virtual machines can not access to the pyshical network and also the host machine can not access

to all virtual machines.

![](/gotocloud-co-kr/posts/post-2304/images/Internal_Netwok-300x204.jpg)

- Host-only Networking

All virtual machinesand host machine are connected to the virtual switch and can access each other

but isolated from the outside network.

The only diﬀerence is that the host machine is added into the internal network.

![](/gotocloud-co-kr/posts/post-2304/images/Host-only_Network-300x204.jpg)

###

### Summary

In the VirtualBox, multiple network interfaces can be set up on one virtual machine. For example, one interface is attached to the NAT network and the other to the Host-only network. NAT network enables connection to the internet and the Host-only network enables the connection from the host machine to the virtual machine.

![](/gotocloud-co-kr/posts/post-2304/images/two-nic-1-300x204.jpg)
