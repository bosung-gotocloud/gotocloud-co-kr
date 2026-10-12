---
title: "OpenStack Mitaka Step-by-Step 설치 (4)"
date: 2016-08-16T21:47:28+09:00
source: https://gotocloud.co.kr/?p=1765
categories: []
tags: []
---

## 3. 컨트롤러, 컴퓨트 노드 OS 설치 및 구성

이 절에서는 OpenStack을 설치할 컨트롤러 노드와 컴퓨트 노드에 운영체제를 설치하고, 기본적인 구성을 설명한다.

### 3.1 운영 체제 설치

컨트롤러 노드와 컴퓨트 노드는 CentOS 7 64 bit를 설치한다. CentOS 7 64bit Minimal 버전을 사용한다. CentOS 인스톨러를 시작한 후 다음의 과정을 고려하여 설치를 진행한다.

 

- INSTALLATION DESTINATION을 선택한 후 20 GB 용량의 sda를 운영체제 설치 디스크로 선택한다. 나머지 두 개의 디스크는 운영체제 설치 후에 별도로 설정한다.[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-3.pdf” viewer=”google”]
