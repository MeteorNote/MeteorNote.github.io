---
title: WEB/WAS Troubleshooting
layout: single
categories: DevOps
tags:
  - WEB
  - WAS
  - Troubleshooting
toc: true
toc_sticky: true
toc_label: 목차
author_profile: false
sidebar: 
    nav: "counts"
search: true
use_math: true
---
# WEB/WAS Troubleshooting
해당 글은 컨테이너 환경이 아닌 일반 VM 운영을 기준으로 작성되었습니다. 개발 단 소스코드의 의도와 다르게 서버 설정에 의해서 다른 결과가 도출될 수 있습니다. 이는 의도치 않은 에러 발생을 야기할 수 있고 기본적으로 개발과 스테이징 환경에서 충분한 테스트를 거쳐야 하지만 운영 환경에서 갑작스러운 에러를 마주할 경우 대처하기 어렵습니다. 순수 소스코드에서 발생되는 에러는 이전 버전으로 롤백하면 되지만 서버 설정은 버전관리보다 설정 값 하나하나를 이해하는 것이 중요합니다.

## 1) Apache Web Troubleshooting
<h3> Case 1 </h3>


## 2) Wildfly WAS Troubleshooting

<h3> Case 1 </h3>
<div class="notice--info">
<h3> Wildfly engine 라이브러리 확인 </h3>
wildfly 사용 시 기본적으로 driver가 존재해야 소스코드 및 config에 맞게 기동이 된다.
</div>

<h3> Case 2 </h3>
<div class="notice--danger">
<h3> 재기동 시 주의사항 </h3>
WAS의 재기동도 WEB과 마찬가지로 정해진 유저로만 기동하게 된다. 하지만 외부 서버에서 스크립트를 돌리거나 재기동을 진행할 때 항상 재기동을 하는 유저의 .bashrc 혹은 .bash_profile의 export 설정값을 확인해야한다. <br>
export에 적용된 변수는 wildfly 실행 시 소스코드에도 영향을 줄 수 있으며 해당 내용을 자세히 확인하기 위해선 wildfly를 debug level로 설정해야 대처할 수 있다.
</div>

