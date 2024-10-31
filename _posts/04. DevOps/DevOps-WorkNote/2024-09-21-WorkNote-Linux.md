---
title: 자주 활용되는 Linux 명령어 Note
layout: single
categories: DevOps
tags:
  - WorkNote
  - Linux
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# Linux Command Note
<div class="notice--success">
  실무에서 자주 사용하는 명령어 정리
</div>

## 1) tar
```shell
tar czvf abc.tar abc
tar czvf abc.tar.gz --exclude "제외할파일" abc
```
<br>

## 2) link
```shell
ln -s /nas/path deploy
```
<br>

## 3) find
파일, 디렉터리명 검색
```shell
find . -iname "test"
```
파일 내 단어 검색
```shell
find . -iname "*" | xargs grep -i --color "찾고싶은키워드"
```
특정 명칭의 파일명 검색
```shell
find . -type f -iname "*D*"
```
<br>

## 4) lsof
특정 포트의 프로세스 종류 및 현황 확인
```shell
lsof -i :8080
```
```shell
# 출력 예시
COMMAND    PID USER   FD TYPE DEVICE SIZE/OFF NOTE NAME
java   1234567  was 486u IPv4 123456     0t0  TCP  *:8080(LISTEN)
java   1234567  was 776u IPv4 123457     0t0  TCP  10.10.10.10:8080->10.10.20.10:58888 (ESTABLISHED)
```
<br>

## 5) awk
```shell

```
<br>

## 6) stty 화면조정
SSH 툴 사용 시 리눅스 vi 창이 깨지는 경우에 사용
```shell
stty -a # 설정확인
stty rows <설정값> # row값 변경
```
<br>

## 7) rsync
```shell
rsync -avzh -e 'ssh -p 22 -o StrictHostKeyChecking=no' /data/old_data/ user@<new_server_ip>:/data/new_data/
```
<br>

## 8) scp
```shell

```
<br>

## 9) telnet 사용 불가 시 통신 확인방법
```shell
echo > /dev/tcp/<접속할ip>/<접속할port>
```