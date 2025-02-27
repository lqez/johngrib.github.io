---
layout  : wiki
title   : Base 64 인코딩
summary : 
date    : 2021-09-24 21:58:53 +0900
updated : 2021-09-24 22:39:36 +0900
tag     : encoding
toc     : true
public  : true
parent  : [[algorithm]]
latex   : false
---
* TOC
{:toc}

## Base 64 알파벳 테이블

```
              Table 1: The Base 64 Alphabet

Value Encoding  Value Encoding  Value Encoding  Value Encoding
    0 A            17 R            34 i            51 z
    1 B            18 S            35 j            52 0
    2 C            19 T            36 k            53 1
    3 D            20 U            37 l            54 2
    4 E            21 V            38 m            55 3
    5 F            22 W            39 n            56 4
    6 G            23 X            40 o            57 5
    7 H            24 Y            41 p            58 6
    8 I            25 Z            42 q            59 7
    9 J            26 a            43 r            60 8
   10 K            27 b            44 s            61 9
   11 L            28 c            45 t            62 +
   12 M            29 d            46 u            63 /
   13 N            30 e            47 v
   14 O            31 f            48 w         (pad) =
   15 P            32 g            49 x
   16 Q            33 h            50 y
```

## 변환 알고리즘

Base 64는 문자열을 6비트씩으로 쪼개어 알파벳 테이블에 매치되는 값으로 연속적으로 표현한다.

### 예제: abcd

`abcd`를 Base 64로 인코딩해 보자.

먼저 각 문자의 ASCII 코드를 알아내자.
각 문자의 ASCII 코드는 `xxd` 명령을 사용하면 쉽게 구할 수 있다.

```sh
$ echo -n abcd | xxd -g 1
00000000: 61 62 63 64                                      abcd
```

(사실 ASCII 코드는 암산으로도 쉽게 구할 수 있고, 어차피 필요한 것은 이진수이기 때문에 이 단계에서 굳이 구하지 않아도 된다.)

이제 ASCII 코드를 이진수로 나타내면 된다.


```sh
$ echo -n abcd | xxd -b
00000000: 01100001 01100010 01100011 01100100                    abcd
```

지금까지 얻은 결과를 정리하면 다음과 같다.

| 원문   | `a`        | `b`        | `c`        | `d`        |
| ASCII  | `61`       | `62`       | `63`       | `64`       |
| binary | `01100001` | `01100010` | `01100011` | `01100100` |

이제 이진수를 쭉 연결하면 다음과 같은 모양이 될 것이다.

`01100001011000100110001101100100`

이제 이렇게 쭉 연결한 것을 6비트씩 나눈 다음, 알파벳 테이블에 있는 값을 매핑한다. (매핑 이해를 돕기 위해 중간에 10진수를 넣었다.)

| 6비트   | `011000` | `010110` | `001001` | `100011` | `011001` | `00` `0000` (4비트 빈칸) |
| 10진수  | `24`     | `22`     | `9`      | `35`     | `25`     | `0` (4비트 빈칸)         |
| Base 64 | `Y`      | `W`      | `J`      | `j`      | `Z`      | `A` `==`                 |

결과를 이어붙이면 `YWJjZA`, 그리고 빈 칸 4비트가 남는다. 이렇게 남는 비트에는 패딩을 채우면 된다.
2비트를 각각 `=`로 치환하면 다음과 같은 결과가 나온다.

`YWJjZA==`

결과를 `base64` 명령으로도 확인할 수 있다.

```sh
$ echo -n 'abcd' | base64 
YWJjZA==
```

### 예제: hello

이번에는 `hello`를 Base 64로 인코딩해 보자.

ASCII 코드, 16진수, 2진수로 변환하면 다음과 같다.

| 원문   | `h`        | `e`        | `l`        | `l`        | `o`        |
| ASCII  | `68`       | `65`       | `6c`       | `6c`       | `6f`       |
| binary | `01101000` | `01100101` | `01101100` | `01101100` | `01101111` |

이제 binary를 모두 이어붙인 다음 6비트씩 잘라 구분하자.


| 6비트   | `011010` | `000110` | `010101` | `101100` | `011011` | `000110` | `1111` `00` (2비트 빈칸) |
| 10진수  | `26`     | `6`      | `21`     | `44`     | `27`     | `6`      | `60` (2비트 빈칸)        |
| Base 64 | `a`      | `G`      | `V`      | `s`      | `b`      | `G`      | `8`                      |

결과를 이어붙이면 `aGVsbG8` 이고, 2비트가 빈칸이므로 패딩으로 `=` 하나를 붙여준다.

따라서 인코딩 결과는 `aGVsbG8=` 이다.

```sh
$ echo -n 'hello' | base64
aGVsbG8=
```

## 참고문헌

- [RFC 4648]( https://datatracker.ietf.org/doc/html/rfc4648 )


