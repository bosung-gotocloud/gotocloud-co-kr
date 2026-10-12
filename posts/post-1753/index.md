---
title: "OpenStack Mitaka Step-by-Step 설치 (3)"
date: 2016-08-16T21:35:56+09:00
source: https://gotocloud.co.kr/?p=1753
categories: []
tags: []
---

## 2. 설치 환경 구성

이 절에서는 Figure 8에 나타나 있는 컨트롤러와 컴퓨트 노드 설치 환경 구성에 대해서 설명한다.

### 2.1 물리적 환경 구성

물리적인 두 대의 호스트 서버를 이용하여 OpenStack을 설치하고자 할 경우는 Figure 8에서와 같이 두 대의 서버를 네트워크 스위치에 연결한다. External Network와 Management Network 및 Install Network 별로 별도의 네트워크 스위치를 사용하는 것을 권장한다. 하드웨어 구성이 완려되면 호스트 서버 설치 및 구성으로 진행한다.

### 2.2 VMware Player 설치 환경 구성

OpenStack 설치를 위한 기본 구성에는 컨트롤러와 컴퓨트 노드 두 대가 필요한데, 현실적으로 두 대의 물리적인 서버가 없을 경우에는 한 대의 호스트 컴퓨터에 두 대의 가상 머신을 설치하여 시스템을 구성할 수 있다. 데스크탑 PC나 노트북 등에서 가상환경을 구성하기 위한 프로그램으로는 오픈소스인 Oracle의 VirtualBox나 VMware의 VMware Workstation Pro또는 VMware Player 등을 사용할 수 있는데, 여기에서는 비상업적 개인 용도로 사용할 경우 무료로 다운로드가 가능한VMware Player 7.0를 이용하여 환경을 구성하고자 한다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-2-1.pdf” viewer=”google”]
