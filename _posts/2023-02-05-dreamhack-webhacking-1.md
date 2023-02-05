---
layout: single
title:  "Cookie & Session"
categories: DreamHack
tag: [DreamHack, WebHacking, Cokkie, Session]
toc: true
author_profile: false
---

# Cokkie & Session

[Web Hacking Background: Cookie & Session](https://dreamhack.io/lecture/courses/166)

웹 서버는 어떻게 수많은 클라이언트를 구별할까? 라는 질문에서부터 이번 내용이 시작된다. 오늘은 클라이언트의 인증 정보를 포함하고 있는 Cookie 와 Session에 대해 알아본다. 


## Cokkie

클라이언트의 IP주소와 User-Agent (소프트웨어 식별정보)는 매번 변경될 수 있는 고유하지 않은 정보일 뿐만 아니라, HTTP프로토콜의 특징 (connectionless, stateless)때문에 클라이언트를 기억 할 수 없다. 

이러한 특성때문에 쿠키(Cokkie)가 만들어 졌다. <u>쿠키란 Key 와 Value로 이루워진 일종의 단위</U>로 서버가 클라이언트한테 쿠키를 발급하면, 클라이언트는 서버가 쿠키를 요청할때마다 같이 전송한다.

다음 그림은 쿠키가 없을때와 있을 때의 예시이다.


![no_cookie](/images/nocookie.png)

![yes_cookie](/images/yescookie.png)

쿠키는 서버가 클라이언트에게 발급해주는 값이기 때문에 만약 서버가 별다른 검증 없이 쿠키를 확인한다면, 클라이언트가 값을 마음대로 바꾸어 아래의 상황이 일어날 수 있다.

![faker](/images/fakecookie.png)

## Session

클라이언트가 쿠키를 변조할 수 있기에 정보를 변경 할 수 없게 세션( Session )을 사용한다. 세션은 인증 정보를 서버에 저장하고 해당 데이터에 접근할 수 있는 키(<U>유추할 수 없는 랜덤한 문자열</u>) 를 만들어 전달한다. 해당 키를 일반적으로 Session ID라고 부른다.

![Session](/images/session.png)

쿠키는 데이터 자체를 이용자가 저장하지만, 세션은 서버가 저장한다는 특징이 있다.

