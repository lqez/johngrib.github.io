---
layout  : wiki
title   : ACID
summary : 트랜잭션의 중요한 네 가지 속성
date    : 2019-10-03 00:33:18 +0900
updated : 2021-06-22 23:11:51 +0900
tag     : db
toc     : true
public  : true
parent  : [[jargon]]
latex   : false
---
* TOC
{:toc}

## 개요

네 가지 속성의 이니셜을 따서 ACID라 부른다.

- Atomicity, Consistency, Isolation, Durability

## 인용

### From: 트랜잭션 처리의 원리

>
* **원자성(atomicity)**: 트랜잭션은 모두 실행되거나 아예 실행되어서는 안된다. 성공적인 트랜잭션은 commit 하고 실패한 트랜잭션은 abort 한다. commit은 데이터베이스를 변경하여 영속적이게 하며, abort는 데이터베이스 변경을 undo 하거나 삭제한다.
* **일관성(consistency)**: 트랜잭션은 데이터베이스의 내부 일관성을 지켜야 한다. 각 트랜잭션은 일관성을 보장하도록 프로그램을 작성한다.
* **고립성(isolation)**: 트랜잭션은 독립적으로 실행되어야 하고, 다른 트랜잭션과 섞여 실행되면 안된다. 트랜잭션의 집합을 실행한 결과가 이들을 한 번에 하나씩 실행하는 결과와 동일해야 한다. 이런 동작방식을 직렬성이라고 하며 잠금에 의해서 이행된다.
* **영속성(durability)**: 트랜잭션의 결과는 시스템 실패로 유실되면 안된다. 정전이나 운영체제 장애 시에도 보존될 수 있도록 디스크 등의 저장장치에 저장한다.
>
-- 트랜잭션 처리의 원리[^list]

* 고립성은 '격리성'이라고도 한다.
* 영속성은 '지속성'이라고도 한다.

### From: 데이터베이스 인터널스

>
DBMS에서 트랜잭션이란 하나의 논리적 작업 단위를 의미하며 여러 작업을 한 단계로 표현하는 방법이다.
작업은 데이터베이스의 읽기와 쓰기를 모두 포함한다.
모든 데이터베이스 트랜잭션은 원자성과 일관성, 격리성, 지속성을 보장한다.
이 네 가지 속성을 줄여서 ACID 라고 부른다[HAERDER83].
>
_원자성 Atomicity_
>
트랜잭션을 더 작은 단계로 나눌 수 없다.
트랜잭션과 관련된 작업은 모두 실행되거나 모두 실패해야 한다는 의미이다.
트랜잭션은 부분적으로 실행될 수 없다.
트랜잭션은 커밋(트랜잭션의 쓰기 작업의 결과를 실제 데이터에 반영)되든지 실패(abort, 아직 적용되지 않은 트랜잭션의 모든 작업을 롤백)하든지 둘 중 하나여야 한다.
커밋은 트랜잭션의 마지막 단계다.
실패한 트랜잭션은 재시도할 수 있다.
>
_일관성 Consistency_
>
일관성은 애플리케이션이 제어하는 속성이다.
트랜잭션은 참조 무결성 등의 제약 조건을 위반하지 않고 데이터베이스를 하나의 유효한 상태에서 또 다른 유효한 상태로 변경한다.
일관성은 가장 약하게 정의된 성질로, 데이터베이스가 아닌 사용자가 제어할 수 있는 유일한 속성이다.
>
_격리성 Isolation_
>
동시에 수행되는 여러 트랜잭션은 다른 트랜잭션이 존재하지 않는 것처럼 서로 간섭 없이 수행돼야 한다.
격리성은 수정 내용이 반영되는 시점과 동시 수행 중인 트랜잭션이 접근할 수 있는 데이터를 정의한다.
많은 데이터베이스는 성능상의 이유로 여기서 설명한 격리성의 정의에 비해 약한 격리 수준(isolation level)을 사용한다.
동시성 제어 방식에 따라 트랜잭션의 변경 내용 중 일부가 동시 수행 중인 다른 트랜잭션에 노출될 수도 있고 노출되지 않을 수도 있다('격리 수준' 절 참고).
>
_지속성 Durability_
>
트랜잭션 커밋 후 디스크에 저장된 데이터베이스의 상태는 시스템이 중단되거나 정전 또는 시스템 장애가 발생해도 그대로 유지돼야 한다.
>
트랜잭션을 수행하기 위해서는 데이터를 디스크에 저장하고 유지하는 자료 구조 외에도 여 러 컴포넌트가 필요하다. 트랜잭션 매니저는 트랜잭션의 세부 단계를 제어, 관리 및 스케줄 링하는 컴포넌트다.
>
-- 데이터베이스 인터널스. 5장. 119쪽.


### From: 자바 ORM 표준 JPA 프로그래밍

>
트랜잭션은 ACID(<https://en.wikipedia.org/wiki/ACID >)라 하는 원자성(Atomicity), 일관성(Consistency), 격리성(Isolation), 지속성(Durability)을 보장해야 한다.
>
- **원자성**: 트랜잭션 내에서 실행한 작업들은 마치 하나의 작업인 것처럼 모두 성공하든가 모두 실패해야 한다.
- **일관성**: 모든 트랜잭션은 일관성 있는 데이터베이스 상태를 유지해야 한다. 예를 들어 데이터베이스에서 정한 무결성 제약 조건을 항상 만족해야 한다.
- **격리성**: 동시에 실행되는 트랜잭션들이 서로에게 영향을 미치지 않도록 격리한다. 예를 들어 동시에 같은 데이터를 수정하지 못하도록 해야 한다. 격리성은 동시성과 관련된 성능 이슈로 인해 격리 수준을 선택할 수 있다.
- **지속성**: 트랜잭션을 성공적으로 끝내면 그 결과가 항상 기록되어야 한다. 중간에 시스템에 문제가 발생해도 데이터베이스 로그 등을 사용해서 성공한 트랜잭션 내용을 복구해야 한다.
>
-- 자바 ORM 표준 JPA 프로그래밍[^jpa-16]

### From: 마이크로서비스 도입 이렇게 한다

> ACID는 데이터 저장소의 내구성과 일관성을 보장하기 위해 신뢰할 수 있는 시스템으로 이끄는 데이터베이스 트랜잭션의 주요 속성을 개괄하는 약어다.
ACID는 원자성(Atomicity), 일관성(Consistency), 격리(Isolation), 내구성(Durability)을 의미하는 약어로서, 각 속성이 제공하는 특성은 다음과 같다.
>
- 원자성
    - 트랜잭션 내에서는 모든 연산이 모두 완료되거나 모두 실패하거나 둘 중 한 가지 상태를 보증한다. 어떤 이유로든 시도하는 변경 내역이 실패하면 전체 연산은 중단되고 마치 아무런 변경사항도 없는 것처럼 보인다.
- 일관성
    - 데이터베이스가 변경되면, 유효하며 일관된 상태로 유지된다.
- 격리
    - 여러 트랜잭션이 간섭 없이 동시에 작동할 수 있다. 이는 어떤 트랜잭션 중에 이뤄진 모든 중간 상태 변경이 다른 트랜잭션에 보이지 않게 하는 방법으로 달성된다.
- 내구성
    - 일단 트랜잭션이 완료되고 나면 시스템 오류가 발생하는 상황에서도 데이터가 손실되지 않는다고 보장한다.
>
모든 데이터베이스가 ACID 트랜잭션을 제공하지는 않는다는 사실을 주목해야 한다.
내가 지금까지 사용한 모든 관계형 데이터베이스 시스템과 네오포제이(Neo4j) 같은 최신 NoSQL 데이터베이스만 ACID 트랜잭션을 지원한다.
수년 동안 몽고DB는 단일 문서(document)에 대한 ACID 트랜잭션만 지원했기에, 문서를 둘 이상 원자적으로 업데이트하고 싶은 경우에는 문제가 일어날 수 있다.
>
-- 마이크로서비스 도입 이렇게 한다. 4장. 228쪽.

## 원자성(Atomicity)

* 트랜잭션이 완전히 실행되거나 전혀 실행되지 않음(all-or-nothing)을 의미한다.[^atomicity0]
* 트랜잭션에 포함된 모든 작업이 성공(Commit) 또는 실패(Abort) 하는 성질을 원자성이라고 한다.[^atomicity1]

>
트랜잭션 프로그램은 부분적으로 실행되어선 안된다.
예를 들어, A계정에서 B계정으로 100$를 이체하는 트랜잭션 프로그램을 실행한다는 가정을 해보자.
이 프로그램은 A계정에서 100$를 출금하여 B계정에 100$를 입금시킨다.
이를 트랜잭션으로 실행할 때, 그 트랜잭션은 원자성이 있어야 한다.
즉, 양쪽 업데이트를 모두 실행하거나 어느 쪽도 실행하지 말아야 한다.
둘 중 하나만 업데이트되는 상황이 있어서는 안 된다.
[^atomicity0]

한편 abort는 원자성의 중요한 특징이다.

> 오류가 생겼을 때 트랜잭션을 어보트하고 해당 트랜잭션에서 기록한 모든 내용을 취소하는 능력은
ACID 원자성의 결정적인 특징이다. 아마도 **어보트 능력(abortability)**이 **원자성**보다 나은 단어겠지만
**원자성**이 자주 쓰이므로 이 단어를 계속 사용하겠다.[^abortability]

* TP 시스템[^tp]은 데이터베이스 메커니즘을 이용하여 원자성을 보장한다.
* **commit**: 트랜잭션의 성공적인 완수를 commit이라 한다.
* **abort**: 트랜잭션의 실패를 abort라 한다.
* undo: 트랜잭션 프로그램이 작업 도중 실패하면, 트랜잭션이 수정한 내용을 모두 undo 한다.
    * 이를 통해 DB가 트랜잭션 실행 이전 상태로 돌아가게 보장해야 한다.



### 보상 트랜잭션(compensating transaction)

원자성을 완벽하게 보장하는 것은 어렵다. 보상 트랜잭션에 대해서도 알아두자.

* commit된 트랜잭션이 실수였다는 것이 밝혀졌을 때, 결과를 바로잡기 위해 실행하는 트랜잭션.
    * **입금** 트랜잭션이 오류였다면, **출금** 트랜잭션으로 결과를 바로잡는다.
    * 무료 상품권을 제공하고, 사과 이메일을 전송하는 등등..
* TP 애플리케이션을 잘 설계하려면 모든 트랜잭션에 대해 보상 트랜잭션을 고려해야 한다.

### 원자성과 고립성

> 이를테면 다중 스레드 프로그래밍에서 한 스레드가 원자적 연산을 실행한다면
다른 스레드에서 절반만 완료된 연산을 관찰할 수 없다.
시스템은 연산을 실행하기 전이나 실행한 후의 상태에만 있을 수 있으며 그 중간 상태에는 머무를 수 없다.
<br><br>
반대로 ACID의 맥락에서 보면 원자성은 동시성과 관련이 없다.
원자성은 여러 프로세스가 동시에 같은 데이터에 접근하려고 할 때 무슨 일이 생기는지 설명하지 않는다.
이 문제는 I, 즉 격리성에서 다루기 때문이다.
[^abortability]


## 일관성(Consistency)

>
트랜잭션 프로그램은 데이터베이스의 일관성을 유지해야 한다.
즉, 처음에 일관적인 데이터베이스에서 트랜잭션을 수행하는 경우,
트랜잭션 실행 종료 후에도 데이터베이스는 일관적이어야 한다.  
일관성이란 '내부적 일관성'을 의미한다.
데이터베이스 측면에서는 데이터베이스가 적어도 무결성 제약조건(integrity constraint)을 모두 충족시킨다는 의미다.
아래는 데이터베이스 시스템이 일반적으로 유지할 수 있는 무결성 제약조건의 종류다.
<br>
* Primary Key는 유일해야 한다.<br>(예: 두 종업원의 기록에 동일한 종업원 번호는 없다.)
* 데이터베이스는 참조 무결성(referential integrity)을 가져야 하며, 이는 레코드가 참조하는 객체는 반드시 존재해야 한다는 의미다.<br>(예: 주문 레코드에 의해 참조되는 고객 레코드가 존재)
* 어떤 데이터 값은 특정 범위 내에 있어야 한다.<br>(예: 연령은 120세 이하이며 주민등록번호는 0이 아니다.)
[^prin-consistency]

이러한 일관성은 꼭 DB에서만 지켜야 하는 것은 아니다.

>
TP 시스템을 떠나 현실에서도 일관성이 이슈가 되는 경우가 있다.
예를 들어 재고 수량은 실제 창고에 있는 재고 수량과 일치해야 한다.
이 제약 조건은 창고 물품의 입출고 업무를 정확히 보고하는 등의 물리적 행동에 의존한다.
궁극적으로 이것이 바로 기업이 일관성이라고 간주하는 것이다.
[^prin-consistency]

즉, 일관성은 애플리케이션의 속성이기도 하다.

>
ACID 일관성의 아이디어는 항상 진실이어야 하는, 데이터에 관한 어떤 선언(불변식(invariant))이 있다는 것이다.
예를 들어 회계 시스템에서 모든 계좌에 걸친 대변과 차변은 항상 맞아떨어져야 한다.
<br>(중략)<br>
그러나 일관성의 아이디어는 애플리케이션의 불변식 개념에 의존하고, 일관성을 유지하도록 트랜잭션을 올바르게 정의하는 것은 애플리케이션의 책임이다.
이는 데이터베이스가 보장할 수 있는 게 아니다.
데이터베이스는 불변식을 위한하는 잘못된 데이터를 쓰지 못하도록 막을 수 없다.
<br>(중략)<br>
원자성, 격리성, 지속성은 데이터베이스의 속성인 반면(ACID에서의) 일관성은 애플리케이션의 속성이다.
애플리케이션에서 일관성을 달성하기 위해 데이터베이스의 원자성과 격리성 속성에 기댈 수는 있지만 데이터베이스만으로 되는 것은 아니다.
따라서 C는 실제로는 ACID에 속하지 않는다.
[^c-in-acid]

## 고립성(Isolation)

* 동시에 실행되는 여러 개의 트랜잭션이 서로 영향을 주지 않는 성질이다.[^isolation0]
* 동시에 실행되는 트랜잭션은 서로 격리된다는 것을 의미한다.[^isolation1]

고립성은 기술적으로 "직렬성(serializability)"으로 정의되곤 한다.
즉 실행 결과의 관점에서, 개별 트랜잭션의 실행 결과가 트랜잭션을 직렬로 실행했을 때와 결과가 같다면 고립성을 준수하고 있는 것이다.

> 어떤 실행의 결과가 트랜잭션의 어떤 두 실행과 중복 없이 순차적으로 연달아서
이들 트랜잭션을 직렬로 실행하는 것과 같은 경우에 그 실행은 직렬적이라고 하며,
트랜잭션을 한 번에 하나씩 실행하는 것과 같은 결과이다.
[^prin-isolation]

* 고립성을 잘 갖춘 시스템이라면, 사용자 관점에서는 시스템을 혼자서만 사용하고 있는 것처럼 생각하고 이용할 수 있다.
* DB는 여러 트랜잭션을 병렬로 수행하기 위해 각 트랜잭션이 엑세스하는 데이터에 잠금(locking)을 설정한다.
    * 모든 처리를 직렬로만 처리하면 너무 비효율적이기 때문.
    * 잠금 처리를 통해 여러 트랜잭션의 실행이 직렬로(순서대로) 일어나는 것처럼 보이게 하는 것이 중요.

## 영속성(Durability)

* 트랜잭션이 실행을 commit 할 때 정전 또는 운영체제에 장애가 발생해도 모든 업데이트가 기억장치에 저장됨을 의미한다.[^prin-durability]
* 일단 커밋이 완료된 트랜잭션이 손상되지 않는 성질이다.[^durability2]
* 트랜잭션이 성공적으로 커밋됐다면 하드웨어 결함이 발생하거나 데이터베이스가 죽더라도 트랜잭션에서 기록한 모든 데이터는 손실되지 않는다는 보장이다.[^durability3]

영속성을 보장하기 위해 쓰이는 기법 중 하나인 로깅에 대해서도 알아두자.

>
영속성은 TP 시스템이 실행되는 동안 모든 트랜잭션의 수정 사항을 로그 파일에 남기는 방법을 사용한다.
트랜잭션 프로그램이 commit 되는 시점에, 시스템은 먼저 로그 파일에 쓰여진 레코드를 기억장치로 옮기고
트랜잭션 프로그램으로 돌아가는데, 이는 이 시점에서 트랜잭션이 사실상 commit 되고 결과 값이 영속적이라는 것을 나타낸다.
그러나 트랜잭션이 commit 된 후 데이터베이스를 수정하기 전에 시스템에 장애가 발생하면, 시스템 복구 후에 데이터베이스를 복구해야 한다.
데이터베이스 복구작업을 위해서 시스템은 로그 파일에서 commit 된 트랜잭션에 의한 수정 사항 중 실제로 데이터베이스에 적용되지 않은 것을 찾아서 데이터베이스에 적용한다.
이러한 복구작업이 끝나면 시스템은 정상 운영을 시작한다.
이런 방법으로 시스템이 복구되면, 모든 트랜잭션은 시스템 장애 이전에 commit 된 트랜잭션의 수정사항이 반영된 데이터베이스를 이용하게 된다.
[^prin-durability]


## 비판

> 1983년, 테오 하더(Theo Härder)와 안드레아스 로이터(Andreas Reuter)는 데이터베이스에서 내결함성 메커니즘을 나타내는 정확한 용어를 확립하기 위해 ACID를 만들었다.  
그러나 현실에서는 데이터베이스마다 ACID 구현이 제각각이다.
예를 들어 곧 보게 되겠지만 **격리성**의 의미 주변에는 모호함이 많이 있다.
상위 수준의 아이디어는 견실하지만 악마는 세부 사항에 있다.
오늘날 시스템이 "ACID를 준수(ADIC compliant)"한다고 할 때 그 시스템에서 실제로 어떤 것을 기대할 수 있는지 분명하지 않다.
ACID는 유감스럽게도 거의 마케팅 용어가 돼버렸다.  
(ACID 표준을 따르지 않는 시스템은 때로 **BASE**라고 불린다. 기본적으로 가용성을 제공하고(Basically Available), 유연한 상태를 가지며(Soft state), 최종적 일관성(Eventual consistency)을 지닌다는 뜻이다. ACID의 정의보다 더 모호하다. BASE의 그럴듯한 정의는 "ACID가 아니다" 뿐인 것 같다. 즉 아무 의미나 갖다 붙일 수 있는 것처럼 보인다.)
[^history]

* 참고로 "데이터 중심 애플리케이션 설계"에서는 Joe Hellerstein이 C에 대해 "tossed in to make the acronym work", 즉 "약어를 만들기 위해" 끼워넣었다는 주장[^c-in-acid]이 있다. 아마도 그의 저서들 중 하나에 나온 말일 것이라는 생각이 들지만 나는 찾아내지 못했다.


## 참고문헌

* 도서
    * 관계형 데이터베이스 실전 입문 / 오쿠노 미키야 저 / 성창규 역 / 위키북스 / 초판 2016년 07월 20일 / 원서 : 理論から學ぶデ-タベ-ス實踐入門 リレ-ショナルモデルによる效率的なSQL/奧野幹也
    * 데이터 중심 애플리케이션 설계 / 마틴 클레프만 저/정재부, 김영준, 이도경 역 / 위키북스 / 초판발행 2018년 04월 12일
    * 데이터베이스 인터널스 / 알렉스 페트로프 저/이우현 역/이태휘 감수 / 에이콘출판사 / 2021년 01월 29일 / 원서 : Database Internals: A Deep Dive into How Distributed Data Systems Work
    * 마이크로서비스 도입 이렇게 한다 / 샘 뉴먼 저/박재호 역 / 책만 / 2021년 01월 20일 / 원서 : Monolith to Microservices: Evolutionary Patterns to Transform Your Monolith
    * 자바 ORM 표준 JPA 프로그래밍 / 김영한 저 / 에이콘출판사 / 2015년 07월 28일
    * 트랜잭션 처리의 원리 / 필립 A. 번스타인, 에릭 뉴코머 공저 / 한창래 역 / KICC(한국정보통신) / 1판 1쇄 2011년 12월 19일
* 웹 문서
    * [Theo Harder, Andreas Reuter: "Principles of Transaction-Oriented Database Recovery", 1983][haerder-1983]: ACID가 최초로 소개된 논문. [백업](https://web.archive.org/web/20190923153438/https://sites.fas.harvard.edu/~cs265/papers/haerder-1983.pdf )

## 주석

[^list]: 트랜잭션 처리의 원리. 1 개요. 52쪽.
[^tp]: Transaction Processing System
[^atomicity0]: 트랜잭션 처리의 원리. 1.3 원자성, 일관성, 고립성, 영속성. 27쪽.
[^atomicity1]: 관계형 데이터베이스 실전 입문. 14 트랜잭션의 본질. 292쪽.
[^prin-consistency]: 트랜잭션 처리의 원리. 1.3 원자성, 일관성, 고립성, 영속성. 31쪽.
[^prin-isolation]: 트랜잭션 처리의 원리. 1.3 원자성, 일관성, 고립성, 영속성. 32쪽.
[^prin-durability]: 트랜잭션 처리의 원리. 1.3 원자성, 일관성, 고립성, 영속성. 32쪽.
[^history]: 데이터 중심 애플리케이션 설계. 7장 트랜잭션. 223쪽.
[^abortability]: 데이터 중심 애플리케이션 설계. 7장 트랜잭션. 224쪽.
[^c-in-acid]: 데이터 중심 애플리케이션 설계. 7장 트랜잭션. 225쪽.

[^isolation0]: 관계형 데이터베이스 실전 입문. 14 트랜잭션의 본질. 294쪽.
[^isolation1]: 데이터 중심 애플리케이션 설계. 7장 트랜잭션. 226쪽.

[^durability2]: 관계형 데이터베이스 실전 입문. 14 트랜잭션의 본질. 294쪽.
[^durability3]: 데이터 중심 애플리케이션 설계. 7장 트랜잭션. 226쪽.

[^jpa-16]: 자바 ORM 표준 JPA 프로그래밍. 16장.

[haerder-1983]: https://sites.fas.harvard.edu/~cs265/papers/haerder-1983.pdf
