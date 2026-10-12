---
title: "OpenStack Mitaka Step-by-Step 설치 (7)"
date: 2016-08-16T23:09:54+09:00
source: https://gotocloud.co.kr/?p=1787
categories: []
tags: []
---

## 4.3 이미지(Image) 서비스

OpenStack 이미지 서비스인 Glance 는 사용자가 가상 머신 이미지를 검색하고 등록하며 가져올 수
있도록 하는 서비스로 REST API 를 통해 가상 머신 이미지 메타데이타에 대한 질의를 통해 실제
이미지를 가져올 수 있도록 한다. 사용자는 단순한 파일 시스템 뿐만 아니라 OpenStack 오브젝트
스토리지 등 다양한 저장소에 가상 머신 이미지를 저장하고 사용할 수 있다.
이 글에서는 간략하게 이미지 서비스를 컨트롤러 노드에서 구동하고, 컨트롤러 노드의
/var/lib/glance/image 디렉토리에 이미지를 업로드하고 저장하는 파일 벡엔드를 사용하여 이미지
서비스를 구성하는 내용을 설명한다. 이를 위해 컨트롤러 노드에는 이미지를 저장하기 위한 최소 몇
기가바이트 이상의 용량이 필요하다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4-3.pdf” viewer=”google”]
