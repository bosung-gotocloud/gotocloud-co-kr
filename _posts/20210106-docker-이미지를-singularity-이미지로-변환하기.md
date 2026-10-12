---
title: "Docker 이미지를 Singularity 이미지로 변환하기"
date: "2021-01-06T21:10:50+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1913"
---

이 글에서는 Docker 컨테이너 이미지를 Singularity 컨테이너 이미지로 변환하는 방법을 설명한다. Docker와 Singularity에 대한 상세한 설명은 Docker 홈페이지와 Singularity 홈페이지를 참조하기 바란다.

Docker와 Singularity는 이미 설치되어 있어야 하며, 테스트에 사용된 Docker 이미지는 CUDA 10.2가 설치된 Ubuntu 18.04 이다.

 

## Docker 이미지 pull

다음의 명령을 통해 nvidia/cuda:10.2-devel-ubuntu18.04 이미지를 pull 한다.

$ sudo docker pull nvidia/cuda:10.2-devel-ubuntu18.04
정상적으로 Docker 이미지가 다운로드 되었는지를 다음의 명령어로 확인한다.

$ sudo docker image list
다음과 같이 다운로드 된 이미지가 표시된다.

REPOSITORY TAG IMAGE ID CREATED SIZE
nvidia/cuda 10.2-devel-ubuntu18.04 004b2ee0f7e3 3 weeks ago 2.93GB
 

 

## Docker 이미지 실행

Docker 이미지가 정상적으로 실행되는지는 다음의 명령어로 확인한다.

$ sudo docker run -ti --rm nvidia/cuda:10.2-devel-ubuntu18.04 bash
정상적으로 이미지가 실행되면 아래와 같이 이미지 내에서 원하는 패키지를 설치할 수 있다. 이 명령어 들은 이미지 내에서 수행되어야 한다.

root@077bfec24da1:/# apt update
root@077bfec24da1:/# apt upgrade
root@077bfec24da1:/# apt install net-tools openssh-server vim sudo s3fs
 

 

## 최신 Docker 이미지 Commit

Docker 이미지 내에서 원하는 패키지 등을 설치한 후에, 최신 이미지를 commit 한다. 이를 위해 로컬 워크스테이션에서 터미털 창을 하나 더 실행한 후 다음의 명령어를 수행하여 현재 실행 중인 docker 이미지의 id를 확인한다. 출력 결과에서 077bfec24da1 이 실행 중인 이미지의 id 이다.

$ sudo docker ps
CONTAINER ID IMAGE COMMAND
077bfec24da1 nvidia/cuda:10.2-devel-ubuntu18.04 "bash"
 

최신 변경 사항이 반영된 이미지를 docker 저장소에 commit 한다. 이 때 앞에서 docker ps 명령어를 통해 출력된 id인 077bfec24da1 를 사용한다. 저장소에 저장될 이미지의 이름은 cuda_10_2-ubuntu_18_04 로 사용한다.

$ sudo docker commit 077bfec24da1 cuda_10_2-ubuntu_18_04
 

Commit이 정상적으로 수행되면 docker image list 명령어를 통해 이미지를 확인할 수 있다.

$ sudo docker image list
REPOSITORY TAG IMAGE ID
cuda_10_2-ubuntu_18_04 latest 9c1b03c4d306
nvidia/cuda 10.2-devel-ubuntu18.04 004b2ee0f7e3
 

 

## Docker 이미지를 파일로 저장

다음의 명령어를 사용하여, commit 된 최신 docker 이미지를 tar 파일로 저장한다. 저장된 파일 이름은 cuda_10_2-ubuntu_18_04.tar 이다.

 

$ sudo docker save cuda_10_2-ubuntu_18_04:latest -o cuda_10_2-ubuntu_18_04.tar
 

 

## 저장된 Docker 파일 Singularity 파일로 변환

Docker는 sudo 권한으로 실행하는 반면, Singularity는 사용자 권한으로 생성, 삭제 및 이미지 내에서 root 권한 실행 등이 가능하다. 앞에서 Docker 이미지를 sudo 명령어로 파일로 변환할 경우 저장된 파일이 root.root에 속하므로, 이를 사용자와 그룹 권한으로 변경한다. 여기에서 user.group은 실제 사용자의 유저와 그룹으로 변경한다.

$ sudo chown user.group cuda_10_2-ubuntu_18_04.tar
 

변환된 파일에 대해서 다음의 명령어를 사용하여 Singularity 컨테이너 이미지로 변경한다. Singularity 이미지는 현재 실행 디렉토리 아래에 cuda_10_2-ubuntu_18_04.sif 디렉토리로 생성된다.

$ singularity build --sandbox cuda_10_2-ubuntu_18_04.sif docker-archive://cuda_10_2-ubuntu_18_04.tar
 

 

## Singularity 이미지 실행

변환된 Singularity 이미지는 다음의 명령을 통해 실행할 수 있다.

$ singularity shell --writable --fakeroot cuda_10_2-ubuntu_18_04.sif
 

writable 옵션은 이미지 내에서 쓰기 권한을 부여하는 옵션이며, fakeroot 옵션은 이미지 내에서 root 권한을 얻을 수 있는 옵션이다. 이 두가지 옵션을 통해 이미지 내에  원하는 패키지를 설치할 수 있다. 이를 통해 일반 사용자 권한으로 Singularity 이미지를 생성하고, 생성된 이미지 내에서는 root 권한으로  원하는 패키지 등을 설치한 후에, 이 이미지를 Singularity가 설치된 다른 컴퓨터에서 실행할 수 있게 된다.

 

## Singularity 이미지 압축

Docker에서는 변경된 이미지를 저장소에 commit 한 후에 save 명령어를 통해 이를 로컬 파일로 저장하는 반면, Singularity 이미지는 아래의 명령어를 통해 이미지가 생성된 디렉토리를 압축하기만 하면, 다른 컴퓨터에 옮겨서 그대로 사용할 수 있다.

$ tar czf cuda_10_2-ubuntu_18_04.tar.gz cuda_10_2-ubuntu_18_04.sif
 

이 명령어로 생성된 cuda_10_2-ubuntu_18_04.tar.gz 파일은 CUDA 10.2가 설치된 Ubuntu 18.04 버전으로 Singularity 설치된 다른 컴퓨터에서 압축을 해제 한 후, 실행하기만 하면 된다.
