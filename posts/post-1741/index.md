---
title: "OpenStack Mitaka Step-by-Step 설치 (1)"
date: 2016-08-16T21:12:35+09:00
source: https://gotocloud.co.kr/?p=1741
categories: []
tags: []
---

## 0. OpenStack개요

### 0.1 서비스 형 인프라(Infrastructure-as-a-Service, IaaS) 클라우드

서비스 형 인프라(Infrastructure-as-a-Service, IaaS) 클라우드는 IT 인프라 자원인 CPU, 메모리, 디스크, 네트워크 및 OS를 인터넷을 통해 셀프 서비스 포털에서 쉽고 빠르게 생성, 관리, 모니터링 할 수 있는 클라우드 플랫폼을 의미한다.

IaaS 클라우드는 서버가상화(하이퍼바이저), 스토리지(블록스토리지, 네트워크 스토리지, 오브젝트 스토리지 및 로컬 스토리지), 네트워크 가상화(L2, L3 스위치, 라우터 및 방화벽, VPN 등), 클라우드 관리(Stack), 과금 및 모니터링 솔루션이 통합되어 사용자에게 셀프 서비스 포털을 통해서 원하는 IT 자원을 제공하게 된다. Figure 1은 IaaS 클라우드 아키텍처를 나타낸 그림으로, IaaS 클라우드는 서버, 스토리지, 네트워크 장치 등으로 구성된 물리적 Layer 위에, 서버가상화, 스토리지 가상화, 네트워크 가상화를 지원하는 가상화 Layer가 위치하게 되며, 이러한 가상 자원을 구성하기 위한 프로비저닝 Layer와 클라우드 관리를 위한 Layer로 구성된다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-0.pdf” viewer=”google”]
