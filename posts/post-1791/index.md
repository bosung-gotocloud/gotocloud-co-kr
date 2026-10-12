---
title: "OpenStack Mitaka Step-by-Step 설치 (9)"
date: 2016-08-16T23:21:39+09:00
source: https://gotocloud.co.kr/?p=1791
categories: []
tags: []
---

## 4.5 네트워킹(Networking) 서비스

이 장에서는 프로바이더 네트워크와 셀프서비스 네트워크 옵션 중에서 셀프 서비스 네트워크 옵션을
사용하여 네트워킹 서비스(Neutron) 서비스를 설치하고 구성하는 과정을 설명한다. 가상 네트워크
구성 요소, 레이아웃 및 트래픽 흐름에 대한 추가적인 정보는 네트워킹 가이드를 참조하기 바란다.

### 4.5.1 네트워킹 서비스 개요

OpenStack 네트워킹 서비스인 Neutron 에서는 Openstack 의 다른 서비스와 통신할 수 있도록
인터페이스 디바이스를 생성하고 연결할 수 있다. 이러한 플러그인 구조는 OpenStack 아키텍쳐와
배포 방식에 유연성을 제공할 수 있는 다양한 네트워킹 장비와 소프트웨어의 조합으로 구현된다.
여기에는 다음과 같은 구성 요소가 포함된다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4-5.pdf” viewer=”google”]
