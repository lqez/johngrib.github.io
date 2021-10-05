---
layout  : wiki
title   : 디자인 패턴 인용문 모음
summary : 
date    : 2019-11-20 21:30:04 +0900
updated : 2021-10-04 13:00:23 +0900
tag     : anti-pattern
toc     : true
public  : true
parent  : [[/pattern]]
latex   : false
---
* TOC
{:toc}

## 주의: 패턴 중독

### 패턴을 과도하게 도입하지 않도록 주의하자

> 프로젝트 전반에 걸쳐 불필요하게 패턴으로 도배하는 것은 엔지니어링 관점에서 도가 지나친 것입니다. 디자인 패턴들은 마술이 아니며, 솔루션이 좋은 디자인이라고 자동적으로 보장해 주지도 않습니다. 디자인 패턴들은 단지 되풀이되는 문제들에 대한 재사용 가능한 솔루션들입니다. 다른 사람들이 그것을 발견하고 문서화해옴으로써 우리가 이미 발명된 바퀴를 찾고 있음을 깨닫게 해줍니다. 문제가 발생할 때 이러한 솔루션으로 해결될 수 있는 문제를 가려내고, 디자인 패턴을 적절하게 적용하는 것이 우리가 할 일입니다. 디자인 패턴에 대한 지식을 과시하려는 여러분의 욕구가 실용주의적인 시각을 가리지 않도록 하십시오. 여러분의 시야를 효과적인 비즈니스 솔루션을 제공하는 시스템을 설계하는 데 초점을 맞추고, 패턴은 각 패턴이 언급하는 문제를 해결하는 데 사용하십시오.
>
-- 소프트웨어 아키텍트가 알아야 할 97가지. 110쪽.

### 숙련자라도 패턴중독에 빠질 수 있다

>
패턴 중독의 폐해는 초보 프로그래머에만 국한된 것이 아니다.
중급 또는 고급 프로그래머 역시 패턴 중독으로부터 자유롭지 못하고, 세련된 패턴 책이나 글을 본 후라면 더욱 그렇다.
예를 들어 내가 개발을 돕던 시스템에서 Closure 패턴을 구현한 코드를 발견한 적이 있었는데,
나중에 알고 보니 그 프로젝트의 어느 프로그래머가 얼마 전에 어떤 위키 페이지[^c2-closure]에서 Closure 패턴을 보고 배웠다는 것이었다.
>
코드를 살펴봤지만 Closure 패턴의 사용을 정당화할 만한 이유를 찾을 수가 없었다.
Closure 패턴은 불필요했다.
따라서 나는 리팩터링을 통해 Closure 패턴을 제거하고, 그 자리를 보다 단순한 코드로 대체했다.
작업을 끝낸 후 그 팀의 프로그래머들에게 새로 바꾼 코드가 Closure를 사용하는 것보다 단순하다고 생각하지 않느냐 물었다.
그들은 코드가 더 단순해졌다고 대답했다. 결국 그 코드의 작성자도 리팩터링된 코드가 더 단순하다는 것을 인정했다.
>
패턴을 배우는 과정에서 패턴 중독을 피하기는 아마 거의 불가능할 것이다.
사실 우리는 대부분 실수를 통해 배운다. 나역시 여러 경우에서 패턴 중독에 빠져 있었다.
>
패턴의 진정한 성과는 패턴을 현명하게 사용할 때 나타난다.
리팩터링은 중복을 제거하고, 코드를 단순화하고, 코드가 그 의도를 잘 드러내도록 하는 데에 우리의 주의를 집중하도록 함으로써, 패턴을 현명하게 사용하도록 도와준다.
리팩터링을 통해 점진적으로 패턴을 도입하면, 패턴으로 인한 과도한 설계가 발생할 기회도 줄어든다.
그리고 리팩터링을 더 잘 이해할수록 패턴이 주는 즐거움을 이해할 확률도 높아진다.
>
-- 패턴을 활용한 리팩터링. 3장. 60쪽.

### 패턴을 구현하는 방법은 다양하다

>
요점은, 하나의 패턴도 여러 가지 방법으로 구현할 수 있다는 것이다.
>
불행히도, 프로그래머들은 [Design Patterns]의 각 패턴에 제시된 구조 다이어그램만을 보고 그것이 해당 패턴을 구현하는 유일한 방법이라는 결론을 내려버리는 경우가 종종 있다.
프로그래머들이 구현 노트를 주의 깊게 읽었더라면, 그러지 않을 것이다.
그러나 많은 프로그래머들이 [Design Patterns]를 펼쳐 구조 다이어그램을 확인한 다음, 바로 코딩을 시작한다.
그 결과로 나온 코드는 당장의 필요에 가장 잘 맞는 패턴 구현이 아니라, 구조 다이어그램을 그대로 구현한 것일 뿐이다.
>
[Design Patterns]가 출간된 지 몇 년 후, 공동 저자 중 한 명인 John Vlissides는 다음과 같은 글을 썼다.
>
> > 패턴의 구조 다이어그램은 명세가 아니라 단지 예제일 뿐이라는 것은 아무리 강조해도 지나치지 않을 것 같다.
> > 구조 다이어그램은 우리가 가장 자주 본 구현을 나타낼 뿐이다.
> > 이런 구조 다이어그램이 자기 자신의 구현과 많은 공통점이 있을 수도 있겠지만, 차이가 생기는 것은 피할 수 없고,
> > 사실은 차이가 있는 것이 바람직하다고까지 할 수 있다.
> > 최소한 구성 요소의 이름은 자신의 도메인에 맞게 바꿀 것이다.
> > 구현상의 트레이드오프trade-off는 경우에 따라 다르고, 자신의 구현은 구조 다이어그램과 상당히 다르게 보일 수 있다.
>
-- 패턴을 활용한 리팩터링. 3장. 63쪽.


## 패턴과 이디엄

> 패턴에 대해 본격적으로 살펴보기에 앞서 패턴(pattern)과 이디엄(idiom)을 비교해 보기로 하자. 디자인 패턴을 매우 일상적으로 사용하게 되면 이는 패턴이 아니라 이디엄이다. 이런 상황에서는 패턴이 특별한 무엇이 아닌 '이미 그렇게 되어 있는 것'일 뿐이다. 어떤 사람들은 패턴은 정형적인 방식으로 표현되어 있는 반면 이디엄은 그렇지 않다는 식으로 패턴과 이디엄을 구분하기도 하지만, 나는 이와 같은 정의를 따르지 않는다. 이디엄은 일상적으로 사용하게 된 패턴이다.  
상속은 패턴이 이디엄으로 진화해 간 훌륭한 예이다. 1980년대 초 C 언어가 왕이었을 무렵 상속은 하나의 디자인 패턴이었다. 실제 C에서 'extends' 관계를 사용하는 여러 예들을 볼 수 잇다. 구체적인 예를 하나 들자면 malloc()의 표준 구현은 헤더(부모 클래스)를 사용하는데, 이 헤더는 확장(extends)되어 새로운 구조체(자식 클래스)를 생성할 수 있고, 자식 클래스는 부모 클래스의 free() 메소드를 상속하게 된다.
>
추상 함수 역시 상속 패턴의 일부였다. C에서 다른 목적을 위해 다르게 초기화된 함수 포인터의 테이블을 넘기는 것은 흔한 일이었다. 그리고 이는 C++가 abstract 메소드와 인터페이스 상속을 구현하는 방식과 같지만 C 세계에서는 이를 지칭하는 이름이 없었다.  
상속은 C 언어에 내장되어 있지 않았으며, 대부분의 C 프로그래머들은 상속을 이용하여 프로그래밍하지 않았다. 그러므로 상속은 프로그래밍 이디엄이 아닌 패턴이었다. C에서의 상속은 비슷한 류의 문제를 해결할 때 많은 프로그램에서 발견되는 방법이었지만, 초중급 수준의 C 프로그래머들이 이용하는 방법은 아니었다. 요즘은 상속과 인터페이스 같은 기능이 많은 언어에 내장되어 있다. 이들은 이디엄이 된 것이다.
>
-- 실전 코드로 배우는 실용주의 디자인 패턴. 22쪽.

## 참고문헌

- 소프트웨어 아키텍트가 알아야 할 97가지 / Richard Monson-Haefel 저 / Eva Study 역 / 지앤선(志&嬋) / 2011년 04월 14일 / 원제 : 97 Things Every Software Architect Should Know
- 실전 코드로 배우는 실용주의 디자인 패턴 / Allen Holub 저 / 송치형 편역 / 지앤선(志&嬋) / 2006년 07월 19일 발행 / 원제 : Holub on Patterns : Learning Design Patterns by Looking at Code
- 패턴을 활용한 리팩터링 / 조슈아 케리에브스키 저 / 윤성준, 조상민 공역 / 인사이트(insight) / 신판 1쇄 발행 2011년 02월 09일 / 원제 : REFACTORING TO PATTERNS

## 주석

[^c2-closure]: <https://wiki.c2.com/?UseClosuresNotEnumerations >
