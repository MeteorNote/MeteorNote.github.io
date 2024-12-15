---
title: Kubernetes 환경 자원 이관 영향도 파악
layout: single
categories: DevOps
tags:
  - Jenkins
  - Kubernetes
  - Research
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# Kubernetes 환경 자원 이관
쿠버네티스 환경에서 운영되고 있는 자원을 타 계정으로 이관한다는 컨셉으로 영향도 파악을 진행했다.

## 1) 자원 이관 대상 리스트
- S3 : 빌드 설정 파일 및 유저 데이터를 저장
- Container Registry : private docker 저장소로 사용
- Jenkins : 쿠버네티스 deployment 배포를 위한 CI/CD
- Gitlab : 개발자 버전 관리 및 소스코드 저장
- Kubernetes : Micro-service Architecture 환경

## 2) 각 자원 영향도 파악
<h3> S3 </h3>
빌드 설정 파일과 유저 데이터가 관리되므로 s3 browser로 전체 이관해야한다.

<h3> Container Registry </h3>
Private Docker image 저장소로 활용되기 때문에 최소 기본 base image 관련 데이터를 같이 이관 시키는 것이 좋다.

<h3> Jenkins </h3>
<div class="notice--info">
<h3> Jenkins 이관 시 체크해야하는 파일</h3>
<ul>
    <li> /etc/sysconfig/jenkins => 포트 및 홈 디렉토리 변경 </li>
    <li> /usr/lib/systemd/system/jenkins.service 혹은 기존 daemon 파일 확인 => 포트 및 홈 디렉토리 변경 </li>
    <li> /etc/logrotate.d/jenkins </li>
    <li> /etc/passwd => 홈디렉토리 변경 </li>
</ul>
</div>

Jenkins는 이관 시 동일한 버전으로 이관해야 Plugin dependency 영향도가 없어지며 jenkins_home 디렉토리 자체를 데이터를 이관 시키는 것이 좋다. Jenkins 서버 내에는 Docker를 설치해야하며 Docker 설치 후 Docker 그룹 내 Jenkins 사용자를 포함시켜야 한다. <br>
Jenkins 내부에 설정되어 있는 S3 및 Docker 인증 Credential ID, Kubernetes URL을 변경해줘야 한다. <br>
Pipeline 내 S3, Gitlab, Kubernetes DNS, Container Registry DNS, Credential과 같은 변경 내역은 모두 확인해줘야 한다.

<h3> Gitlab </h3>
Gitlab Backup 방식으로 데이터 이관을 해야하고 AS-IS 서버 TO-BE 서버 간 gitlab 버전 차이가 동일해야한다.

<h3> Kubernetes </h3>
kubectl 서버와의 인증 초기화, IAM 권한, kubectl 설치 등 기본적인 환경설정이 우선적으로 진행되어야 한다. <br>
Container Registry가 변경되기 때문에 k8s에서 Docker image pull을 하기 위한 신규 regcred 생성을 해줘야 한다.



## 3) 이관 전 정리해야할 문서
<div class="notice--info">
<h3> Check List </h3>
<ul>
    <li> As-is Jenkins Pipeline </li>
    <li> Dockerfile </li>
    <li> kubernetes yaml 파일 </li>
    <li> 각 namespace의 Pod, Service, Secret 등 </li>
    <li> Jenkins workspace, 배포파일 일치여부 </li>
</ul>
</div>
