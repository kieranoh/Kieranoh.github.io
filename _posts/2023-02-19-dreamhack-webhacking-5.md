---
layout: single
title:  "ClientSide : CSRF"
categories: DreamHack
tag: [DreamHack, WebHacking,CSRF]
toc: true
author_profile: false
---

# ClientSide : CSRF

[ClientSide : CSRF](https://dreamhack.io/lecture/courses/172)
 
오늘은 <U>교차 사이트 요청 위조</U> *(Cross Site Request Forgery, CSRF)*에 대해 공부해볼꺼다.

## CSRF

CSRF는 임의 이용자의 권한으로 임의 주소 HTTP 요청을 보낼 수 있는 취약점이다.

CSRF 공격에 성공하기 위해서는 공격자가 작성한 악성 스크립트를 이용자가 실행 해야된다.

이는 공격자가 메일을 보내거나 게시판에 글을 작성해 이용자가 이를 조회하도록 유도하는 방법이 있다.

CSRF 공격 스크립트는 HTML 또는 Javascript를 통해 작성이 가능하다.

아래는 CSRF 통해 공격하는 예시이다.

---

송금 기능

```python
@app.route('/sendmoney')
def sendmoney(name):
    to_user=request.args.get('to')

    amount = int(request.args.get('amount'))

```


HTML img 태그 공격

 ```html
<img src='http://h=bank.dreamhack.io/sendmoney?to=dreamhack&amount=1337' width=0px height=0px>

```
Javascript 공격

```javascript
window.open('http://bank.dreamhack.io/sendmoney?to=dreamhack&amount1337');

```

----

## XSS와 CSRF의 차이

공통점

모두 클라이언트를 대상으로 하는 공격이다.

이용자가 스크립트가 포함된 페이지에 접속하도록 유도해야된다.


차이점

서로 다른 목적을 가진다.

XSS

인증 정보인 세션 및 쿠키 탈취

공격할 사이트의 오리진에서 스크립트를 실행시킨다


CSRF

이용자가 임의 페이지에 HTTP요청을 보내기

