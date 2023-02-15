---
layout: single
title:  "Mitigation: Same Origin Policy"
categories: DreamHack
tag: [DreamHack, WebHacking, SOP]
toc: true
author_profile: false
---

# Mitigation : Same Origin Policy

[Web Hacking Mitigation : Same Origin Policy](https://dreamhack.io/lecture/courses/186)

이번 강의는 쿠키로 인해 브라우저에서 발생 될 수 있는 문제들을 방지하기 위해 만들어진 <U>동일 출처 정책 </U>  *Same Origin Policy (SOP)* 를 배울 예정이다.


## Same origin Policy (SOP)

브라우저는 인증 정보로 사용될 수 있는 쿠키를 브라우저 내부에 보관한다. 사용자가 웹 서비스에 접속할 때, 부라우저는 해당 웹 서비스에서 사용하는 인증 정보인 쿠키를 HTTP요청에 포함시켜 보낸다. 

브라우저는 웹 리소스 간접적으로 타 사이트에 접근할 때도 인증정보인 쿠키를 함께 전송하는 특징을 가지고 있다.

이러한 특징 때문에 악의적인 페이지가 클라이언트 권한을 이용해 대상 사이트에 HTTP요청을 보내고 응답정보를 획득하는 코드를 실행 할 수 있다. 

클라이언트 입장에서는 가져온 데이터를 악의적인 페이지에서 읽을 수 없도록 해야한다. 이것이 브라우저의 보안 메커니즘인 <U>동일 출처 정책</U> *Same Origin Policy (SOP)* 이다.

### Origin의 구별법

브라우저가 가져온 정보의 출처인 오리진 (Origin)을 구별할때는 *프로토콜 (Protocol, Scheme)* , *포트(Port)*, *호스트(Host)* 로 구별한다. 이러한 구성요소들이 전부다 일치해야 동일한 오리진이라고 한다.

```
http://same-origin.com/
```

라는 오리진과 아래 URL을 비교하면

|URL|결과|이유|
|---|---|---|
|https://same-origin.com/frame.html| Same Origin| Path만 다름|
|<U>http</U>://same-origin.com/frame.html| Cross Origin| Sheme이 다름|
|https://<U>cross.same-origin.com</U>/frame.html| Cross Origin| Host가 다름|
|https://same-origin.com:1234| Cross Origin| Port가 다름|


SOP는 Cross origin이 아닌 Same Origin일 때만 정보를 읽을 수 있도록 해준다. 


## Cross Origin Resourse Sharing(CORS)

이미지나 자바스크립트, CSS등의 리소스를 불러오는 \<img> ,\<sytle>, \<script> 등의 태그는 SOP의 영향을 받지 않는다.

이러한 경우 외에도 웹 서비스에서 동인한 출처 정책인 SOP를 완화하여 다른 출처의 데이터를 처리해야하는 경우도 있다. 예를 들면 사이트가 카페, 블로그, 메일 서비스를 아래 주소로 운영하고 있다고 하면, 각 사이트 마다 Host가 다르기에 오리진이 다르다고 인식한다.

* 카페 : https://cafe.dreamhack.io
* 블로그 : https://blod.dreamhack.io
* 메일 : https://mail.dreamhack.io
* 메인 : https://dreamhack.io

이러한 환경에서 사용자가 수신한 메일의 갯수를 메인 페이지에  출력하려면, 개발자들은 메인페이지에서 메일서비스에 관련된 리소스를 요청해야한다. 이때 두 사이트는 오리진이 다르므로 SOP를 적용받지 않고 리소스를 공유 할 방법이 필요하다.

이런 상황에서 자원을 공유하기 위해 사용할 수 있는 공유 방법을 <U> 교차 공유 리소스 공유</U> *( Cross Origin Resource Sharing, CORS)* 라고 한다. HTTP헤더를 추가하여 전송 혹은 JSONP 방법을 사용한다.

