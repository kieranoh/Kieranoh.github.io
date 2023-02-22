---
layout: single
title:  "ServerSide : Command Injection"
categories: DreamHack
tag: [DreamHack, WebHacking, Command, Injection]
toc: true
author_profile: false
---

# ServerSide : Command Injection

웹 애플리케이션을 개발하다보면, 특정 기능을 스스로 코드를 작성하기보다 이미 설치된 함수, Command 를 사용하기도 한다.

함수의 인자를 셀의 명령어로 전달한다는 점에서 치명적인 취약점이 만들어진다.

## Command Injection

Command Injection은 명령어를 실행하는 함수에 이용자가 임의의 인자를 전달할 수 있을 때 발생한다. 

예를들어 파이썬으로 개발된 웹 애플리케이션에서 IP 에 ping 을 전송하고 싶으면 

"os.system("ping [user-input]")"를 입력하면 된다.

이러한 함수를 사용할 때 이용자의 입력을 제대로 검사하지 않으면 임의 명령어가 실행될 수도 있다. 이는 리눅스 셸 프로그램이 지원하는 메타 문자 때문이다.

| 메타문자 | 설명 | Example|
|---|---|---|
|' '| 명령어 치환  ' '안에 들어있는 명령어를 실행한 결과로 치환한다 |  $ echo `'echo theori`'  >>theori|
| $( ) | 명령어 치환 $ ( ) 안에 있는 명령어를 실행한 결과로 치환한다. 중복 사용 가능 | $ echo $(echo theori)  >>theori|
| && | 명령어 연속 실행 한줄에 여러 명령어를 실행한다.  (앞에 오류가 나면 뒤 명령어 실행 X)| $ echo hello && echo theori  >>hello  theori |
| &#124; &#124; | 명령어 연속 실행 한줄에 여러 명령어를 실행한다.  (앞에 오류가 나도 뒤 명령어 실행 )| $ echo hello  &#124; &#124; echo theori  >>hello  theori|
| ; | 명령어 구분자 한줄에 여러 명령어를 사용할때 구분을 도와준다 (앞에 오류가 나도 뒤 명령어 실행 ) |  echo hello ; echo theori  >>>hello  theori |
| &#124; | 파이프 앞 명령어의 결과가 뒷 명령어의 입력으로 들어간다 |  $ echo id &#124;  /bin/shuid=1001(theori) gid=100  >>(theori) groups=1001(theori)|

