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


<head>
  <style>
    table.dataframe {
      white-space: normal;
      width: 100%;
      height: 240px;
      display: block;
      overflow: auto;
      font-family: Arial, sans-serif;
      font-size: 0.9rem;
      line-height: 20px;
      text-align: center;
      border: 0px !important;
    }

    table.dataframe th {
      text-align: center;
      font-weight: bold;
      padding: 8px;
    }

    table.dataframe td {
      text-align: center;
      padding: 8px;
    }

    table.dataframe tr:hover {
      background: #b8d1f3; 
    }

    .output_prompt {
      overflow: auto;
      font-size: 0.9rem;
      line-height: 1.45;
      border-radius: 0.3rem;
      -webkit-overflow-scrolling: touch;
      padding: 0.8rem;
      margin-top: 0;
      margin-bottom: 15px;
      font: 1rem 'Cascadia Code', Consolas, 'Courier New', monospace;
      color: $code-text-color;
      border: solid 1px $border-color;
      border-radius: 0.3rem;
      word-break: normal;
      white-space: pre;
    }

  .dataframe tbody tr th:only-of-type {
      vertical-align: middle;
  }

  .dataframe tbody tr th {
      vertical-align: top;
  }

  .dataframe thead th {
      text-align: center !important;
      padding: 8px;
  }

  .page__content p {
      margin: 0 0 0px !important;
  }

  .page__content p > strong {
    font-size: 0.8rem !important;
  }

  </style>
</head>




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
```python
import pandas
x = 1

```