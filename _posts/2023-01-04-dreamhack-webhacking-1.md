---
layout: single
title:  "HTTP/HTTPS"
categories: DreamHack
tag: [DreamHack, WebHacking, HTTP/HTTPS]
toc: true
author_profile: false
---

# Background : HTTP/HTTPS

[Web Hacking Background: HTTP/HTTPS](https://dreamhack.io/lecture/courses/199)

웹서버에서  클라이언트는 요청 ( Request ), 서버는 행위를 응답( Response )한다 .

프로토콜( Protocol ) 이란 이와같은 규결화된 상호작용에 적용되는 약속이다.


## HTTP

HTTP( Hyper Text Transfer Protocol )란 서버와 클라이언트의 데이터 교환을 <U>Request 와 Response</U> 형식으로 정의한 프로토콜이다.

HTTP의 기본 메커니즘은 클라이언트가 서버에세 요청하면, 서버가 응답하는 것이다. 웹서버는 HTTP 서버를 HTTP서비스 포트에 대기시킨다.( 이 포트는 일반적으로 TCP/80 또는 TCP/8080이다. ) 

클라이언트가 서비스포트에 HTTP를 요청하면, 이를 해석하여 적절한 응답을 받는다.

서비스 포트 ( Service Port )는 네트웨크 포트중 특정 서비스가 점유하고 있는 포트다. 포트로 데이터를 교환하는 방식은 전송계층 ( Transport Layer )의 프로토콜을 따른다. 대표적으로 TCP 와 UDP가 있다. 

TCP로 데이터 전송하려는 서비스에 UDP 클라이언트가 접근하면 데이터는 교환되지 않는다. 반대의 경우도 마찬가지이다. 이러한 이유로 서비스 포트를 표시할 때 서비스가 사용하는 전송 계층 프로토콜을 같이 표기하기도 한다

ex)

* HTTP의 서비스 포트가 TCP/80 이면 80번 포트에서 TCP로 제공한다.


### HTTP 메세지

![HTTPMessage](/images/HTTPmessage.png)

HTTP는 기본적으로 헤드와 바디로 구성되어 있다.

* HTTP 헤드

HTTP 헤드의 각줄은 CRLF로 구분된다. 첫 줄은 <U>시작 줄 ( Start-line )</U>, 나머지 줄은 <U>헤더( Header )</U>라고 부른다. 헤드의 끝은 CRLF 한줄로 나타난다.

( CRLF 란 CR + LF, CR == \r , LF == \n, 다음줄을 의미)

헤더는 *필드* 와 *값* 으로 구성되며 HTTP 메세지 또는 바디의 속성을 나타낸다. 하나의 HTTP 메세지에는 0개 이상의 해더가 있을 수 있다.

* HTTP 바디

HTTP바디는 헤드의 끝을 나타내는 CRLF 뒤, 모든 줄이다. 클라이언트나 서버에게 전송하려는 데이터가 바디에 포함된다.


#### HTTP 요청

HTTP 요청( Request )은 서버에게 특정 동작을 요구하는 메시지이다. 서버는 동작이 실현 가능한지, 클라이언트가 권한이 있는지 등을 검토하고, 적절할 때만 이를 처리한다.

* 시작 줄
  
HTTP 요청의 시작 줄은 <U>메소드 ( Method )</U>, <U>요청 URL ( Request-URL )</U>, <U>HTTP 버전</U>으로 구성되고 각각은 띄어쓰기로 구분한다.

메소드는 서버가 수행하길 바라는 동장을 나타낸다. HTTP 표준에 정의된 메소드는 8개가 있다.그중 자주 사용되는건 GET, POST다.


GET은 리소스를 가져오라는 메소드다. 이용자가 웹서버의 주소를 입력하면, 새로운 페이지를 렌터링하기 위해 리소스가 필요하는데, 이때 GET요청을 서버에 전송해서 리소스를 받아온다.

POST는 반대로 데이터를 보내는 메소드다. 전송할 데이터는 HTTP 바디에 포함된다. 로그인할 때 ID 와 비밀번호, 게시물 등이 POST로 서버에 보내진다.

요청 URL은 메소드의 대상을, HTTP 버전은 클라이언트가 사용하는 HTTP 프로토콜의 버전을 나타낸다.

#### HTTP 요청

HTTP 응답은 HTTP 요청에 대한 결과를 반환하는 메시지이다. 요청을 수행했는지, 하지 않았는지, 안 했다면 이유는 무엇인지와 같은 상태 정보 ( Status ), 그리고 클라이언트에게 전송할 리소스가 응답에 포함된다. 

* 시작 줄

HTTP 응답의 시작 줄은 <U>HTTP 버전</U>, <U>상태 코드 ( Status Code )</U>, <U>처리 사유( Reason Phrase )</U>으로 구성되고 각각은 띄어쓰기로 구분한다.

HTTP 버전은 서버에서 사용하는 HTTP 프로토콜의 버전을 나타낸다.

상태 코드는 요청에 대한 처리 결과를 세 자릴수로 나타낸다. 이들은 첫번째 자릿수에 따라 5개의 클래스로 분류된다.

|상태 코드|설명|대표 예시|
|---|---|---|
|1xx|요청을 제대로 받았고, 처리가 진행중임||
|2xx|요청이 제대로 처리됨|200:성공|
|3xx|요청을 처리하려면, 클라이언트가 추가 동작을 취해야 함.|302: 다른 URL로 갈 것|
|4xx|클라이언트가 잘못된 요청을 보내어 처리에 실패했습니다|400:요청이 문법에 맞지 않음<br>403:클라이언트가 리소스레 요청 할 권한이 없음<br>404:리소스가 없음|
|5xx|클라이언트의 요청은 유효하지만, 서버에 에러가 발생하여 처리에 클패했습니다|500:요청을 처리하다가 에러가 발생함<br>503:서버가 과부하로 인해 요청을 처리할 수 없음|

HTTP 요청 사용해 보기

[HTTP TEST TOOl](https://learn.dreamhack.io/199#9)


## HTTPS

HTTP의 응답과 요청은 평문으로 전달되어 중단에 다른사람이 가로챈다면 중요한 정보가 유출될 수 있다.

HTTPS( HTTP over Secure socket layer ) 는 TLS( Transport Layer Security ) 프로토콜은 도입하여 문제점을 해결했다. TLS는 서버와 클라이언트 사이에 오가는 모든 HTTP메시지를 암호화한다.





