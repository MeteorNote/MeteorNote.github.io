---
title: Jenkins install & backup
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

Environment="JENKINS_HOME=/data/jenkins"
WorkingDirectory=/data/jenkins
Environment="JENKINS_WEBROOT=%C/jenkins/war"
Environment="JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.12.0.7-0.el7_9.x86_64"
Environment="JAVA_OPTS=-Djava.awt.headless=true"
Environment="JENKINS_PORT=8080"

[Install]
WantedBy=multi-user.target
```

<h3> /etc/sysconfig/jenkins </h3>
```shell
JENKINS_HOME="/data/jenkins"
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