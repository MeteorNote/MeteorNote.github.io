---
title: Nexus Intro
layout: single
categories: DevOps
tags:
  - Nexus
  - Intro
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# Nexus Intro
## 1) Nexus 란?
Nexus는 소프트웨어 아티팩트를 저장하고 관리하는 리포지토리 관리 도구이다. Nexus는 Sonatype Nexus Repository Manager라는 이름으로 제공되며 소프트웨어 빌드 과정에서 Maven, Gradle, npm, Docker 등의 빌드 도구와 연동된다. 무료 버전인 Nexus OSS와 추가적인 기능을 제공하는 Nexus Pro 버전이 있다.

<h3> Nexus 기능 </h3>

- 아티팩트 저장소 : Nexus는 아티팩트를 중앙에서 관리하고 팀이 공유할 수 있도록 하며 소프트웨어 개발 과정에서 일관성 있고 안정적인 버전 관리가 가능합니다.
- 프록시 리포지토리 : 외부 저장소를 프록시로 설정하여 외부 패키지를 로컬에서 캐싱하고 관리할 수 있다. 외부 저장소에 대한 의존성을 줄이고 빌드 속도를 향상시키는데 도움이 된다.
- 호스팅 리포지토리 : 직접 생성한 아티팩트를 저장하고 배포할 수 있는 호스팅 리포지토리를 제공한다.
- 복합 리포지토리 : 여러 저장소를 하나의 리포지토리처럼 묶어주는 기능을 제공해 여러 소스에서 아티팩트를 통합적으로 관리가 가능하다.
- 권한 관리 : 접근 권한 설정을 통해 특정 사용자 또는 그룹이 특정 아티팩트나 저장소에 접근할 수 있도록 관리할 수 있다.
- 자동화 통합 : CI/CD 파이프라인과 쉽게 통합되어 빌드 후 자동으로 아티팩트를 Nexus로 배포하는 작업을 자동화할 수 있다.


## 2) Nexus 구조




## 3) Nexus 라이브러리 업로드