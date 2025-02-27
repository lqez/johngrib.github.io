---
layout  : wiki
title   : DDD 관련 인용문 모음
summary : 
date    : 2020-07-12 17:27:28 +0900
updated : 2020-07-12 17:38:37 +0900
tag     : 
toc     : true
public  : true
parent  : [[software-engineering]]
latex   : false
---
* TOC
{:toc}

## From: 마이크로서비스 패턴

> DDD는 도메인을 구성하는 각 하위 도메인(애플리케이션의 문제 공간(problem space)을 가리키는 DDD 용어)마다 도메인 모델을 따로 정의합니다.
하위 도메인은 비즈니스 능력과 같은 방법(비즈니스를 분석하고 상이한 전문 영역을 식별)으로 식별하므로 십중팔구 비즈니스 능력과 유사한 하위 도메인이 도출됩니다.
가령 FTGO의 하위 도메인은 주문 접수, 주문 관리, 주방 관리, 배달, 재무 등이 있습니다.
좀 전에 식별한 비즈니스 능력과 비슷하죠?
>
> 도메인 모델의 범위를 DDD 용어로는 경계 컨텍스트(bounded context, 경계가 분명한 컨텍스트)라고 합니다.
경계 컨텍스트는 도메인 모델을 구현한 코드 아티팩트(code artifact)를 포함하며,
마이크로 서비스 아키텍처에 DDD를 적용하면 각 서비스(들)가 경계 컨텍스트가 됩니다.
그림 2-9는 각각 자체 도메인 모델을 가진 서비스에 하위 도메인을 매핑한 것입니다.
>
> ![]( /resource/wiki/ddd-quotes/ric-2-9.jpg )
>
> DDD와 마이크로서비스 아키텍처는 거의 찰떡궁합입니다.
DDD의 하위 도메인, 경계 컨텍스트 개념은 마이크로서비스 아키텍처의 서비스와 잘 맞고, 마이크로서비스 아키텍처의 서비스 자율팀 개념은 도메인 모델을 개별 팀이 소유/개발한다는 DDD 사고방식과 잘 어울립니다.
자체 도메인 모델을 가진 하위 도메인이라는 개념 덕분에 만능 클래스를 제거하고 서비스로 분해하기가 더 수월해집니다.[^ric-2-2-3]


## 참고문헌

- [RIC] 마이크로서비스 패턴 / 크리스 리처드슨 저/이일웅 역 / 길벗 / 초판발행 2020년 01월 30일

## 주석

[^ric-2-2-3]: [RIC] 2.2.3장.

