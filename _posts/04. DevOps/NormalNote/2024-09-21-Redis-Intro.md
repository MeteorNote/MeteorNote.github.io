---
title: Redis Intro
layout: single
categories: DevOps
tags:
  - Intro
  - Redis
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# Redis Intro
Redis는 Remote Dictionary Server의 약자로, 오픈 소스 기반의 인메모리 데이터 구조 저장소이다. <br>
데이터를 메모리에 저장하고 관리하며, 매우 빠른 성능을 제공하며 주로 캐시, 세션 저장소, 큐 시스템, 실시간 데이터 분석 등에서 사용된다.
<div class="notice--success">
<h4> Redis 설치 방법 </h4>
<ul>
    <li> 단일 서버(Standalone) </li>
    <li> Redis 복제(Replication) </li>
    <li> Redis Sentinel (고가용성 제공) </li>
    <li> Redis 클러스터(Redis Cluster) </li>
</ul>
</div>

## 1) 단일 서버(Standalone)
단일 서버 설치는 하나의 Redis 인스턴스만을 실행하고 해당 서버가 모든 요청을 처리한다.<br>
install link
<h3> 장점 </h3>
- 설정이 매우 간단하다.

<h3> 단점 </h3>
- 단일 장애점(SPOF): 단일 서버에만 의존하기 때문에 서버가 다운되면 전체 시스템이 중단될 수 있다.

<br>

## 2) Redis 복제(Replication)
복제를 통해 하나의 마스터 서버와 다수의 슬레이브 서버를 설정할 수 있다. 슬레이브 서버는 마스터 서버의 데이터를 복제하며 읽기 요청은 슬레이브가 처리할 수 있어 로드 밸런싱을 구현할 수 있다.
<h3> 장점 </h3>
- 읽기 성능 향상: 읽기 작업을 슬레이브 서버로 분산할 수 있어 성능을 높일 수 있다.
- 데이터 백업: 슬레이브 서버가 마스터 서버의 데이터를 복제하므로 마스터 서버 장애 시 슬레이브가 데이터를 보존하고 복구할 수 있다.

<h3> 단점 </h3>
- 마스터 서버가 다운되면 데이터 쓰기 작업이 불가능

<br>

## 3) Redis Sentinel (고가용성 제공)
Redis Sentinel은 Redis의 고가용성(HA)을 제공하는 도구이다. 마스터-슬레이브 구조에서 마스터 서버가 다운될 경우 자동으로 새로운 마스터 서버를 선택해 클러스터를 복구한다.
<h3> 특징 </h3>
- 자동 장애 조치: Sentinel은 마스터 서버가 장애를 일으켰을 때 슬레이브 서버 중 하나를 새로운 마스터로 승격시킴
- 모니터링: Sentinel은 마스터와 슬레이브를 지속적으로 모니터링하여 장애를 감지한다.
- 알림: 문제가 발생하면 관리자가 지정한 방식으로 알림을 받을 수 있다.

<br>

## 4) Redis 클러스터(Redis Cluster)
Redis 클러스터는 분산 환경에서 데이터의 자동 분산과 샤딩을 지원하는 설치 방식입니다. 여러 노드에 데이터를 분산하여 저장하고 노드 간 데이터 복제를 통해 고가용성과 확장성을 제공한다.

<h3> 특징 </h3>
- 자동 샤딩: 데이터를 여러 노드에 분산 저장하며, 데이터의 일부가 한 노드에만 저장되도록 해준다.
- 고가용성: 노드 중 일부가 장애를 일으켜도 나머지 노드가 정상적으로 동작한다.
- 확장성: 새로운 노드를 추가하거나 제거하여 클러스터의 크기를 유연하게 조정할 수 있다.
