---
title: 자주 활용되는 Docker 활용
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
### 자주 활용되는 Docker 명령어와 활용
#### 1) install
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

#### 2) docker-compose install
```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

sudo docker-compose -v

```

#### 3) 이미지 <--> tar
```shell
sudo docker save -o [image_tag].tar image:tag
sudo docker load -i [image_tag].tar
```

#### 4) docker root directory - daemon.json
```shell
vim /etc/docker/daemon.json

{
	"data-root": "/data/docker/docker"
}
```

#### 5) docker root directory - daemon docker.service
```shell



```

#### 6) docker 프로세스 종료
```shell
docker stop [container]
docker rm [container]
```


#### 7) docker-compose 파일 예시
```shell



```