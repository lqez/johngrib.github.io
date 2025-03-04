---
layout  : wiki
title   : dc 명령어
summary : an arbitrary precision calculator
date    : 2020-08-01 15:32:11 +0900
updated : 2021-06-27 21:02:43 +0900
tag     : bash command calculator
toc     : true
public  : true
parent  : [[cmd]]
latex   : true
---
* TOC
{:toc}

## 출력 명령

- `p`
    - 스택 최상단에 있는 값을 출력하고, 개행 문자를 하나 출력한다.
    - 이 명령은 스택을 변경하지 않는다.
- `n`
    - 스택 최상단에 있는 값을 pop해서 출력한다.
    - pop 하기 때문에 스택 최상단의 값을 버린다.
- `P`
    - 스택 최상단에 있는 값을 pop해서 출력한다.
    - 스택 최상단 값이 string이면 그 값을 출력한다. 마지막에 개행문자는 붙이지 않는다.
    - 스택 최상단 값이 string이 아니면, 숫자로 출력하되 절대값의 정수 부분이 "base(UCHAR_MAX+1)" byte stream으로 출력된다.
- `f`
    - 스택 전체를 출력한다.
    - 이 명령은 스택을 변경하지 않는다.
    - dc를 사용할 때 가장 많이 쓰는 명령.

## 스택 컨트롤

- `c`
    - 스택을 비운다.
- `d`
    - 스택 최상단에 있는 값을 중복시켜 push한다.
    - 예: 스택이 `[3]`일 때 `d`하면 스택은 `[3, 3]`이 된다.
- `r`
    - 스택을 최상단에 있는 2개 값의 순서를 뒤집는다.
    - 스택 전체를 뒤집는 명령이 아니라는 점에 주의.
    - 예: 스택이 `[1, 2, 3]`일 때 `r`하면 스택은 `[1, 3, 2]`가 된다.

## 숫자

숫자를 입력하고 엔터를 치면 스택에 값이 들어간다.

다음은 `1`, `2`, `3`, `f`를 순서대로 입력한 것이다.

```sh
1
2
3
f
3
2
1
```

`f` 입력 후에 보이는 `3`, `2`, `1`은 스택을 위에서부터 출력한 것이다.

즉 `f`를 입력했을 때의 스택을 JSON 배열 형식으로 표현한다면 `[1, 2, 3]`과 같은 상태였다.
(배열 인덱스 0이 스택의 바닥이라고 할 때)

## 연산자

- `+`
    - 스택에서 2개의 값을 pop하고, 더한 다음, 스택에 push 한다.
    - 예: 스택이 `[2, 3]`일 때 `+`하면 스택은 `[5]`가 된다.
    - 예: 스택이 `[7, 2, 3]`일 때 `+`하면 스택은 `[7, 5]`가 된다. (`7`은 연산에 참여하지 않았음)
- `-`
    - 스택에서 2개의 값을 pop하고, 뺀 다음, 스택에 push 한다.
    - 예: 스택이 `[2, 3]`일 때 `-`하면 스택은 `[-1]`이 된다.
    - 예: 스택이 `[3, 2]`일 때 `-`하면 스택은 `[1]`이 된다.
- `*`
    - 스택에서 2개의 값을 pop하고, 곱한 다음, 스택에 push 한다.
    - 예: 스택이 `[2, 3]`일 때 `*`하면 스택은 `[6]`이 된다.
- `/`
    - 스택에서 2개의 값을 pop하고, 나눈 다음, 스택에 push 한다.
    - 예: 스택이 `[2, 3]`일 때 `/`하면 스택은 `[0]`이 된다.
    - 예: 스택이 `[3, 2]`일 때 `/`하면 스택은 `[1]`이 된다.
- `%`
    - 스택에서 2개의 값을 pop하고, 나눈 다음, 스택에 push 한다.
    - 예: 스택이 `[8, 3]`일 때 `%`하면 스택은 `[2]`이 된다.
    - 예: 스택이 `[7, 4]`일 때 `%`하면 스택은 `[3]`이 된다.
- `~`
    - 스택에서 2개의 값을 pop하고, 나눈 다음, 스택에 몫과 나머지를 순서대로 push한다.
    - 예: 스택이 `[20, 3]`일 때 `~`하면 스택은 `[6, 2]`가 된다. ( $$ 3 \times 6 + 2 = 20 $$ )
- `^`
    - 스택에서 2개의 값을 pop하고, 거듭제곱한 다음, 스택에 거듭제곱의 결과를 push한다.
    - 예: 스택이 `[2, 10]`일 때 `^`하면 스택은 `[1024]`가 된다.
    - 예: 스택이 `[10, 2]`일 때 `^`하면 스택은 `[100]`이 된다.
- `|`
    - 스택에서 3개의 값을 pop하고, 지수 모듈러 연산을 한 다음, 스택에 push 한다.
    - 예: 스택이 `[2, 50, 13]`일 때 `|`하면 스택은 `[4]`가 된다.
        - $$ 2^{50} \mod 13 = 4 $$ 이기 때문이다. ( `(2 ** 50) % 13 = 4`)
        - [WolframAlpha 링크]( https://www.wolframalpha.com/input/?i=%7B2%5E50%7D+mod+13 )
        - 위의 예는 스택이 `[1125899906842624, 13]`일 때 `%` 하는 것과 똑같다. 결과 스택은 `[4]`가 된다.
            - ($$ 2^{50} = 1125899906842624 $$)
    - 예: 스택이 `[3, 2, 5]`일 때 `|`하면 스택은 `[4]`가 된다.
        - $$ 3^2 \mod 5 = 4 $$ 이고, `(3**2) % 5 = 4`.
    - 예: 스택이 `[3, 2, 6]`일 때 `|`하면 스택은 `[3]`이 된다.
        - $$ 3^2 \mod 6 = 3 $$ 이고, `(3**2) % 6 = 3`.
- `v`
    - 스택에서 1개의 값을 pop하고, 제곱근을 구한 다음, 스택에 push 한다.
    - 예: 스택이 `[100]`일 때 `v`하면 스택은 `[10]`이 된다.
    - 예: 스택이 `[49]`일 때 `v`하면 스택은 `[7]`이 된다.
    - 예: 스택이 `[1.44]`일 때 `v`하면 스택은 `[1.20]`이 된다.

## 레지스터

dc 명령은 256개의 메모리 레지스터를 제공한다.

레지스터에 값이나 문자열을 저장하고 불러올 수 있다.

각 레지스터는 글자 1개로 이름이 지정된다(Vi/Vim 과 같다).

- `sr`
    - 스택 최상단의 값을 pop 해서 `r`레지스터에 저장한다.
    - 예: 스택이 `[42]`일 때 `sr`하면 스택은 `[]`가 되고, `r` 레지스터에는 `[42]`가 저장되어 있다.
- `lr`
    - `r`레지스터에서 값을 복사해서 스택에 push한다.
    - 복사하는 명령이므로 레지스터의 값은 손상되지 않는다.
    - 예: 스택이 `[42]`일 때 `sr`, `lr`, `lr` 하면 스택은 `[42, 42]`가 되고, `r` 레지스터에는 `[42]`가 저장되어 있다.

그리고 각 레지스터는 자신만의 스택을 갖고 있다. 레지스터의 현재 값은 레지스터 스택의 최상단 값이 된다.

- `Sr`
    - (메인)스택 최상단의 값을 pop 해서 `r`레지스터 스택에 push한다.
        - `r`레지스터 스택에 먼저 들어갔던 값들은 직접적으로 접근할 수 없게 된다.
- `Lr`
    - `r`레지스터 스택 최상단 값을 pop 해서 (메인)스택에 push한다.
    - `r`레지스터 스택 최상단 아래에 있던 값이 `lr`이나 `Lr` 명령으로 접근 가능하게 된다.

## 파라미터 조작

dc는 3가지의 파라미터를 갖는다.

- precision: 실수 정밀도. 분수와 소수 정밀도.
    - `0` 이상이어야 한다.
    - 정밀도는 input radix, output radix와 관계 없이 항상 10진수로 표현된다.
- input radix: 입력 진법. 입력된 숫자를 몇 진법으로 해석할지를 정한다.
    - `2`진법 ~ `16`진법으로 값을 지정해야 한다.
- output radix: 출력 진법. 출력되는 숫자를 몇 진법으로 보여줄지를 정한다.
    - `2`진법 이상의 값을 지정해야 한다.

다음은 이 세 파라미터를 조작하는 명령이다.

- `i`
    - 스택 최상단 값을 pop 해서 input radix로 설정한다.
- `o`
    - 스택 최상단 값을 pop 해서 output radix로 설정한다.
- `k`
    - 스택 최상단 값을 pop 해서 precision으로 설정한다.
- `I`
    - 현재 설정된 input radix를 스택에 푸시한다.
    - 기본 상태에서 `I`를 입력하면 스택은 `[10]`이 된다. 10진법으로 입력 받고 있다는 뜻.
- `O`
    - 현재 설정된 output radix를 스택에 푸시한다.
- `K`
    - 현재 설정된 precision을 스택에 푸시한다.

precision의 기본값은 `0`이다. `2.0 / 3.0`을 계산하면 결과로 `0`이 나온다.

```
2.0
3.0
/
f
0
```

그러나 precision을 `10`으로 설정한다면 `2.0 / 3.0`을 계산하면 결과로 `.6666666666`이 나온다(6이 10개). 

```
10
k
2.0
3.0
/
f
.6666666666
```

## string과 macro

dc의 모든 레지스터와 스택은 숫자 뿐만 아니라 문자열도 집어넣을 수 있다.
dc는 숫자와 문자열 타입을 항상 분명하게 인식한다.

- `[문자열]`
    - `[]` 사이에 있는 문자들을 모아 string을 만들고 스택에 push한다.
    - 예: `[test]`와 같이 입력하면 `"test"` 문자열이 스택에 들어간다.
- `a`
    - 스택 최상단의 값을 pop하고, 타입에 따라 값을 다시 push한다.
        - pop된 값이 숫자라면, 숫자의 low-order byte를 string으로 변환해서 스택에 push한다.
        - pop된 값이 string이면, 해당 string의 첫 글자를 스택에 push한다.
    - 예: 스택이 `[65]`일 때 `a` 하면 스택은 `["A"]`가 된다.
    - 예: 스택이 `[65, 32]`일 때 `+`, `a`하면 스택은 `["a"]`가 된다.
        - 이 방법으로 숫자를 조작해 스택에 문자를 쌓을 수 있다.
- `x`
    - 스택 최상단의 값을 pop하고, 그 값을 매크로 명령으로 실행한다.
        - Vim의 매크로와 비슷하게 쓸 수 있다.
    - pop된 값이 string이면, 매크로로 실행한다.
    - pop된 값이 숫자이면, 다시 스택에 push 한다.
    - 예: 스택이 `["1 2 3 + + f"]`일 때 `x` 하면 `[6]`이 된다.

여기서부터가 재미있는 부분이다.

- `>r`
    - 2개의 숫자 값을 pop한 다음, 두 값을 비교해서 최상단에 있던 값이 더 크다면 `r`레지스터의 매크로를 실행한다.
    - 아래의 예제를 보자.
        - `a` 레지스터에 `"1000 42 *"`을 집어넣고, `if (2 > 1)` 이면 `a`레지스터의 값을 매크로로 실행하는 내용이다.

```
[1000 42 *]
sa
1
2
>a
f
42000
```

- `!>r`
    - `>r`과 반대로 작동한다. 최상단에 있던 값이 작거나 같은 경우에 매크로를 실행한다.
- `<r`
    - 최상단에 있던 값이 작은 경우에 매크로를 실행한다.
- `=r`
    - 두 값이 같은 경우에 매크로를 실행한다.
- `!=r`
    - 두 값이 다른 경우에 매크로를 실행한다.
- `?`
    - 터미널에서 사용자 매크로 명령을 1줄 입력받아 실행한다.
- `q`
    - 매크로를 탈출한다.
    - 최상위 레벨에서 `q`를 직접 호출하면 dc를 종료한다.
- `Q`
    - 스택에서 pop하여, 종료할 매크로 실행 레벨로 사용한다.
    - 즉, `[3]`이 있을 때 `Q`하면 3개의 레벨 매크로를 종료한다. 단 dc를 종료하지는 않는다.

## 상태 조사 명령

- `Z`
    - 스택에서 값을 pop한 다음 숫자라면 자릿수, string이라면 문자의 수를 스택에 push한다.
    - 예: `[123456789]`일 때 `Z` 하면 `[9]`가 된다.
- `X`
    - 스택에서 값을 pop한 다음, 소수점 이하 숫자가 몇 개인지를 스택에 push한다.
    - 예: `[12.5678]`일 때 `X` 하면 `[4]`가 된다.
- `z`
    - 현재 스택의 depth를 스택에 push한다.

## 기타 명령

- `!`
    - `!`뒤의 문자열을 시스템 명령으로 실행한다.
- `#`
    - `#` 뒤의 문자열을 주석으로 인식한다.
- `:r`
    - 스택에서 2개의 값을 pop해서 배열 `r`에 저장한다. 스택 최상단의 값은 배열 인덱스, 최상단 아래에 있었던 값은 저장할 값이 된다.
- `;r`
    - 스택 최상단의 값을 pop하고, 배열 `r`의 인덱스로 사용한다. 선택된 값은 스택에 push된다.

## Examples

dc는 스택 기반의 계산기이기 때문에, 스택에 두 숫자를 push한 다음 연산자 하나를 push하는 방법이 기본적인 사용법이다.

```sh
$ dc -e '2 3 + n'
5
```

- 계산: $$ 2 + 3 $$
- 스택에 `[2, 3]`와 같이 push되었고, `+`가 push되자 스택의 값은 `[2, 3, +]`를 거쳐 `[5]`가 되었다.
    - `n` 명령으로 `5`가 pop 되어 화면에 출력된다.


```sh
$ echo '2 3 + 7 * n' | dc
35
```

- 계산: $$ (2 + 3) \times 7 $$
- 스택에 `[2, 3]`과 같이 push 되었고, `+`로 `[5]`가 된 다음...
    - `7`이 push 되어 `[5, 7]`이 된 상태에서 `*` 해서 `[35]`가 되었다.
    - `n` 명령으로 `35`가 pop 되어 화면에 출력된다.


