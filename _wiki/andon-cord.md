---
layout  : wiki
title   : 안돈 코드 (Andon cord)
summary : 문제가 발생하면 누구나 잡아당길 수 있는 코드
date    : 2020-01-16 21:01:15 +0900
updated : 2021-08-24 23:29:34 +0900
tag     : 
toc     : true
public  : true
parent  : [[software-engineering]]
latex   : false
---
* TOC
{:toc}

![image]( /resource/wiki/andon-cord/130634802-d8148526-8662-492d-9b9a-f5b7d4ddd858.png )
[^image-ref]

## From: 데브옵스 핸드북

> 도요타 생산 공장 내의 모든 작업장에는 모든 근로자와 관리자가 문제 발생 시 잡아당기는 코드가 있다. 예를 들어, 부품에 결함이 있거나 필요한 부품을 사용할 수 없을 때 그리고 작업 시간이 서류상 예정된 시간보다 오래 걸릴 때도 코드를 잡아당긴다.
<br/><br/>
안돈 코드가 당겨지면 팀장이 알림을 받고 곧바로 문제 해결에 착수한다. 특정 시간(예를 들어, 55초) 내에 문제가 해결되지 않으면, 생산 라인이 중단되고 대응책이 마련될 때까지 전체 조직이 동원되기도 한다.[^handbook-73]

### 안돈 코드가 당겨지면 스워밍으로 문제를 해결한다.

* 안돈 코드가 당겨지면
    * 문제를 해결할 때까지 신규 작업의 도입을 금지한다.
    * 문제를 해결할 때까지 스워밍(swarming)한다.

모든(가능한 한 많은) 사람이 한 문제를 해결하기 위해 벌 떼처럼 모여드는 것을 스워밍(swarming) 이라 부른다.

문제를 방치한 상태로 계속 일하지 않는 것이 중요하다.

* 문제를 방치한 상태로 계속 일하면,
    * 문제가 여기저기 퍼져나갈 수 있다.
    * 복구 비용과 복구에 필요한 노력이 기하급수적으로 증가할 수 있다.
    * 기술 부채가 누적된다.
* 스워밍을 통해 문제를 즉시 고치면,
    * 많은 사람이 문제에 대해 학습하고 경험을 쌓게 된다.
    * 문제가 더 악화되기 전에 해결하게 된다.

스워밍을 통해 문제를 즉시 고칠 수 있도록 한다.

만약 꾸준한 개선 노력으로 안돈 코드의 당김 횟수가 감소하면, 관리자는 허용 오차를 줄이도록 한다.

* 허용 오차를 줄이게 되면,
    * 아주 약한 실패 신호도 감지하게 된다.
    * 안돈 코드 당김 횟수가 다시 증가하며 품질도 같이 오르게 된다.
    * 가치 흐름 내의 모든 사람(시스템 장애를 일으킨 사람 포함)에게 빠른 피드백을 제공한다.
    * 문제를 신속하게 진단하고 격리할 수 있다.



## 참고문헌

* 데브옵스 핸드북 / 진 킴, 제즈 험블, 패트릭 드부아, 존 윌리스 저/김영기 역 외 1명 정보 더 보기/감추기 / 에이콘출판사 / 2018년 07월 06일 / 원제: The DevOps Handbook: How to Create World-Class Agility, Reliability, and Security in Technology Organizations

## 주석

[^image-ref]: 이미지 출처는 <https://www.learningpersonalized.com/empowering-others-to-pull-the-andon-cord/ >
[^handbook-73]: 데브옵스 핸드북. 73쪽.

