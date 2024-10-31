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
# SVN install & backup
## 1) Install
<h3> Dockerfile </h3>
```Dockerfile
FROM alpine:latest
RUN apk update && apk add subversion
CMD ["/usr/bin/svnserve","--daemon","--foreground","--root","/var/opt/svn"]
EXPOSE 3690
VOLUME ["/var/opt/svn"]
```

<h3> Docker-compose </h3>
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
<br>

## 2) Backup
위 Docker-compose 파일을 예시로 생성했을 때 백업 받을 directory는 /data/svn/svn-[업무]/repositories이다.<br>
예시) SVN을 7일 간 backup을 받도록 설정
<h3> /script/svn-backup/bin/svn-backup.sh</h3>
```shell
#!/bin/bash
source /script/svn-backup/cfg/svn-backup.cfg

function fn_backup_success()
{
  echo "$(date) - backup succeeded: $(date +%Y-%m-%d)_$1" >> "$LOG_FILE"
}

function fn_backup_fail()
{
  echo "$(date) - backup failed: $(date +%Y-%m-%d)_$1" >> "$LOG_FILE"
}

function fn_remove_success()
{
    echo "$(date) - Deleted backup file : $(date +%Y-%m-%d -d "7 days ago")_$1" >> "$LOG_FILE"
}

function fn_remove_fail()
{
    echo "$(date) - remove failed: $(date +%Y-%m-%d -d "7 days ago")_$1" >> "$LOG_FILE"
}

DIR_LENGTH=${#SVN_DIR[@]}

function fn_backup(){
    for ((dir=0; dir<DIR_LENGTH; dir++)); do
        VAR_SVN=${SVN_DIR[dir]}
        VAR_BACKUP=${BACKUP_DIR[dir]}
        if tar -cvf $VAR_BACKUP/svn-dev_$(date +%Y-%m-%d).tar $VAR_SVN/; then
            fn_backup_success "$VAR_BACKUP"
        else
            fn_backup_fail "$VAR_BACKUP"
        fi
    done
}

function fn_remove(){
    for ((dir=0; dir<DIR_LENGTH; dir++)); do
        VAR_BACKUP=${BACKUP_DIR[dir]}
        if find $VAR_BACKUP/*.tar -mtime +6 -exec rm {} \; ; then
            fn_remove_success "$VAR_BACKUP"
        else
            fn_remove_fail "$VAR_BACKUP"
        fi
    done
}
echo "[$(date +%Y-%m-%d) log]" >> "$LOG_FILE"
fn_backup
fn_remove

```

<h3> /script/svn-backup/cfg/svn-backup.cfg </h3>
```shell
LOG_FILE="/script/svn-backup/log/backup.log"
SVN_DIR=(
    "/data/svn/svn-[업무]/repositories"
)

BACKUP_DIR=(
    "/data2/backup/svn-[업무]"
)

```

<h3> crontab </h3>
```shell
0 0 * * * /script/svn-backup/bin/svn-backup.sh
```