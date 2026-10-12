---
title: "ownCloud에서 2GB 이상 파일 올리기"
date: "2013-11-08T21:19:30+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=934"
---

ownCloud를 설치하고 사용하다보면 큰 파일(2GB 이상)을 업로드해야할 필요가 생긴다. 이에 대해서는 Forum 등에서 무수히 많은 질문과 답글이 있는데, 해결 방안이 명쾌하게 나와있는 경우가 별로 없다. php.ini 설정의 upload_max_filesize를 8G 로 바꾸기, .htaccess 파일의 php_value upload_max_filesize와 php_value post_max_size를 변경해보는 등의 시도를 해도 2GB 이상의 파일을 업로드하는 것이 불가능해 보였다. 이러한 문제로 인해 FTP 등을 사용하여 owncloud/data/사용자/files 아래에 직접 파일을 업로드하거나 Sync 클라이언트를 사용하여 동기화해서 업로드하는 방법을 사용하는 등 상당히 불편할 수 밖에 없었다.

큰 사이즈의 파일 업로드 제한의 원인은 ownCloud를 설치할 때 사용하는 php 의 버전이 32 bit 이기 때문으로 알려져 있고 64 bit의 php를 설치하면 해결할 수 있다고 한다. 32bit php의 2GB 파일 사이즈 제한에 대해서는 http://forum.owncloud.org/viewtopic.php?f=23&t=10695를 참조하기 바란다.

이 글에서는 CentOS 6에 설치된 ownCloud 5에서 php 버전을 기본 CentOS의 5.3에서 64비트를 지원하는 5.5 버전으로 업그레이드 하여 2GB 가 넘는 파일을 업로드할 수 있도록 변경하는 과정을 설명하고자 한다. CentOS 6에 ownCloud 5를 설치하는 과정은 ownCloud 5 설치를 참조하기 바라며 이미 CentOS 6에 ownCloud 5가 설치되어 있는 상태에서 그 과정을 설명할 것이다

PHP 5.5.3은 2013년 8월 22일 PHP.net에서 릴리즈되었으며 CentOS/RHEL 5.9와 CentOS 6에서 yum을 통해 설치가 가능하다. PHP 5.5.3의 주요 특징은 다음과 같으며 자세한 내용은 What has changed in PHP 5.5.x  를 참조하기 바란다.

- Zend Optimizer+ opcode cache included, now known as opcache extension

- Generators

- try { } finally { }

- Literal dereferencing for arrays and strings

- Array return value de-referencing

- Class name resolution

- Password hashing API

- and much more

먼저 PHP 5.5.3을 설치하기 위하여 ownCloud 5가 설치되어 있는 서버에 root로 로그인하여 다음의 명령어로 Webtatic EL yum 저장소 정보를 추가한다.

> CentOS / RHEL 6.x :
> # rpm -Uvh http://mirror.webtatic.com/yum/el6/latest.rpm
> CentOS/RHEL 5.x :
> # rpm -Uvh http://mirror.webtatic.com/yum/el5/latest.rpm

저장소 정보를 추가한 후 다음의 명령어로 PHP를 5.5 버전으로 업그레이드 한다.

> # yum install yum-plugin-replace
> # yum replace php-common –replace-with=php55w-common
> # yum install php55w-opcache

위의 명령어를 수행하면 ownCloud 5 설치시 설치했던 PHP 관련 패키지들도 모두 업그레이드 된다.

업그레이드를 완료한 후 php.ini 의 upload_max_filesize 를 수정한다. (이 글에서는 8G로 설정하였다.)

> # vi /etc/php.ini
> upload_max_filesize = 8G

그리고 ownCloud 5의 설치 디렉토리의 .htaccess 파일에서 php_value upload_max_filesize 와 php_value post_max_size 도 수정한다. 역시 이 글에서는 8G 로 설정하였다.

> # vi .htaccess
> php_value upload_max_filesize 8G
> php_value post_max_size 8G

위의 과정을 완료한 후 apache 웹서버를 재시작한다.

> # service httpd restart

ownCloud 5 웹서버를 재시작한 후 ownCloud 5 에 admin 계정으로 로그인한 후 admin -> 관리자 페이지에서 최대 업로드 크기를 앞에서 설정한 최대 값 (8 GB)로 변경한다.

![](/posts/post-934/images/ownCloud-최대-업로드-크기-21-300x212.png)

이상의 과정을 완료하면 2GB 가 넘는 큰 파일도 문제 없이 업로드가 가능하다.
