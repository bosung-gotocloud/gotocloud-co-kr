---
title: "OpenStack Mitaka Step-by-Step 설치 (8)"
date: 2016-08-16T23:17:00+09:00
source: https://gotocloud.co.kr/?p=1789
categories: []
tags: []
---

## 4.4 컴퓨트(Compute) 서비스

### 4.4.1 컴퓨트 서비스 개요

OpenStack 컴퓨트(Compute)는 서비스 형 인프라 클라우드 컴퓨팅 시스템의 운영과 관리의 가장
중요한 부분을 담당하는 서비스로 주요 모듈은 파이썬으로 구현되어 있다.
OpenStack 컴퓨트 서비스는 인증을 위한 자격증명 서비스, 디스크와 서버 이미지를 위한 이미지
서비스, 사용자와 관리자 인터페이스를 위한 대시보드와 상호작용하여 동작한다. 이미지 접근은
프로젝트와 사용자 별로 제한되며, 인스턴스의 숫자와 같은 제한은 프로젝트 별로 이루어진다.
OpenStack 컴퓨트는 표준 하드웨어로 수평 확장이 가능하며 이미지를 다운로드하여 인스턴스를
구동한다.
OpenStack 컴퓨트는 다음의 영역과 구성 요소로 구성되어 있다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4-4.pdf” viewer=”google”]
