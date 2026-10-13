---
title: "OpenStack Mitaka Step-by-Step 설치 (11)"
date: "2016-08-16T23:28:41+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1797"
---

## 4.7 블록 스토리지 서비스

OpenStack 블록 스토리지 서비스는 게스트 인스턴스에 블록 스토리지 디바이스를 제공하는
서비스이다. 이 서비스에서는 블록 스토리지 드라이버나 다양한 벡엔드 구성을 통해 스토리지가
제공되고 사용된다. 지원되는 블록스토리지 드라이버로는 NAS/SAN, NFS, iSCSI, Chep 등이 있으며
블록 스토리지 API 와 스케쥴러는 일반적으로 컨트롤러 노드에서 실행되고 볼륨 서비스는 사용되는
드라이버에 따라 컨트롤러 노드나 컴퓨트 노드 또는 별도의 블록 스토리지 노드에서 실행된다. 더
자세한 정보는 설정 레퍼런스를 살펴보기 바란다.

### 4.7.1 블록 스토리지 서비스 개요

OpenStack 블록 스토리지 서비스(cinder)에서는 가상 머신에 고정적인 스토리지를 추가할 수 있다.
블록 스토리지는 볼륨 관리를 위한 인프라와 함께 OpenStack 컴퓨트와 상호작용하여 인스턴스에
볼륨을 제공한다. 이와 함께 볼륨 스냅샷 및 볼륨 유형 관리가 가능하다.
블록 스토리지 서비스는 다음의 구성요소로 이루어져 있다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4-7.pdf” viewer=”google”]
