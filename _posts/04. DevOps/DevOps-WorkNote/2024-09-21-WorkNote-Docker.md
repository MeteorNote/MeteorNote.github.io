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
## 1) install
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

## 2) docker-compose install
docker-compose 버전 1.27.4 설치
```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

sudo docker-compose -v

```
<br>

## 3) 이미지 <--> tar
```shell
sudo docker save -o [image_tag].tar image:tag
sudo docker load -i [image_tag].tar
```
<br>

## 4) docker root directory - daemon.json
```json
vim /etc/docker/daemon.json

{
	"data-root": "/data/docker/docker"
}
```
<br>

## 5) docker root directory - daemon docker.service
```shell
# Edit the docker.service file
sudo vim /usr/lib/systemd/system/docker.service

# Find the line starting with ExecStart and update it:
ExecStart=/usr/bin/dockerd --data-root /data/docker/docker
```
<br>

## 6) docker 프로세스 종료
```shell
docker stop [container]
docker rm [container]
```
<br>

## 7) docker-compose 파일 예시
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

## 8) docker process -> images
```shell
docker commit <CONTAINER ID> [이미지이름:tag]
```