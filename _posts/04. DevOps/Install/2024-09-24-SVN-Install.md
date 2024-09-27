---
title: SVN install & backup
layout: single
categories: DevOps
tags:
  - SVN
  - Install
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true

---
# SVN 활용
## 1) Install
### Dockerfile
```Dockerfile
FROM alpine:latest
RUN apk update && apk add subversion
CMD ["/usr/bin/svnserve","--daemon","--foreground","--root","/var/opt/svn"]
EXPOSE 3690
VOLUME ["/var/opt/svn"]
```
### Docker-compose
```yaml
version: '3'
services:
  svn-[업무]:
    privileged: true
    restart: always
    image: svn:latest
    container_name: svn-[업무]
    ports:
      - "3356:3690"
    environment:
      SET_PERMS: "false"
      TZ: "Asia/Seoul"
      mem_limit: 2G
    volumes:
      - "/data/svn/svn-[업무]/repositories:/var/opt/svn:rw"
```

## 2) Backup
위 Docker-compose 파일을 예시로 생성했을 때 백업 받을 directory는 /data/svn/svn-[업무]/repositories이다.
예시) SVN을 7일 간 backup을 받도록 설정하는 방법
### svn-backup.sh
```shell


```

### svn-backup.cfg
```shell


```

### crontab
```shell

```