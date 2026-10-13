---
title: "Windows 8.1에서 Hyper-V 사용 (1)"
date: "2014-10-24T18:23:15+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1106"
---

### 1. Microsoft Hyper-V 개요

마이크로소프트 Hyper-V는 Windows Server 2008 x64 버전에서 서버 가상화를 지원하기 위해서 Microsoft가 2008년 6월 공개한 하이퍼바이저(Hypervisor)로 VMware의 vSphere, Citrix의 XenServer 및 RedHat의 KVM과 함께 x86 시스템에서 구동되는 대표적인 하이퍼바이저 중의 하나이다. 타사의 하이퍼바이저와 달리 Windows OS에 통합되어 제공된다는 점에서 별도의 비용이 들지 않고 손쉽게 사용자가 자신의 윈도우 시스템에서 가상 머신을 구동할 수 있다는 점에서 최근 널리 확산되고 있다. 최근의 가트너 발표에 의하면 VMware의 vSphere에 이어 하이퍼바이저에서 2위의 시장점유율을 기록하고 있다고 한다. 하이퍼바이저는 클라우드 컴퓨팅 구현의 기반 기술로 클라우드를 구축하기 위한 필수 요소인데 마이크로소프트는 자사의 클라우드 서비스인 Microsoft Azure를 Hyper-V 기반으로 구축하여 운영하고 있다는 점에서 앞으로도 지속적으로 발전될 것으로 생각된다.

### 2. 윈도우 8.1 Hyper-V 지원

Hyper-V는 원래 Window Server 2008에서 최초로 지원되기 시작하여 Windows Server 2012에 기본으로 포함된 하이퍼바이저로 Windows 서버에서만 지원되던 기능이었으나 최근에 발표된 Windows 8에도 포함되어 데스크탑 사용자 들도 자신의 PC에서 손쉽게 가상 머신을 별도의 비용없이 구동할 수 있게 되었다. 데스크탐에서 가상머신을 구동하기 위한 소프트웨어로는 VMware Workstation, VMware Player 등의 상용 솔루션(VMware Player는 개인에 한해 무료이다)을 설치하거나 Oracle에 인수된 VirtualBox 등 오픈소스 기반의 데스크탑용 하이퍼바이저가 알려져 있는데 많은 사용자들에게 Windows 8에 기본적으로 Hyper-V가 내장되어 있다는 사실은 잘 알려져 있지 않는 것이 현실이다. 이 글에서는 Windows 8 이상에서 지원되는 Hyper-V에 대한 사용법과 이를 바탕으로 데스크탑 PC에서 가상 머신을 생성하고 구동하는 방법을 설명하고자 한다. 이를 통해 사용자들은 별도의 비용을 지불하지 않고서도 자신의 데스크탑에서 다양한 가상 머신을 사용할 수 있으며 데스트탑에서 생성한 가상 머신을 별도의 변환 없이 Hyper-V 기반의 Windows 서버로 이전할 수 있다는 점에서 많은 장점을 얻을 수 있을 것이다.

### 3. Hyper-V를 구동하기 위한 Windows OS 요구 사항

데스크탑 PC에서 Hyper-V를 구동하기 위한 최소 요구 사항은 다음과 같다.

- Windows 8 Pro 또는 Windows 8 Enterprise 64bit

- 최소 4GB 메모리

- SLAT (Second Level Address Transition)을 지원하는 64 bit 프로세스

- BIOS에서 하드웨어 가상화 (Virtualization)  지원

SLAT는 인텔의 네할렘(Nehalem) 이후의 프로세서와 AMD의 바르셀로나 이후의 프로세서에서 지원되는 기능이고 BIOS에서 다음과 같이 Virtualization을 지원하는지 확인하고 이를 활성화 해야 한다.

![](/posts/post-1106/images/6116_HVW8a-300x182.jpg)

사용자는 Hyper-V를 데스크탑 PC에서 실행하기 이전에 먼저 자신의 프로세서가 SLAT를 지원하면서 BIOS에서 위와 같이 가상화 기능(VTx)를 지원하고 있는지 사전에 확인하기 바란다. 최근에 판매되고 있는 대부분의 PC에서는 위의 기능이 지원되고 있으므로 Hyper-V의 구동에 크게 문제가 없을 것으로 생각된다.

다음 글에서는 Hyper-V 기능을 활성화하는 방법에 대해서 알아보고자 한다.
