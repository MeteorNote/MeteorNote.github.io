---
title: Gitlab install & backup
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
# Gitlab install & backup
## 1) Gitlab install

```rb
external_url 'http://172.29.224.202:10480'

git_data_dirs({
	"defualt" => {
		"path" => "/data/gitlab/git-data"
	}
})

nginx['enable'] = true
nginx['client_max_body_size'] = '2G'

```
<br>
## 2) Gitlab Backup
### old gitlab 백업(저장소, db 등)
- /var/opt/gitlab/backups 경로에 *_gitlab_backup.tar 형태의 파일로 생성된다.
```shell
gitlab-backup create
```
<br>
### 주요 백업 대상 파일
```shell
/etc/gitlab/gitlab.rb
/etc/gitlab/gitlab-secrets.json
```
<br>
### new gitlab 실행