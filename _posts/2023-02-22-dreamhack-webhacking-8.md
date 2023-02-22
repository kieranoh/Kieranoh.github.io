---
layout: single
title:  "Background : Non-Relational DBMS"
categories: DreamHack
tag: [DreamHack, WebHacking, Non-Relationa_DBMS,NoSQL,MongoDB,Redis,CouchDB]
toc: true
author_profile: false
---

# Background : Non-Relational DBMS

[Non-Relational DBMS](https://dreamhack.io/lecture/courses/168)
 
RDBMS는 스키마를 정의하고 해당 규격에 맞는 데이터를 2차원 테이블 형태로 저장한다. 이는 복잡할 뿐만 아니라, 저장해야 하는 데이터가 많아지면 용량의 한계에 다다를 수 있다.

이러한 단점을 해결하기 위해 등장한 것이 <U>Non-Relational DBMS</U> *(NRDBMS, NoSQL)* 이다.

관계형 데이터베이스는 SQL Injection 이 발생할 수 있었는데 NoSQL 또한 이러한 문제가 발생 할 수 있다.

## NRDBMS 비관계형 데이터베이스

NoSQL은 SQL를 사용하지 않고 복잡하지 않은 데이터를 저장해 단순 검색 및 추가 검색 작업을 위해 최적화된 저장 공간인 것이 특징이자 차이점이다. 키 - 값 을 사용해 데이터를 저장하는 차이점도 존재한다.

RDBMS는 SQL이라는 정해진 문법을 통해 데이터를 저장하기 때문에 한가지의 언어로 다양한 DBMS을 사용할 수 있다.

하지만 NoSQl은 Redis, Dynamo, CouchDB, MongoDB등 다양한 DBMS가 존재하기 때문에 각각의 구조와 사용 문법을 익혀야하는 단점이 있다.

### MongoDB

MongoDB는 JSON형태인 도큐먼트(Document)를 저장한다.
MongoDB 특징


1. 스키마를 따로 정의하지 않아 각 <U>콜렉션 *(Collection)*</U> 에 대한 정의가 필요 없다.
2. JSON 형식으로 쿼리를 작성할 수 있다.
3. _id 필드가 Primary Key 역할을 한다.

다음은 MongoDB에서 데이터를 삽입하고 조회하는 쿼리의 예시이다.

```
$mongo
>db.user.insert({uid:'admin', upw:'secretpassword'})
WriteResult({"nInserted" : 1})

>db.user.find({uid:'admin'})
{"_id" : ObjectId("5e71d395b050a2511caa827d"), "uid" : "admin", "upw" : "secretpassword" }
```

각 DBMS에서 "status"의 값이 "A"고 "qty"값이 30보다 작은 데이터를 조회하는 쿼리는 다음과 같다

|DBMS|Query|
|---|---|
|RDBMS| SELECT * FROM inventory WHERE status = "A" and qty <30;|
|MongoDB|db.inventory.find({ $and ;[ {status: "A"}, {qty : { $ly:30} } ] } )|

MongoDB의 경우 "$"문자를 통해 연산자를 사용한다.

#### MongoDB 연산자

Comparsion
|Name|Description|
|---|---|
|$eq|equal|
|$in|in|
|$ne|not equal|
|$nin|not in|

Logical
|Name|Description|
|---|---|
|$and|AND|
|$not|NOT|
|$nor|NOR|
|$or|OR|

Element
|Name|Description|
|---|---|
|$exists|지정된 필드가 있는 문서를 찾는다|
|$type|지정된 필드가 지정된 유형인 문서를 선택한다|

Evaluation
|Name|Description|
|---|---|
|$expr|쿼리 언어 내에서 집계 식을 사용할 수 있다|
|$regex|지정된 정규식과 일치하는 문서를 선택한다|
|$text|지정된 텍스트를 검색한다|

#### MongoDB 기본 문법

SELECT


```
Sql

SELECT * FROM account;

MongoDB

db.account.find()

---------------------

Sql

SELECT * FROM account WHERE user_id="admin";

MongoDB

db.account.find({user_id : "admin"})

---------------------

Sql

SELECT user_idx FROM account WHERE user_id="admin";

MongoDB

db.account.find(
{ user_id: "admin" },
{ user_idx:1, _id:0 }
)

```

----
INSERT

```
Sql

INSERT INTO account(
user_id,
user_pw,
) VALUES ("guest", "guest");

MongoDB

db.account.insert({
user_id: "guest",
user_pw: "guest"
})


```

----

DELETE

```
Sql

DELETE FROM account;

MongoDB

db.account.remove()

---------------------

Sql

DELETE FROM account WHERE user_id="guest";

MongoDB

db.account.remove( {user_id: "guest"} )

```

----

UPDATE

```
Sql

UPDATE account SET user_id="guest2" WHERE user_idx=2;

MongoDB

db.account.update(
{user_idx: 2},
{ $set: { user_id: "guest2" } }
)

```


### Redis

Redis는 키 - 값(Key - Value)의 쌍을 가진 데이터를 저장한다. Redis 는 메모리 기반의 DBMS이다.

메모리를 사용해 데이터를 저장하고 접근하기 때문에 읽고 쓰는 작업이 다른 DBMS 보다 빠르다. 다양한 서비스에 임시 데이터를 캐싱하는 용도로 주로 사용한다.

Redis 명령어 공식 문서
https://redis.io/commands

Redis 명령어 사용 예시

```
$ redis-cli
127.0.0.1:6379> SET test 1234 # SET key value
OK

127.0.0.1:6379> GET test # GET key
"1234"
```

#### Redis 명령어

데이터 조회 및 조작 명령어

|명령어|구조|설명|
|---|---|---|
|GET|GET key|데이터 조회|
|MGET|MGET key [ket ...]|여러 데이터를 조회|
|SET|SET key value|새로운 데이터를 추가|
|MSET|MSET key value[key value...]|여러데이터를 추가|
|DEL|DEL key[key...]|데이터 삭제|
|EXISTS|EXISTS key[key...]|데이터 유무 확인|
|INCR|INCR key|데이터 값에 1더함|
|DECR|DECR key|데이터 값에 1뺌|

관리 명령어

|명령어|구조|설명|
|---|---|---|
|INFO|INFO[section]|DBMS 정보 조회|
|CONFIG GET|CONFIG GET parameter|설정 조회|
|CONFIG SET|CONFIG SET parameter value|새로운 설정을 입력|

### CouchDB

CouchDB 또한  MongoDB와 같이 JSON 형태인 도큐먼트(Document)를 저장한다. 

이는 웹 기반의 DBMS로, REST API 형식으로 요청을 처리한다.

HTTP 요청으로 레코드를 업데이하고 조회하는 예시이다.

|메소드|가능 설명|
|---|---|
|POST|새로운 레코드를 추가한다|
|GET|레코드를 조회힌디|
|PUT|레코드를 업데이트힌다|
|DELETE|레코드를 삭제한다|

CouchDB 레코드 업데이트 및 조회 예시
```
$ curl -X PUT http://{username}:{password}@localhost:5984/users/guest -d '{"upw":"guest"}'

{"ok":true,"id":"guest","rev":"1-22a458e50cf189b17d50eeb295231896"}

$ curl http://{username}:{password}@localhost:5984/users/guest

{"_id":"guest","_rev":"1-22a458e50cf189b17d50eeb295231896","upw":"guest"}
```

CouchDB API 공식문서
https://docs.couchdb.org/en/latest/api/index.html