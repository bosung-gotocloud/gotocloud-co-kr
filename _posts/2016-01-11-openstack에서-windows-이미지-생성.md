---
title: "OpenStack에서 Windows 이미지 생성"
date: "2016-01-11T14:48:40+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1575"
---

## 1. 클라우드 템플릿 이미지

일반적으로 클라우드에서는 서비스제공자가 다양한 형태의 가상머신 이미지를 템플릿으로 미리 생성해두고, 사용자가 이를 이용하여 가상머신을 생성함으로써 손쉽게 서비스를 구성할 수 있다는 점이 클라우드의 가장 큰 장점인데, 관리자가 제공하는 기본적인 템플릿 이미지 이외에도 사용자는 자신이 생성한 가상머신에 필요한 소프트웨어를 설치하고 구성을 완료한 후 이를 스냅샷 등을 통해 이미지로 저장하여 추후 이를 이용하여 새로운 가상머신을 손쉽게 생성할 수도 있다.

![](/posts/post-1575/images/아마존이미지-300x138.png)

![](/posts/post-1575/images/이노드리드템플릿-300x225.png)

위의 그림에는 아마존 AWS와 국내 클라우드서비스인 Cloudit에서 제공하고 있는 기본적인 가상머신 이미지의 예가 나타나 있다.

OpenStack에서는 Glance라는 가상머신 이미지 서비스를 통해 다양한 다양한 하이퍼바이저에서 사용되는 가상머신 이미지를 템플릿 형태로 저장 및 관리하고 있는데,  OpenStack 관리자 또는 사용자가 다양한 OS용 이미지를 Glance에 업로드하고 이를 이용하여 새로운 가상머신을 생성할 수 있다.

![](/posts/post-1575/images/오픈스택탬플릿-300x167.png)

그림은 필자가 사용하고 있는 OpenStack에 저장되어 있는 이미지를 보여주고 있다. OpenStack의 이미지 서비스인 Glance에 대한 설명은 [OpenStack Class] 제9강 이미지 서비스! GLANCE 나 [OpenStack] Image Service, Glance 등의 블로그를 참조하기 바란다.

## 2. OpenStack Windows 이미지

이 글에서는 OpenStack에서 사용될 이미지를 생성하는 방법 중에서도 특히 Windows 가상머신 이미지를 생성하는 방법에 대해서 정리하고자 한다. 기존의 다양한 글에서 OpenStack 용 가상머신 이미지를 생성하는 방법을 설명하고 있는데, 여기에는 주로 리눅스 KVM 환경에서 Windows 설치 이미지를 이용하여 가상머신 이미지를 생성하고, 이를 OpenStack Glance 에 업로드하는 방법이 설명되어 있다. Windows Image Preparation for OpenStack에서는 Linux에서 virt-manager를 이용하여 Windows 가상머신을 생성하고, 이를 Glance에 업로드하는 방법을 설명하고 있고, OpenStack Virtual Machine Image Guide에서도 virt-install을 이용하여 Windows 이미지를 생성하는 방법을 설명하고 있다. 또는 직접 Windows 설치하지 않고 Cloudbase와 같은 업체에서 미리 생성해 놓은 Windows 이미지를 다운로드하여 OpenStack에 업로드하여 사용할 수도 있다.

그런데, 미리 만들어진 이미지를 다운로드해서 사용하지 않고, 자신만의 Windows 이미지를 직접 생성하고자 하는데, 이미지 생성용 리눅스 머신은 준비되어 있지 않아 직접 OpenStack에서 Windows 이미지를 생성할 수 있는 방법에 대해서 설명한 글은 별로 없는 듯하다. 그래서 이 글에서는 Windows 설치 이미지를 이용하여 OpenStack 상에서 바로 Windows 가상머신 이미지를 생성하고 이를 Glance에 등록하는 방법에 대해서 설명해보고자 한다.

## 3. OpenStack에서 Windows 이미지 생성 문제점

OpenStack에서 직접 Windows 가상머신 이미지를 생성하기 위해서 일반적으로 다음과 같은 방법을 생각할 수 있다.

- Glance에 Windows 설치 이미지 업로드

- 업로드한 설치 이미지를 이용하여 가상머신 생성

- 설치 이미지를 이용하여 운영체제 설치

- 설치된 가상머신을 이미지로 변환

- 변환된 이미지를 Glance에 저장

리눅스의 경우 위의 1~5의 과정으로 가상머신 템플릿을 생성하는데 큰 문제는 없는데, 윈도우의 경우 몇가지 문제점에 직면하게 된다.

![](/posts/post-1575/images/사용자-지정-0-300x54.png)

![](/posts/post-1575/images/사용자-지정-1-300x300.png)

일반적으로 그림처럼 Glance에 설치 이미지(이글에서는 Windows 8.1 32bit 설치 이미지를 사용한다)를 ISO 형태로 업로드하고 가상머신을 생성한 후 콘솔에서 Windows 설치를 시작하게 되면 첫번째로 다음과 같이 운영체제를 설치할 디스크가 보이지 않는 문제에 직면한다. 이를 해결하기 위해서는 설치이미지에 미리 VirtIO 드라이버를 넣어두고 설치 시에 드라이버를 불러들이거나, 혹은 설치용 디스크를 가상머신 생성 시에 미리 추가해 두고 여기에 설치하는 방법 등이 필요하다. 이에 대해서는 Windows Image Preparation for OpenStack 이나 Running Windows 7 guests on OpenStack Icehouse 등의 자료를 참고하기 바란다.

![](/posts/post-1575/images/사용자-지정-2-300x225.png)

설치를 완료한 후 장치 관리자를 보면 네트워크 드라이버가 제대로 설치되어 있지 않아서 드라이버 업데이트가 필요한데 문제는 가상머신 내에서 네트워크가 동작하지 않아서 네트워크 드라이버를 다운로드할 수가 없다는 점이다.

![](/posts/post-1575/images/사용자-지정-20-300x219.png)

따라서  Windows 이미지를 OpenStack에서 직접 생성하기 위해서는 설치 이미지에 VirtIO 드라이버를 미리 넣어두고 이를 이용하여 설치를 진행하는 추가적인 과정이 필요하게 된다. 이 글에서는 Windows 설치 이미지에 VirtIO 드라이버를 저장하고 이를 이용하여 OpenStack 상에서 바로  Windows 이미지를 생성해서 Glance에 저장하는 과정을 정리하고자 한다.

## 4. OpenStack에서 Windows 이미지 생성

이 절에서 설명할 OpenStack에서 Windows 이미지 생성 절차는 다음과 같다.

- Windows 설치 ISO 이미지에  VirtIO 드라이버 저장

- Glance에 ISO 이미지 업로드

- ISO 이미지로 Windows 가상 머신 생성

- OS 설치용 Volume 생성 및 Windows 가상머신에 연결

- Windows OS 설치

- Windows 가상머신에 VirtIO 드라이버 설치

- Windows 업데이트 및 원격접속 설정

- Sysprep 실행을 통한 일반화

- OS 설치 볼륨을 이미지로 변환

### 4.1 Windows 설치 이미지에 VirtIO 이미지 저장

먼저 https://fedoraproject.org/wiki/Windows_Virtio_Drivers 에서 Windows 용 VirtIO 드라이버 IOS를 다운로드한다.

![](/posts/post-1575/images/사용자-지정-3-300x120.png)

다운로드한 VirtIO 드라이버의 압축을 풀어 virtio-win이라는 폴더에 아래의 그림과 같이 드라이버 이미지의 파일을 복사해 둔다.

![](/posts/post-1575/images/사용자-지정-5-300x182.png)

Windows 설치 ISO를 UltraISO 와 같은 ISO 이미지 관리 프로그램을 사용하여 연 다음에 virtio-win 폴더를 설치 ISO에 복사한 후 Windows_8.1_x86-virtio.iso 라는 이름으로 저장한다.

![](/posts/post-1575/images/virtio-win-iso-300x108.jpg)

### 4.2 Glance에 VirtIO 드라이버가 포함된 설치이미지 업로드

![](/posts/post-1575/images/사용자-지정-10-300x68.png)

Glance에 VirtIO 드라이버가 포함된 Windows 설치 ISO를 업로드한다.

### 4.3 ISO 이미지로 Windows 가상 머신 생성

다음으로 업로드한 ISO 설치 이미지를 이용하여 Windows 가상머신을 생성한 후 가상머신을 Shutoff 한다.

![](/posts/post-1575/images/사용자-지정-9-1-284x300.png)

### 4.4 OS 설치용 Volume 생성 및 Windows 가상머신에 연결

다음으로  Windows OS를 설치할 Volume을 생성한다. 이 글에서는 OS 설치용 볼륨의 크기를 40GB로 지정하였다.

![](/posts/post-1575/images/사용자-지정-11-300x263.png)

다음으로 생성된 Volume에 대해서 Manage Attachment 메뉴를 이용하여 앞에서 생성해 둔 Windows 가상머신에 연결한다.

![](/posts/post-1575/images/사용자-지정-12-300x143.png)

![](/posts/post-1575/images/사용자-지정-13-300x198.png)

![](/posts/post-1575/images/사용자-지정-14-300x90.png)

위의 그림과 같이 40GB Volume이 Windows 8.1 x86 가상머신에 /dev/hdb로 연결되어 있다.

### 4.5 Windows OS 설치

Volume을 연결한 후에 Windows 설치를 시작하면 3장에서와 는 달리 추가로 연결한 Volume이 설치 화면에서 나타나며 이 Volume에 Windows를 설치를 시작한다.

![](/posts/post-1575/images/사용자-지정-15-300x224.png)

![](/posts/post-1575/images/사용자-지정-16-300x225.png)

설치가 완료되면 admin 계정을 생성한다. 네트워크가 연결되어 있지 않으므로 로컬계정만 생성할 수 있다.

![](/posts/post-1575/images/사용자-지정-18-300x224.png)

Windows 설치가 완료된 후 생성한 계정으로 Windows에 로그인할  수 있다. 네트워크 드라이버가 설치되지 않아서 네트워크에 연결되지 않았음을 우측 하단의 작업표시줄에서 알 수 있다.

![](/posts/post-1575/images/사용자-지정-19-300x224.png)

### 4.6 Windows 가상머신에 VirtIO 드라이버 설치

설치 후에 Windows 가상 머신의 장치관리자를 실행해 보면 그림과 같이 드라이버 들이 제대로 설치되지 않았음을 알 수 있다.

![](/posts/post-1575/images/사용자-지정-201-300x219.png)

VirtIO 드라이버 설치를 위해 내컴퓨터를 실행하면 설치 이미지가 CD 드라이브로 연결되어 있음을 알 수 있다. CD 드라이브를 열어서 설치 ISO에 미리 저장해 둔 virtio-win 폴더에 접근한다.

![](/posts/post-1575/images/사용자-지정-21-300x224.png)

![](/posts/post-1575/images/사용자-지정-22-300x225.png)

각 드라이버 폴더에 들어가서 inf 파일을 선택한 후 “설치”를 눌러 드라이버를 설치한다. 모든 드라이버에 대해서 이와 같이 설치한다.

![](/posts/post-1575/images/사용자-지정-23-300x225.png)

![](/posts/post-1575/images/사용자-지정-24-300x225.png)

![](/posts/post-1575/images/virtio설치완료-296x300.png)

VirtIO 드라이버가 정상적으로 설치되었음을 장치관리자를 통해 확인할 수 있다.

### 4.7  Windows 업데이트 및 원격접속 설정

다음으로 Windows 이미지의 사용 편의를 위해 Windows 업데이트와 원격 접속 설정을 허용한다. 이외에도 사용자가 필요로하는 소프트웨어가 있다면 설치하는 과정을 진행한다. (가상머신에 대해서 추후에 원격접속을 원할 경우 가상머신에서의 원격접속과 함께 OpenStack의 Security Group에서 3389 포트를 허용해야 접속이 가능하다)

![](/posts/post-1575/images/사용자-지정-28-300x225.png)

![](/posts/post-1575/images/사용자-지정-271-273x300.png)

### 4.8 Sysprep 실행을 통한 일반화

Windows 가상 머신을 클라우드나 가상화 환경에서 운영할 때는 반드시 일반화(generalization) 과정을 거쳐야 한다.  Windows의 일반화란 Windows 머신의 복제, 감사 및 고객 제공을 위해 Windows 설치를 준비하는 과정으로 Windows에 포함된 Sysprep (System Preparation) 도구를 사용하여 수행하게 된다. 이러한 일반화 과정을 거치지 않고 Windows 머신을 복제할 경우 (하드 디스크를 통째로 복사하거나, 가상머신 이미지 복제를 통해 Windows 가상머신을 생성하는 경우)에는 복제된 Windows 와 원본 Windows의 SID가 동일하여 Active Directory에 Join 하지 못하는 등 문제가 발생한다. 이러한 문제를 방지하기 위하여 클라우드 환경이나 가상화 환경에서는 sysprep을 실행하여 일반화된 형태로 템플릿 이미지를 생성해 두거나, 혹은 가상머신의 복제 후에 cloudbase-init과 같은 초기화 서비스를 설치하여 가상머신이 생성될 때마다 자동으로 초기화가 수행되도록 해야한다. 이 글에서는 sysprep을 이용하여 일반화가 완료된 상태로 가상머신 이미지를 저장하는 방법을 설명하고자 한다.

![](/posts/post-1575/images/사용자-지정-33-300x195.png)

위의 그림과 같이 Windows 가상 머신에서 관리자 명령 프롬프트를 실행한 후 c:\windows\system32\sysprep.exe 를 실행한 후 “시스템 OOBE(첫 실행 경험) 시작”을 선택하고 “일반화(G)”를 체크한 후 “시스템 종료”를 선택하고 “확인”을 누른다.

![](/posts/post-1575/images/사용자-지정-34-300x196.png)

그림과 같이 Sysprep가 실행되고 Windows 가상머신의 일반화가 완료되면 가상 머신이 종료된다.

### 4.9 OS 설치 볼륨을 이미지로 변환

앞절에서 sysprep가 완료된 후 Windows 가상머신이 종료되면 OS가 설치된 Volume을 이미지로 변환한다.

![](/posts/post-1575/images/사용자-지정-36-300x139.png)

그림과 같이 Manage Volume Attachments 메뉴에서 Windows 가상 머신에 연결되어 있는 Volume을 해제한다. (Windows 가상머신이 종료되지 않으면 해제할 수 없으므로, 가상머신을 종료한다)

![](/posts/post-1575/images/사용자-지정-37-300x138.png)

![](/posts/post-1575/images/사용자-지정-38-300x154.png)

해제된 Volume에 대해서 Upload Image를 선택하여 Glance에 Windows 8.1 x86 Base라는 이름의 이미지로 QCOW2 포맷으로 등록한다.

![](/posts/post-1575/images/사용자-지정-39-300x78.png)

![](/posts/post-1575/images/사용자-지정-40-300x73.png)

위와 같이 Windows 8.1 x86 Base라는 Windows 가상머신 이미지가 등록되었음을 볼 수 있다.

## 5. Windows 이미지를 이용한 가상머신 생성

4장에서 생성한 Windows 이미지를 이용하여 가상머신이 정상적으로 생성되는지를 확인해보고자 한다.

먼저 4장에서 업로드한 Windows 8.1 x86 Base 이미지를 이용하여 Windows 가상머신을 생성한다.

![](/posts/post-1575/images/사용자-지정-41-300x300.png)

![](/posts/post-1575/images/사용자-지정-42-300x73.png)

그림과 같이 가상머신이 정상적으로 생성되었음을 알 수 있고, 콘솔에 접속하면 다음의 그림과 같이 Windows를 처음 설치했을 때와 같이 초기 설정화면을 볼 수 있는데 이는 Sysprep을 이용하여 초기화된 상태로 이미지를 생성하였기 때문이다.

![](/posts/post-1575/images/사용자-지정-44-300x225.png)

이상으로 OpenStack 에서 직접 Windows 이미지를 생성하여 Glance에 업로드하는 과정을 정리하였다. 이글에서는 sysprep을 이용하여 일반화된 Windows 가상머신 이미지를 생성하는 방법에 대해서만 언급하였는데, 실제 다량의 Windows 가상머신을 자동으로 생성하기 위해서는 sysprep 을 자동화한 스크립트나 cloudbase-init과 같은 형태의 서비스를 가상머신에 설치하고 이를 이미지로 저장해두는 것이 필요할 수 있을 것이다.

이 글에서 생성한 Windows 가상 머신 이미지는 다음의 링크에서 다운로드 할 수 있다.

Windows 8.1 x86 Base  이미지 다운로드
