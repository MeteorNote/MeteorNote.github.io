---
title: Jenkins Intro
layout: single
categories: DevOps
tags:
  - Jenkins
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
# Jenkins 소개
## 1) Jenkins 란?
Jenkins는 오픈 소스 자동화 CI/CD(Continuous Integration/Continuous Delivery) 파이프라인을 구축하고 관리하는 데 사용된다. CI/CD는 코드 변경을 자동으로 빌드, 테스트, 배포하는 프로세스를 의미하며 빠르고 안정적인 소프트웨어 배포가 가능하다.

<h3> Jenkins 기능 </h3>
- 지속적 통합(Continuous Integration): 개발자가 소스 코드를 변경할 때마다 Jenkins가 자동으로 빌드 및 테스트를 실행하여 코드의 품질을 유지한다.
- 지속적 배포(Continuous Delivery): 빌드 및 테스트 후 자동으로 애플리케이션을 배포하는 작업을 지원한다.
- 플러그인 확장성: 다양한 플러그인을 통해 Jenkins는 Git, SVN, Docker, Maven, Kubernetes 등과 연동하여 다양한 워크플로우를 지원한다.

## 2) Jenkins 구조
### Jenkins Login/User


### Jenkins Item
- Freestyle project

- Maven project

- Pipeline


- External Job


- Multi-configuration project

- Folder


- Multibranch Pipeline


- Organiztion Folder

- Ivy project


### Jenkins 관리
- 시스템 설정


- 플러그인 관리


- Security



- 시스템 정보



- ThinBackup


# Jenkins install & backup
## 1) Install
```shell

```

<h3> /usr/lib/systemd/system/jenkins.service </h3>
```shell
[Unit]
Description=Jenkins Continuous Integration Server
Requires=network.target
After=network.target

[Service]
Type=notify
NotifyAccess=main
ExecStart=/usr/bin/jenkins
Restart=on-failure
SuccessExitStatus=143
User=jenkins
Group=jenkins

Environment="JENKINS_HOME=/app/jenkins"
WorkingDirectory=/app/jenkins
Environment="JENKINS_WEBROOT=%C/jenkins/war"
Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.12.0.7-0.el7_9.x86_64"
Environment="JAVA_OPTS=-Djava.awt.headless=true"
Environment="JENKINS_PORT=8080"

[Install]
WantedBy=multi-user.target
```

<h3> /etc/sysconfig/jenkins </h3>
```shell
JENKINS_HOME="/app/jenkins"
JENKINS_JAVA_CMD=""
JENKINS_USER="jenkins"
JENKINS_JAVA_OPTIONS="-Djava.awt.headless=true"
JENKINS_PORT="8080"
JENKINS_LISTEN_ADDRESS=""
JENKINS_HTTPS_PORT=""
JENKINS_HTTPS_KEYSTORE=""
JENKINS_HTTPS_KEYSTORE_PASSWORD=""
JENKINS_HTTPS_LISTEN_ADDRESS=""
JENKINS_HTTP2_PORT=""
JENKINS_HTTP2_LISTEN_ADDRESS=""
JENKINS_DEBUG_LEVEL="5"
JENKINS_ENABLE_ACCESS_LOG="no"
JENKINS_HANDLER_MAX="100"
JENKINS_HANDLER_IDLE="20"
JENKINS_EXTRA_LIB_FOLDER=""
JENKINS_ARGS=""
```

<h3> /etc/logrotate.d/jenkins </h3>
```shell
/var/log/jenkins/jenkins.log /var/log/jenkins/access_log {
  compress
  dateext
  maxage 365
  rotate 99
  size=+4096k
  notifempty
  missingok
  create 644
  copytruncate
}

```

## 2) Backup
### thinBackup


### 단순 전체 백업
