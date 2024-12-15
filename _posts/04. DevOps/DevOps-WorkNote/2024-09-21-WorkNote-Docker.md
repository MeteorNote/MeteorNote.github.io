---
title: 자주 활용되는 Docker Note
layout: single
categories: DevOps
tags:
  - WorkNote
  - Docker
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---

# Docker Note
## 1) Docker 란?
Docker는 애플리케이션을 컨테이너로 패키징하고 배포할 수 있게 해주는 오픈 소스 플랫폼이다. 호스트 운영체제 위에서 애플리케이션이 독립적으로 실행될 수 있는 환경을 제공하여 정확하고 빠르게 배포 및 확장이 가능하다.

<h3> 특징 </h3>
- 컨테이너화: 독립적인 실행 환경을 제공하여 시스템 간의 차이로 인해 발생할 수 있는 문제를 최소화한다.
- 이미지 기반: Docker 이미지는 애플리케이션을 실행하기 위한 모든 것을 포함하고 있어 동일한 환경을 보장한다.
- 이식성: Docker 컨테이너는 로컬 개발 환경, 클라우드, 서버 등 여러 곳에서 실행할 수 있어 이식성이 좋다.
- 효율성: VM에 비해 더 적은 리소스로 애플리케이션을 격리하고 실행할 수 있다.

## 2) install
아래 링크를 참고하였습니다.
[Docker 공식 설치](https://docs.docker.com/engine/install/centos/)
최신 docker 버전 설치
```shell
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine


sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo


sudo yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl start docker

```
<br>

## 3) docker-compose install
docker-compose 버전 1.27.4 설치
```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

sudo docker-compose -v

```
<br>

## 4) 이미지 <--> tar
```shell
sudo docker save -o [image_tag].tar image:tag
sudo docker load -i [image_tag].tar
```
<br>

## 5) docker root directory - daemon.json
```json
vim /etc/docker/daemon.json

{
	"data-root": "/data/docker/docker"
}
```
<br>

## 6) docker root directory - daemon docker.service
```shell
# Edit the docker.service file
sudo vim /usr/lib/systemd/system/docker.service

# Find the line starting with ExecStart and update it:
ExecStart=/usr/bin/dockerd --data-root /data/docker/docker
```
<br>

## 7) docker 프로세스 종료
```shell
docker stop [container]
docker rm [container]
```
<br>

## 8) docker-compose 파일 예시
SVN 설치 시 예시
```yaml
version: '3'
services:
  svn:
    privileged: true
    restart: always
    image: svn:latest
    container_name: svn
    ports:
      - "3356:3690"
    environment:
      SET_PERMS: "false"
      TZ: "Asia/Seoul"
      mem_limit: 2G
    volumes:
      - "/data/svn/svn-[업무]/repositories:/var/opt/svn:rw"
```
<br>

## 9) docker process -> images
```shell
docker commit <CONTAINER ID> [이미지이름:tag]
```