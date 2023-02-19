---
layout: single
title:  "Background : Relational DBMS"
categories: DreamHack
tag: [DreamHack, WebHacking,DBMS]
toc: true
author_profile: false
---

# Background : Relational DBMS

[Relational DBMS](https://dreamhack.io/lecture/courses/169)
 
컴퓨터는 정보를 기록하기 위해 <U>데이터베이스</U> *(Database)* 를 사용한다. 데이터베이스들을 관리하는 애플리케이션을 <U>DataBase Management System *(DBMS)*</u>이라고 한다

## DataBase Management System

DBMS는 데이터베이스에 새로운 정보를 기록하거나, 기록된 내용을 수정, 삭제하는 역할을 한다.

DBMS는 다수의 사람이 동시ㅣ에 데이터베이스에 접근할 수 있고, 웹 서비스의 검색 기능과 같이 복잡한 요구사항을 만족하는 데이터를 조회할 수 있다.

DBMS는 크게  관계형과 비관계형을 기준으로 분류하며 다양한 종류의 DBMS가 존재한다.

관계형은 행과 열의 집합인 테이블 형식으로 데이터를 제공한다. 비관계형은 테이블 형식이 아닌 키-값 (Key-Value)형태로 저장한다.

|종류|대표적인 DBMS|
|---|---|
|Relatoinal  (관계형)|MySQL, MariaDB, PostgreSQL, SQLite|
|Non-Relational  (비관계형)|MongoDB, CouchDB, Redis|

### Relational DBMS

Relational DataBase Management System (RDBMS, 관계형 RDBMS)는 Codds가 12가지 규칙을 정의하여 생산한 데이터베이스 모델이다.

RDBMS는 행(Row)과 열(Column)의 집합으로 구성된 테이블 형식으로 데이터를 관리하고, 테이블 형식의 데이터를 조작할 수 있는 관계 연산자를 제공한다. 

Codds는 12가지 규칙을 정의 했지만 RDBMS들은 12가지 규칙을 모두 따르지 않았고, 최소한의 조건으로 앞의 두 조건을 만족하는 DBMS를 RDBMS라고 부르게 되었다.

RDBMS 에서 관계연산자는 Structured Query Language (SQL)라는 쿼리 언어를 사용하고, 쿼리를 통해 테이블 형식의 데이터를 조작한다.

#### SQL

Structured Query Language (SQL)는 RDBMS의 데이터를 정의하고 질의, 수정 등을 하기 위해 고안된 언어이다. SQL은 구조화된 형태를 가지는 언어로 웹 어플리케이션이 DBMS와 상호작용할 때 사용된다.

SQL은 사용 목적과 행위에 따라 다양한 구조가 존재한다.

|언어|설명|
|---|---|
|DDL (Data Definition Language)| 데이터를 정의하기 위한 언어이다. 생성/수정/삭제 등의 행위를 수행한다.|
|DML (Data Manipulation Language)|데이터를 조작하기 위한 언어이다. 조회/저장/수정/삭제등을 수행한다.|
|DCL (Data Control Language)|대이터베이스의 접근권한 등의 설정을 하기위한 언어이다.|

RDBMS에 사용하는 기본적인 구조는 데이터베이스 -> 테이블 -> 데이터 구조이다. 데이터를 다루기 위해 데이터베이스와 테이블을 생성해야 하며, DDL을 사용해야 한다.

다음은 Dreamhack이라는 데이터베이스를 생선하는 쿼리문이다.

----

```sql
CREATE DATABASE Dreamhack;
```

테이블 생성

```SQL
USE Dreamhack;

CREATE TABLE Board(
    idx INT AUTO_INCREMENT,
    boardTitle VARCHAR(100) NOT NULL, 
    boardContent VARCHAR(2000)NOT NULL,
    PRIMARY KEY(idx)
)
```

----

생선된 테이블에 데이터를 추가하기 위해 DML을 사용한다.

다음은 새로운 데이터를 생선하는 예시이다. 



```SQL
INSERT INTO

    Board(boardTitleboardContent, createDate)

Values(
    'Hello',
    'World !',
    Now()
);
```

----

Board 테이블을 조회하는 쿼리문

```SQL
SELECT
    boardTitle, boardContent
FROM
    Board
Where
    idx=1;
```

----
Board 테이블의 컬럼 값을 변경하는 쿼리문

```SQL
UPDATE Board SET boardContent='DreamHack!'
    Where idx=1;
```

----