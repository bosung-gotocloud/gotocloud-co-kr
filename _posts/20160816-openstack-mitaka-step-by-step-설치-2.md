---
title: "OpenStack Mitaka Step-by-Step 설치 (2)"
date: "2016-08-16T21:27:33+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1749"
---

## 1. 준비 단계 점검 사항

OpenStack을 설치하기 위한 준비 사항에 앞서, 어떠한 환경에서 OpenStack을 설치할 것인지를 결정하고, 그에 필요한 사항에 대해서 점검하도록 한다.

### 1.1 시스템 구성

이 가이드에서는 다음의 형태로 시스템을 구성하고자 한다.

- 하드웨어 구성 : 한 대의 컨트롤러 노드와 한 대의 컴퓨트 노드

- 네트워크 옵션 : 셀프서비스 네트워크(External 네트워크 + Management 네트워크)

- 호스트 서버 운영체제 : CentOS 7

- OpenStack 버전 : Mitaka(RDO)

- 설치할 OpenStack 서비스 : Keystone, Glance, Nova, Neutron, Cinder, Horizon

- 가상 환경에서 설치 : VMware Player 환경에서 시스템 구성

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-1.pdf” viewer=”google”]
