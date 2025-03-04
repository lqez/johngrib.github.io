---
layout  : wiki
title   : (요약) The mind behind Linux | Linus Torvalds
summary : 나는 엔지니어입니다
date    : 2020-07-09 21:41:30 +0900
updated : 2021-10-03 00:54:20 +0900
tag     : 
toc     : true
public  : true
parent  : [[summary]]
latex   : false
issue-number : 137
---
* TOC
{:toc}

<iframe max-width="100%" height="auto" src="https://www.youtube.com/embed/o8NPllzkFhE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

- 2016-05-04
- TED
- 인터뷰어: 크리스 앤더슨
- 인터뷰이: 리누스 토발즈

## 리누스 토발즈가 일하는 방식

일할 때 외부 자극을 받지 않기를 원한다.
- 벽지: 요양원 벽지 같은 차분한 색.
- 컴퓨터: 완벽하게 소음이 없어야 한다.
    - 강력하고 빠른 컴퓨터보다 조용한 컴퓨터가 좋다.
    - 무릎에 올라온 고양이의 가르릉 소리를 듣고 싶지, 컴퓨터 팬 소리는 듣고 싶지 않다.

## 오픈소스에 대하여

리눅스의 시작

- 토발즈는 집에서 혼자, 목욕 가운을 입고 일한다.
- 리눅스는 공동 프로젝트가 아니라 개인 프로젝트로 시작한 것이다.
    - 결과물이 필요해서.
    - 프로그램을 즐겼기 때문에.
- 리눅스를 시작했을 땐 오픈 소스를 의도하지 않았다.
- 프로젝트가 커지면서 다른 사람들에게 보여주고 싶어졌을 뿐이다. 대단하지 않았다.

사람들에 대하여

- 아이디어를 제공한 사람들의 도움이 크다.
    - 누군가가 코드를 읽고 아이디어를 준다.
- 토발즈는 사교적인 사람이 아니지만, 프로젝트에 의견을 주거나 기여하는 사람들을 좋아한다.
    - 프로젝트가 더 나아지기 때문.

## 기술의 발전에 대하여

> 토발즈: 제게 진짜 중요한 순간은 뭔가가 크게 되었을 때가 아니라 작게 될 때입니다.
>
> 혼자일 때가 아니라 10명, 아니 100명이 참여할 때입니다.
>
> 그러고 나면, 모든 것이 서서히 진행됩니다.
>
> 100명이 100만 명이 되는 것은 제게는 큰 일이 아닙니다.

- 뭔가가 크게 되었을 때가 아니라 작게 될 때가 중요한 순간이다.
    - 100명이 100만명이 되는 것보다 1명에서 10명, 10명에서 100명이 되는 것이 중요하다고 말한다.
- 중요한 것은 공동체를 이루고 성장시켜 가는 일.

## git에 대하여

- 수많은 사람들이 동시에 작업을 하고 있음.
- 규모에 따라 유지보수하는 방법이 달라진다.
- 어떤 프로젝트는 소스코드 유지보수만을 하기도 한다.

CVS

- CVS가 너무 싫어서 CVS를 쓰기 싫었다.
- 그래서 급진적이고 흥미있는 작업을 해서 git을 만들었다.

git

- git은 토발즈에게 두 번째로 큰 프로젝트.
- 오직 제 1 프로젝트인 리눅스를 유지보수할 용도로 만든 도구.
    - 토발즈는 이런 방식으로 일한다.
    - 코딩은 재미로 한다.
    - 지금까지 토발즈가 참여한 모든 프로젝트는 자신에게 필요한 것이었다.

## 성격

꾸준함

- 괴짜였다.
- 사교적이지 않았다.
- 컴퓨터, 수학, 물리학에 푹 빠져 있었고 능숙했다.
    - 그러나 특별히 뛰어났다고는 생각하지 않는다.
- 여동생이 말하는 토발즈의 특출난 점: 포기하지 않는 것.
- 뭔가 시작하자마자 끝내는 일이 드물고, 오래 잡고 있었다.
    - 실리콘밸리에서 7년간 하나의 회사를 다녔다. (실리콘밸리의 프로그래머들은 7년이면 수차례 이직을 한다)

완고한 성격

- 완고한 성격 때문에 사람들과 논쟁하기도 하지만,
    - 여러 사람들이 어울려 일할 수 있는 오픈소스를 정말 좋아한다.
    - 서로를 좋아하지 않아도 같이 일할 수 있다.

오픈소스로 상업적인 이익을 얻는 사람들

- 이익을 위해 오픈소스를 쓰는 사람들? 정말 좋은 사람들이다.
- 토발즈가 관심만 있고 하지 않았던 일들을 대신 해주었다.
- 토발즈가 원하지 않았던 방법으로 오픈소스를 사용했다.
    - 그런 방식으로 일이 진행되는 것이 멋지다고 생각한다.

사교적인 사람

- 주위에 따뜻하고, 친절하고 사교적이고, 소통을 잘 하는 사람이 있어야 한다.
- 그런 사람들이 여러분을 공동체로 이끌어준다.

취향

- (`if`문을 제거한 코드를 보여주며) 예외 상황이 없는 코드가 더 좋다.
- 함께 일하고 싶은 사람을 보는 기준: 좋은 취향을 갖고 있는가?
- 좋은 취향은 대규모 패턴을 볼 때 알 수 있다.
    - 좋은 취향: 본능적인 감각으로 무엇을 하는 것이 옳은지를 아는 것.

미래에 대한 비전

- 토발즈: 나는 선지자가 아니다.
    - 5년 간의 계획도 없다.
    - 나는 엔지니어다.

> 저는 엔지니어입니다. 저는 많은 사람들과 함께 해서 무척 행복합니다.
같이 걷거나 그냥 구름을 바라보거나 별을 보면서 "저기 가보고 싶다"고 얘기하는 사람들 말입니다.
>
하지만 저는 땅을 바라봅니다. 그리고는 제 바로 앞에 있는 웅덩이를 메우려고 합니다. 누군가 빠지지 않게 말입니다.
>
> 저는 그런 사람입니다.

## 에디슨과 테슬라

- 사람들은 테슬라를 좋아한다. 에디슨은 종종 비난받는다.
- 토발즈는 에디슨 편이다.
    - 테슬라는 최근 사람들이 좋아하지만 실제로 세상을 변화시킨 것은 에디슨이다.
    - 에디슨은 좋은 사람이 아니었지만 많은 일을 했다.

## 돈

구글 같은 회사들은 토발즈의 소프트웨어로 많은 돈을 벌었다. 열받지 않나?

> 아닙니다.

- 이유
    - "저는 잘 하고 있습니다."
    - 오픈소스가 아니었으면 리눅스는 지금처럼 성공할 수 없었을 것이다.
    - 누리보지 못했던 대단한 경험들을 많이 할 수 있게 됐다.
    - 자신을 행복하게 만드는 여러 일들이 진행되고 있다.

## 오픈소스 아이디어는 충분히 실현되었는가?

- 그렇다고도 생각하고, 아니라고도 생각한다.
- 코드는 논쟁의 여지가 적다. 하지만 그럼에도 논쟁을 한다.
- 정치 사안과 관련된 토론 등은 동의하기 어려운 경우도 있다.
- 오픈소스는 과학 분야에서 다시 대세가 되고 있다.
    - 역사적으로 오픈소스는 과학에서 시작됐다.


> 크리스 앤더슨: 하지만 당신은 선지자가 아니고 새로운 것을 얘기하는 것은 당신 몫이 아니지 않습니까.
>
> 리누스 토발즈: 맞습니다. 그것은 여러분에게 달려있습니다, 그렇지 않습니까?


