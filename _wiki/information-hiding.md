---
layout  : wiki
title   : 정보 은닉 (Information Hiding)
summary : 
date    : 2021-04-30 23:50:07 +0900
updated : 2021-05-01 21:00:32 +0900
tag     : proverb oop
toc     : true
public  : true
parent  : [[jargon]]
latex   : false
---
* TOC
{:toc}

## From: 마이크로서비스 도입 이렇게 한다

>
결합도에 대한 논의와 관련해 여러 차례 반복해서 나오는 개념은 정보 은닉(Information Hiding)이라는 기법이다.
1971년 데이비드 파나스(David Parnas)가 처음 개괄한 이 개념은 모듈 경계를 정의하는 방법에 대한 연구에서 비롯되었다.
>
정보 은닉의 핵심 개념은 자주 변경되는 코드부를 정적인 코드부와 분리하는 것이다.
우리는 모듈 경계가 안정되기를 원하며 더 자주 변경될 것으로 예상되는 모듈 구현 부분을 숨겨야 한다.
즉 모듈 호환성이 유지되는 동안에는 내부 변경을 안전하게 수행할 수 있다.
>
나는 모듈 (또는 마이크로서비스) 경계에서 가능한 한 적게 외부로 노출하는 접근 방식을 선호하는 편이다.
일단 뭔가 모듈 인터페이스의 일부가 되면, 이를 철회하기란 어렵다.
그러나 만일 지금 숨기면 언제든지 나중에 공유하기로 결정할 수 있다.
>
객체 지향 소프트웨어의 개념으로서 캡슐화(encapsulation)는 정보 은닉과 관련이 있지만 여러분이 받아들이는 정의에 따라 둘은 정확하게 동일하지 않을 수도 있다.
객체 지향 프로그래밍에서 캡슐화는 하나 이상의 항목을 컨테이너로 묶는 것을 의미하게 되었다.
필드와 해당 필드에서 작동하는 메소드를 모두 포함하는 클래스를 생각해보라.
그런 다음 클래스 정의에서 가시성을 사용해 구현의 일부를 숨길 수 있다.
>
정보 은닉에 대한 역사를 깊숙이 파보고 싶다면, 파나스가 저술한 논문 "정보 은닉의 비밀스러운 역사 기록"을 추천한다.
>
-- 마이크로서비스 도입 이렇게 한다. 1장.

## 함께 읽기

- [[OOP-to-me-Alan-Kay]]{앨런 케이의 심플한 OOP 정의}
- [[constantine-s-law]]{콘스탄틴의 법칙}
- [[oop-quotes]]{객체지향 인용문 모음}

## 참고문헌

- 마이크로서비스 도입 이렇게 한다 / 샘 뉴먼 저/박재호 역 / 책만 / 2021년 01월 20일 / 원서 : Monolith to Microservices: Evolutionary Patterns to Transform Your Monolith

