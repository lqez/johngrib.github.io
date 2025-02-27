---
layout  : wiki
title   : vim-rest-console 사용법
summary : vim을 cURL 클라이언트로 사용하자
date    : 2018-04-12 21:41:12 +0900
updated : 2022-06-18 10:34:20 +0900
tag     : vim http
toc     : true
public  : true
parent  : [[/vim]]
latex   : false
---
* TOC
{:toc}

## 개요

* HTTP 메시지를 보내고 받을 수 있다.
* HTTP raw 포맷과 비슷하게 각 요청을 만들 수 있다는 장점이 있다.

포스트맨 같은 API 클라이언트로 사용할 수도 있지만, 텍스트 파일로 관리하기 때문에 git 과의 궁합이 좋다. rest 파일을 잘 작성하면 자체로 개발에 도움이 되는 문서나 API 문서의 역할도 할 수 있다.

## 설치 방법

* VimPlug

```viml
Plug 'diepm/vim-rest-console'
```

## 간단한 사용 방법

확장명이 `rest`인 파일을 만들고 Vim에서 열어주면 된다.

파일의 내용엔 다음과 같이 HTTP 리퀘스트 메시지를 작성해주면 된다.


```
## 공통으로 사용할 header 를 다음과 같이 작성해준다
Content-Type: application/json; charset=utf-8
Authorization: XXXX XXXX-XXXX
--

## GET 요청을 보낸다
https://httpbin.org/
GET /ip

## 헤더를 개별 정의하려면 URI 아래에 두면 된다.
## POST 요청을 보낸다
https://httpbin.org/
Content-Type: application/json; charset=utf-8
Authorization: XXXX XXXX-XXXX
POST /post
{
    "test" : "1234"
}

## GET, POST 는 물론이고 모든 HTTP 메소드를 사용할 수 있다.
https://httpbin.org/
PUT /put
{
    "test": "1234"
}
```

* 커서를 각 항목 위에 놓고 `<C-j>`를 입력하면, 해당 문단에 작성해 둔 메시지로 리퀘스트를 보낸다.
* 리스폰스를 받으면 오른쪽에 `vs`를 열고 보여준다.

## 설정

### 트리거 키 변경

다음과 같이 변경해주면 된다.

```viml
let g:vrc_trigger = '<C-k>'
```

### curl 옵션 설정

다음과 같이 curl에 기본으로 제공할 옵션을 정의할 수 있다.

```viml
let g:vrc_curl_opts = {
            \ '-s': '',
            \ '-D -': '',
            \}
```

### 실제로 실행하는 curl 명령어 함께 보기

다음 옵션을 `1`로 설정해주면 리퀘스트를 보낼 때마다 실제 실행하는 `curl` 명령어와 그 옵션들이 화면에 나타난다.

```viml
let g:vrc_show_command = 1
```

curl을 잘 쓰고 싶은 사람에게는 최고의 옵션이다.

### response 결과 포매팅

```viml
let s:vrc_auto_format_response_patterns = {
            \   'json': 'jq',
            \}
```

### json 결과 출력에 formatting이 안 되는 문제 해결

vim-rest-console은 결과 출력의 포매팅을 위해 다음과 같은 옵션을 디폴트로 제공하고 있다.

```viml
let s:vrc_auto_format_response_patterns = {
  \ 'json': 'python -m json.tool',
  \ 'xml': 'xmllint --format -',
\}
```

하지만 막상 실행해 보면 다음과 같이 표기되며, 포매팅이 안 되는 경우가 있다.

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0100   129  100   129    0     0    146      0 --:--:-- --:--:-- --:--:--   146
{"headers":{"Accept":"*/*","Content-Type":"application/json","Host":"nghttp2.org","User-Agent":"curl/7.54.0","Via":"2 nghttpx"}}
```

원인은 심플하다. curl 수행 보고 테이블이 위에 출력되기 때문에 `python -m json.tool`이 통하지 않는 것이다.

이 문제를 해결하려면 다음과 같이 vrc가 리퀘스트를 보낼 때 `curl`의`-s` 옵션(silence)을 사용하도록 설정해주면 된다.

```viml
let g:vrc_curl_opts = {
  \ '-s': '',
\}
```

이렇게 수정한 다음, 다시 실행해 보면 다음과 같이 포매팅이 완료된 결과가 나온다.

```json
{
    "headers": {
        "Accept": "*/*",
        "Content-Type": "application/json",
        "Host": "nghttp2.org",
        "User-Agent": "curl/7.54.0",
        "Via": "2 nghttpx"
    }
}
```

## 내가 사용하고 있는 설정

```viml
" http 응답 헤더를 함께 보여준다
let g:vrc_include_response_header = 1
" 기본 응답 타입은 json 이다
let g:vrc_response_default_content_type = 'application/json'
" 같은 결과를 얻을 수 있는 curl 명령어를 보여준다
let g:vrc_show_command = 1

" curl 명령 실행 결과 나오는 메타데이터는 생략한다
let g:vrc_curl_opts = { '-s': '' }
" 디버그 모드는 끈다
let g:vrc_debug = 0
```

## Links

* [vim rest console](https://github.com/diepm/vim-rest-console )

