---
layout  : wiki
title   : 디미터 법칙 (The Law of Demeter)
summary : 객체는 그것이 내부적으로 보유하고 있거나 메시지를 통해 확보한 정보만 가지고 의사 결정을 내려야 한다
date    : 2020-03-22 12:13:49 +0900
updated : 2020-07-19 13:38:01 +0900
tag     : law oop
toc     : true
public  : true
parent  : [[jargon]]
latex   : false
---
* TOC
{:toc}

"Don't Talk to Strangers" 라고도 한다.

## 어원

### From: UML과 패턴의 적용

> 칼 리베헤(Karl Lieberherr)와 그의 동료들은 디미터(Demeter) 프로젝트 산하에서 훌륭한 객체 설계 원칙에 대해 연구하였다.
그들은 객체 구조의 변화와 불안정이 자주 발생되는 것을 보았고 객체 연결에 관한 정보를 지닌 코드는 불안정하다는 사실을 접하면서 디미터 법칙(Don't Talk to Strangers)을 만들었다.[^larman-462]

### From: 오브젝트

> 디미터 법칙은 "Object-Oriented Programming: An Objective Sense of Style"에서 처음으로 소개된 개념으로 이 글의 저자들은 디미터라는 이름의 프로젝트를 진행하던 도중 객체들의 협력 경로를 제한하면 결합도를 효과적으로 낮출 수 있다는 사실을 발견했다.[^cho-184]

### From: 실용주의 프로그래머

> 디미터(Demeter)는 그리스 신화의 농업, 결혼, 사회 질서의 여신이다.
디미터라는 프로젝트에서 이 법칙을 발견했다고 해서 그렇게 이름 붙였다.
그 프로젝트는 소프트웨어를 '성장'시키는 방법을 사용한다(디미터가 농업의 여신이라는 점을 기억하라).[^andrew-227]

## 의미
### From: UML과 패턴의 적용

> **구조 은닉 설계(structure-hiding design)**  
이 책의 초판에서, 9개의 GRASP 패턴 중 하나로서 Don't Talk to Strangers(낯선 사람에게 말하지 마라)패턴 또는 **디미터 법칙**으로 불리는 중요한 객체 설계 원칙을 다루었다.
간단하게 말하면, 긴 객체 구조의 경로를 따라 멀리 떨어져 있는 간접적인(낯선) 객체에 메시지를 보내는(또는 이야기하는) 설계는 피하라는 것이다.
이러한 설계는 일반적으로 불안정한 지점으로, 객체 구조의 변화에 부서지기 쉽다.
>
> (중략)
>
> Don't Talk to Strangers 패턴은 메소드 내에서 어떤 객체에 메시지를 보내야 하는가에 대한 제약을 가한다.
메소드 안에서 다음의 객체들에게만 메시지를 보내야 한다.
1. this(또는 self) 객체
2. 메소드의 매개변수
3. this의 속성
4. this의 속성인 컬렉션의 요소
5. 메소드 내에서 생성된 객체[^larman-461]

### From: 소트웍스 앤솔로지

>
디미터의 법칙("친구하고만 대화하라")이 좋은 출발점이긴 하지만, 이런 식으로 생각하자.
자기 소유의 장난감, 자기가 만든 장난감, 그리고 누군가 자기에게 준 장난감하고만 놀 수 있다.
하지만 절대 장난감의 장난감과 놀면 안 된다.[^thoughtworks-90]

### From: 테스트 주도 개발로 배우는 객체 지향 설계와 실천

> 서로 메시지를 전달하는 객체가 있다면 객체는 서로 무슨 이야기를 할까?
경험상 객체를 호출할 땐 이웃 객체가 하는 역할 측면에서 해당 객체가 무엇을 원하는지 기술하고,
호출된 객체가 그러한 바를 어떻게 실현할지 결정하게 해야 한다.
이것은 흔히 '묻지 말고 말하라' 스타일이나 좀 더 형식적으로 말하면 디미터의 법칙(Law of Demeter)으로 알려져 있다.
객체는 그것이 내부적으로 보유하고 있거나 메시지를 통해 확보한 정보만 가지고 의사 결정을 내려야 한다.
객체는 다른 객체를 탐색해 뭔가를 일어나게 해서는 안 된다.[^steve-19]

**객체는 그것이 내부적으로 보유하고 있거나 메시지를 통해 확보한 정보만 가지고 의사 결정을 내려야 한다.**

### From: Clean Code

> 디미터 법칙은 잘 알려진 휴리스틱으로, 모듈은 자신이 조작하는 객체의 속사정을 몰라야 한다는 법칙이다.
앞 절에서 봤듯이, 객체는 자료를 숨기고 함수를 공개한다. 즉, 객체는 조회 함수로 내부 구조를 공개하면 안 된다는 의미다.
그러면 내부 구조를 (숨기지 않고)노출하는 셈이니까.  
좀 더 정확히 표현하자면, 디미터 법칙은 "클래스 C의 메서드 f는 다음과 같은 객체의 메서드만 호출해야 한다"고 주장한다.
- 클래스 C
- f가 생성한 객체
- f 인수로 넘어온 객체
- C 인스턴스 변수에 저장된 객체

> 하지만 위 객체에서 허용된 메서드가 반환하는 객체의 메서드는 호출하면 안 된다.
다시 말해, 낯선 사람은 경계하고 친구랑만 놀라는 의미다.[^bob-123]

- 짧은 설명

> 일반적으로 한 모듈은 주변 모듈을 모를수록 좋다.
좀 더 구체적으로, A가 B를 사용하고 B가 C를 사용한다 하더라도 A가 C를 알아야 할 필요는 없다는 뜻이다.[^bob-395]

### From: 오브젝트

- 협력 경로를 제한하라.

> 이처럼 협력하는 객체의 내부 구조에 대한 결합으로 인해 발생하는 설계 문제를 해결하기 위해 제안된 원칙이 바로 디미터 법칙(Law of Demeter)이다.
디미터 법칙을 간단하게 요약하면 객체의 내부 구조에 강하게 결합되지 않도록 협력 경로를 제한하라는 것이다.[^cho-183]

- 객체의 내부 구조를 묻지 말고, 무언가를 시켜라.

> 이처럼 협력하는 객체의 내부 구조에 대한 결합으로 인해 발생하는 설계 문제를 해결하기 위해 제안된 원칙이 바로 디미터 법칙(Law of Demeter)이다.
> 디미터 법칙은 객체가 자기 자신을 책임지는 자율적인 존재여야 한다는 사실을 강조한다.
정보를 처리하는 데 필요한 책임을 정보를 알고 있는 객체에게 할당하기 때문에 응집도가 높은 객체가 만들어진다.
>
> 하지만 무비판적으로 디미터 법칙을 수용하면 퍼블릭 인터페이스 관점에서 객체의 응집도가 낮아질 수도 있다.
자세한 내용은 이번 장에 포함된 "원칙의 함정" 절을 읽어보기 바란다.
>
> 디미터 법칙은 객체의 내부 구조를 묻는 메시지가 아니라 수신자에게 무언가를 시키는 메시지가 더 좋은 메시지라고 속삭인다.
[^cho-186]

### From: UML을 활용한 객체지향 분석 설계

> 객체 간 관계를 설정할 때 한 가지 유용한 지침을 디미터 법칙이라 부른다.
그 내용은 다음과 같다. "한 클래스에 속한 메소드들은 어떤 식으로든지 다른 클래스 구조에 의존해서는 안된다.
단, 직 상위 클래스 구조만은 예외로 의존해도 된다.
게다가 각 메소드가 메시지를 보낼 때도 극히 제한된 클래스 집합에 속하는 객체에게만 보내야 한다."
이 법칙을 적용해 얻을 수 있는 기본 효과는 느슨히 결합된 클래스가 생성되고, 그들의 구현 비밀은 캡슐화로 감춰진다는 것이다.
이런 클래스들이라면 아주 부담이 적어서 어떤 클래스의 의미를 알고자 할 때, 다른 여러 클래스의 상세한 내용까지는 알지 않아도 된다.[^uml-151]

### From: 실용주의 프로그래머

> 디미터 법칙은 객체의 모든 메서드는 다음에 해당하는 메서드만을 호출해야 한다고 말한다.
- 자신
- 메서드로 넘어온 인자
- 자신이 생성한 객체
- 직접 포함하고 있는 객체

> 디미터 법칙을 따르면 함수를 호출하는 클래스의 응답집합 크기를 줄일 수 있기 때문에 좀 더 에러가 적은 클래스들을 만들 수 있다.[^andrew-231]

즉, 객체의 협력 경로를 제한하라는 의미이다.

## 법칙의 준수와 위반
### 디미터 법칙을 잘 지킨 코드

디미터 법칙을 따르는 형태의 코드는 다음과 같이 매우 단순하다.

```java
object.method(parameter);
```

### 법칙을 지킬 필요가 없는 경우

한편, 객체가 아니라 자료구조라면 디미터 법칙을 거론할 필요가 없다.

>
```java
Options opts = ctxt.getOptions();
File scratchDir = opts.getScratchDir();
final String outputDir = scratchDir.getAbsolutePath();
```
(중략)  
위 예제가 디미터 법칙을 위반하는지 여부는 `ctxt`, `Options`, `ScratchDir`이 객체인지 아니면 자료 구조인지에 달렸다.
객체라면 내부 구조를 숨겨야 하므로 확실히 디미터 법칙을 위반한다.
반면, 자료 구조라면 당연히 내부 구조를 노출하므로 디미터 법칙이 적용되지 않는다.[^bob-124]

디미터 법칙은 경우에 따라 판별이 매우 애매하므로 이분법적으로 생각하지 않도록 한다.

### 디미터 법칙을 위반한 코드 - 기차 충돌

> 이 법칙을 따르지 않으면 메시지 체인(Message Chains)이란 악취가 나게 된다.[^andrew-227]

디미터 법칙을 위반한 전형적인 코드의 형태는 다음과 같다.

```java
object.getChild().getContent().getItem().getTitle();
```

`getter`가 줄줄이 이어진 모습이 기차와 닮아서 **열차 전복, 기차 충돌(train wreck)** 이라는 단어로 표현하기도 한다.

> 이 스타일을 따르지 않으면 '열차 전복' 코드라고도 알려진 코드가 만들어진다.
바로 접근자(getter) 메서드가 기차 객차처럼 연이어 이어진 경우다.[^steve-19]

&nbsp;

> 원거리의 간접적인 객체에 메시지를 보내기 위하여(즉, 원거리의 낯선 사람에게 이야기하기 위해서) 객체의 연결 경로를 따라 더 멀리 순회한다.
이러한 설계는 객체들이 어떻게 연결되어 있는지를 나타내는 특정한 구조와 결합된다.
**프로그램 순회의 경로가 길어질수록 프로그램은 더 불안정해진다.**
그 이유는 객체 구조(연결)는 변경될 수 있기 때문이다.[^larman-462]

## 주의: 디미터 법칙은 하나의 . 을 강제하는 규칙이 아니다

>
앞에서 설명한 것처럼 디미터 법칙은 "오직 하나의 도트만을 사용하라"는 말로 요약되기도 한다. 따라서 대부분의 사람들은 자바 8의 `IntStream`을 사용한 아래의 코드가 기차 충돌을 초래하기 때문에 디미터 법칙을 위반한다고 생각할 것이다.
```java
IntStream.of(1, 15, 20, 3, 9)
    .filter(x -> x > 10)
    .distinct()
    .count();
```
> 하지만 이것은 디미터 법칙을 제대0로 이해하지 못한 것이다.
위 코드에서 `of`, `filter`, `distinct` 메서드는 모두 `IntStream`이라는 동일한 클래스의 인스턴스를 반환한다. 즉, 이들은 `IntStream`의 인스턴스를 또다른 `IntStream`의 인스턴스로 변환한다.

> 따라서 이 코드는 디미터 법칙을 위반하지 않는다.
디미터 법칙은 결합도와 관련된 것이며, 이 결합도가 문제가 되는 것은 객체의 내부 구조가 외부로 노출되는 경우로 한정된다.
`IntStream`의 내부 구조가 외부로 노출됐는가? 그렇지 않다. 단지 `IntStream`을 다른 `IntStream`으로 변환할 뿐, 객체를 둘러싸고 있는 캡슐은 그대로 유지된다.

> 하나 이상의 도트(.)를 사용하는 모든 케이스가 디미터 법칙 위반인 것은 아니다. 기차 충돌처럼 보이는 코드라도 객체의 내부 구현에 대한 어떤 정보도 외부로 노출하지 않는다면 그것은 디미터 법칙을 준수한 것이다.[^cho-198]

## 부록
### 메시지 체인의 리팩토링

마틴 파울러의 "리팩토링"을 읽어보면 메시지 체인에 대한 언급이 있다.

> 메시지 체인은 클라이언트가 한 객체에 제 2의 객체를 요청하면, 제 2의 객체가 제 3의 객체를 요청하고, 제 3의 객체가 제 4의 객체를 요청하는 식으로 연쇄적 요청이 발생하는 문제점을 뜻한다.
이러한 메시지 체인은 수많은 코드 행이 든 `getThis` 메서드나 임시변수 세트라고 봐도 된다.
이런 요청의 왕래로 인해 클라이언트는 그 왕래 체제에 구속된다.
그 사이의 관계들에 수정이 발생할 때마다 클라이언트도 수정해야 한다.

> 이럴 때는 대리 객체 은폐(Hide DElegate, 195쪽)를 실시해야 한다.
이 기법은 원칙적으로 체인을 구성하는 모든 객체에 적용할 수 있지만, 그렇게 하면 모든 중간 객체가 중개 메서드로 변해서 과잉 중개 메서드(middle man)의 구린내를 풍기는 문제가 흔히 발생한다.
그래서 차라리 결과 객체가 어느 대상에 사용되는지를 알아내는 방법이 더 낫다.
그렇게 알아낸 객체가 사용되는 코드 부분을 메서드 추출(Extract Method, 142쪽)을 통해 별도의 메서드로 빼낸 후 메서드 이동(Move Method, 178쪽)을 실시해서 체인 아래로 밀어낼 수 있는지 여부를 검사해야 한다. 만약 체인에 속한 객체 중 한 객체의 여러 클라이언트가 나머지 객체들에 왕래한다면 그 기능을 수행하는 메서드를 추가하면 된다.
[^fowler-111]

### 객체지향 생활 체조

객체지향 생활 체조에 이와 관련된 규칙이 있다.

> **규칙 4. 한 줄에 한 점만 사용**

>
종종 하나의 동작에 대해 어떤 오브젝트가 맡고 있는지 구분하기 어려울 때가 있다.
여러 개의 점이 들어 있는 코드 몇 줄을 들여다보기 시작하면,
책임소재의 오류를 많이 발견하기 시작한다.
어떠한 코드 한 줄에서라도 점이 하나 이상 있으면 그른 곳에서 동작이 일어나고 있다는 뜻이다.
어쩌면 오브젝트는 다른 두 오브젝트들을 동시에 다루고 있는 것이다.
이 경우 그 오브젝트는 중개상, 즉 너무 많은 사람들에 대해 지나치게 알고 있는 꼴이다(마치 유통에 있어 중개상을 배제하고 직거래하듯).
문제의 동작을 관련 오브젝트 중에 하나로 옮겨보자.

>
그 모든 점들이 연결되어 있다면 대상 오브젝트는 딴 오브젝트에 깊숙이 관여하고 있다.
이런 중복된 점들은 캡슐화를 어기고 있다는 방증이기도 하다.
오브젝트가 자기 속을 들여다 보려 하기보다는 뭔가 작업을 하도록 만들려고 해야 한다.
캡슐화의 주요점은 클래스 경계를 벗어나 알 필요가 없는 타입으로 진입하지 않는 것이다.
[^thoughtworks-89]

참고로, 객체지향 생활 체조는 다음과 같이 9개의 규칙으로 이루어져 있다.

>
훈련의 규칙은 아래와 같다.
1. 한 메서드에 오직 한 단계의 들여쓰기만 한다.
2. `else` 예약어(keyword)를 쓰지 않는다.
3. 모든 원시값과 문자열을 포장(wrap)한다.
4. 한 줄에 점을 하나만 찍는다.
5. 줄여쓰지 않는다(축약금지).
6. 모든 엔티티(entity)를 작게 유지한다.
7. 2개 이상의 인스턴스 변수를 가진 클래스를 쓰지 않는다.
8. 제일 클래스(first-class) 콜렉션을 쓴다.
9. 게터(getter)/세터(setter)/프로퍼티(property)를 쓰지 않는다.[^thoughtworks-95]

## 참고문헌

- Clean Code / 로버트 C. 마틴 저/박재호, 이해영 역 / 인사이트(insight) / 초판 3쇄 2016년 05월 25일
- 리팩토링 / 마틴 파울러 저 / 김지원 역 / 한빛미디어 / 초판 2쇄 2013년 03월 07일 / 원서 : Refactoring (Addison-Wesley Professional; 1 edition, 1999)
- 실용주의 프로그래머 / 앤드류 헌트,데이비드 토머스 공저 / 김창준,정지호 공역 / 인사이트(insight) / 초판 1쇄 2005년 08월 15일
- 오브젝트 / 조영호 저 / 위키북스 / 2쇄 2019년 07월 17일
- 테스트 주도 개발로 배우는 객체 지향 설계와 실천 / 스티브 프리먼, 냇 프라이스 공저 / 인사이트(insight) / 초판 3쇄 2016년 07월 05일 / 원제 : Growing object-oriented software, guided by tests
- 소트웍스 앤솔러지 / 정지웅 역 / 위키북스 / 초판발행 2009년 02월 26일 / 원제 : The ThoughtWorks Anthology
- UML을 활용한 객체지향 분석 설계 / 그래디 부치, 로버트 막심처크, 마이클 잉글 등저 / 박현철, 임춘봉 등역 / 에이콘출판사 / 발행 2013년 01월 31일 / 원서 : Object-Oriented Analysis and Design with Applications Third Edition
- UML과 패턴의 적용 [3판] / Craig Larman 저 / 김수동 역 / 홍릉과학출판사 / 3판 1쇄 2005년 12월 10일

## 주석

[^andrew-227]: 실용주의 프로그래머. 5장. 227쪽. 역자 주석.
[^andrew-231]: 실용주의 프로그래머. 5장. 231쪽.

[^cho-183]: 오브젝트. 6장. 183쪽.
[^cho-184]: 오브젝트. 6장. 184쪽.
[^cho-185]: 오브젝트. 6장. 185쪽.
[^cho-186]: 오브젝트. 6장. 184쪽.
[^cho-198]: 오브젝트. 6장. 198쪽.
[^steve-19]: 테스트 주도 개발로 배우는 객체 지향 설계와 실천. 2장. 19쪽.

[^bob-123]: Clean Code. 6장. 123쪽.
[^bob-124]: Clean Code. 6장. 124쪽.
[^bob-395]: Clean Code. 17장. 395쪽.

[^fowler-111]: 리팩토링. Chapter 3. 111쪽.
[^thoughtworks-95]: 소트웍스 앤솔러지. 6장. 85쪽.
[^thoughtworks-89]: 소트웍스 앤솔러지. 6장. 89쪽.
[^thoughtworks-90]: 소트웍스 앤솔러지. 6장. 90쪽.

[^uml-151]: UML을 활용한 객체지향 분석 설계. 1부 3장. 151쪽.
[^larman-461]: UML과 패턴의 적용. 25장. 461쪽.
[^larman-462]: UML과 패턴의 적용. 25장. 462쪽.
