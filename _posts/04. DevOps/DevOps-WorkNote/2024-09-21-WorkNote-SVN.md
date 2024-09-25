---
title: 자주 활용되는 SVN Note
layout: single
categories: DevOps
tags:
  - WorkNote
  - SVN
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
## 1) install
### Docker로 SVN 설치
```Dockerfile
FROM alpine:latest
RUN apk update && apk add subversion
CMD ["/usr/bin/svnserve","--daemon","--foreground","--root","/var/opt/svn"]
EXPOSE 3690
VOLUME ["/var/opt/svn"]
```
### Docker-compose
```yaml

```