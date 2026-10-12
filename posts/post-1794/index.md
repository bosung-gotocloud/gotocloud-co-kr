---
title: "OpenStack Mitaka Step-by-Step 설치 (10)"
date: 2016-08-16T23:25:58+09:00
source: https://gotocloud.co.kr/?p=1794
categories: []
tags: []
---

## 4.6 대시보드(Dashboard)

대시보드(horizon)는 웹 인터페이스 기반으로 클라우드 관리자와 사용자가 다양한 OpenStack 의
자원과 서비스를 관리할 수 있도록 한다.

이 가이드에서는 Apache 웹서버를 사용하여 대시보드를 구성한다.

### 4.6.1 설치 및 구성

이 섹션에서는 컨트롤러 노드에 대시보드를 설치하고 구성하는 과정에 대해서 설명한다.
대시보드는 자격증명, 이미지, 컴퓨트 및 네트워킹 등 핵심 서비스를 바탕으로 동작하며 오브젝트
스토리지와 같은 독립 서비스는 대시보드를 필요로 하지 않는다.
이 섹션은 Apache HTTP 서버와 Memcached 서비스를 사용하여 자격증명 서비스가 설치, 구성되고
동작한다고 가정하고 진행한다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4-6.pdf” viewer=”google”]
