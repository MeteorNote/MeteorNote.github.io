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

```rb
external_url 'http://172.29.224.202:10480'

git_data_dirs({
	"defualt" => {
		"path" => "/data2/gitlab/git-data"
	}
})

nginx['enable'] = true
nginx['client_max_body_size'] = '2G'

```