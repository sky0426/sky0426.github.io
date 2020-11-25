---
title: "AWS RDS mysql 세팅하기"
date: 2020-11-25 20:16:00 +0900
categories: 서버사이드
tags: ["활자중독", "mysql", "aws", "rds"]
---

AWS RDS에서 MYSQL 생성

#### 데이터베이스 연결
퍼블릭 엑세스 가능 여부 선택 (나중에는 가능 여부를 없애야겠찌..)

보안그룹에서 인바운드 그룹에 일단 모든 접속을 허용해주자. MYSQL/Aurora TCP 3306 0.0.0.0/0

#### 다음으로는 캐릭터셋을 utf8로 바꿔주자
데이터베이스 -> 만든것 -> 구성 -> 파라미터 그룹을 선택
mysql8.0을 만들었더니 기본으로 default.mysql8.0이 만들어져 있다.
그것을 수정하려하니... 안됨.. 기본은 원래 수정이 안된다고 한다.

그래서 새로운 파라미터 그룹을 만든다.
패밀리 mysql8.0으로.. 만든다

***
여기는 utf8로 변경
character_set_client
character_set_connection
character_set_database
character_set_filesystem
character_set_results
character_set_server
***
여기는 utf8_general_ci로 변경해준다.
collation_connection
collation_server
***

DBeaver 설치 후 연결 시도
admin으로 접속 후

#### DB 생성 및 권한
create database 디비이름;
create user '아이디'@'%' identified by '비번';
@뒤에 '%'는 어디서든 접속할 수 있도록 설정, localhost 또는 ip

grant all privileges on 디비이름.* to 아이디@'%';

FLUSH PRIVILEGES;

