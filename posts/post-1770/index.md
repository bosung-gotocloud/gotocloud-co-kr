---
title: "OpenStack Mitaka Step-by-Step 설치 (5)"
date: 2016-08-16T21:57:36+09:00
source: https://gotocloud.co.kr/?p=1770
categories: []
tags: []
---

## 4. OpenStack 설치 및 구성

이 절에서는 컨트롤러 노드와 컴퓨트 노드에 OpenStack을 구성하는 서비스 들을 실제로 설치하는 과정을 설명한다. 이 절에서의 진행 순서는 다음과 같다.

- 공통 서비스 설치

- 자격증명(Identity) 서비스 – Keystone

- 이미지(Image) 서비스 – Glance

- 컴퓨트 서비스 – Nova

- 네트워킹 서비스 – Neutron

- 대시보드 서비스 – Horizon

- 블록스토리지 서비스 – Cinder

이 절에서 설명할 내용은 OpenStack의 설지 가이드를 기본으로 진행한다.

### 4.1 공통 서비스 설치

먼저 OpenStack 서비스에서 공통으로 사용될 패키지와 서비스 들을 설치한다. 다음의 모든 과정은 OS에 루트로 로그인하여 실행되어야 한다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4.pdf” viewer=”google”]
