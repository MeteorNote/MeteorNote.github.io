---
title: Gitlab intro
layout: single
categories: DevOps
tags:
  - Gitlab
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
# Gitlab Intro
## 1) Gitlab 이란?

# Gitlab install & backup
## 1) Gitlab install
### Install

```rb
external_url 'http://[사용 IP : Port]'

git_data_dirs({
	"defualt" => {
		"path" => "/data/gitlab/git-data"
	}
})

nginx['enable'] = true
nginx['client_max_body_size'] = '2G'

```
<br>


### Login



### Project 생성 및 Commit
테스트용 Project와 파일을 Commit한다.


## 2) Gitlab Backup
Gitlab은 동일한 Gitlab 버전으로 백업 및 이관되어야 한다.
<h3> old gitlab 백업(저장소, db 등) </h3>
/var/opt/gitlab/backups 경로에 *_gitlab_backup.tar 형태의 파일로 생성된다.
```shell
gitlab-backup create
```
<br>

<h3> 주요 백업 대상 파일 </h3>
```shell
/etc/gitlab/gitlab.rb
/etc/gitlab/gitlab-secrets.json
```
<br>

<h3> new gitlab 실행 </h3>