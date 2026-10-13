---
title: "OpenStack Mitaka Step-by-Step 설치 (6)"
date: "2016-08-16T23:04:36+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1776"
---

## 4.2 자격증명(Identity) 서비스

### 4.2.1 자격증명 서비스 개요

OpenStack 자격증명(Identity) 서비스는 인증, 권한 관리 및 서비스 카탈로그 제공을 위한 통합된
서비스로 Keystone이라는 프로젝트 명을 갖는다. OpenStack의 다른 서비스들에서는 공통 API형태
로 자격증명 서비스가 사용되며, OpenStack에서 직접 사용자를 생성하지 않고, LDAP과 같은 기존
시스템과의 통합을 통해 사용자 정보를 제공할 수 있다.
OpenStack 자격증명 서비스와 통합된 다른 서비스에서 사용자 요청이 발생하면 자격증명 서비스를
통해 사용자 권한 부여를 수행하고, 각 서비스들은 사용자 요청을 수행하게 된다.
자격증명 서비스는 다음의 구성 요소로 이루어져 있다.

[embeddoc url=”https://gotocloud.co.kr/wp-content/uploads/2016/08/chapter-4-2.pdf” viewer=”google”]
