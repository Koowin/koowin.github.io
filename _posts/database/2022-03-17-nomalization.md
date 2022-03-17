---
title:  "정규화"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - database

date: 2022-03-17
last_modified_at: 2022-03-17
---

# 이상현상

잘못 설계된 데이터베이스에서 발생하는 현상.
삽입 시 NULL 값이 입력되거나 삭제 시 연쇄삭제 현상이 일어나거나, 수정 시 데이터의 일관성이 훼손되는 현상.

<br><br>

# 함수 종속성

어떤 속성 A의 값을 알면 다른 속성 B의 값이 유일하게 정해지는 의존 관계를 '속성 B는 속성 A에 종속한다' 혹은 '속성 A는 속성 B를 결정한다'라고 한다.

종속관계에 있는 예

* 학생번호 -> 학생이름
* 학생번호 -> 주소
* 강좌이름 -> 강의실
* 학과 -> 학과사무실

종속하지 않는 예

* 학생이름 - 강좌이름
* 학과 - 학생번호

<br><br>

# 정규화

정규화(normalization)란, 이상현상이 발생하는 테이블을 수정하여 정상으로 만드는 과정.

<br>

## 정규화 과정

### 제 1 정규형

릴레이션 R의 모든 속성 값이 원자값을 가지면 제 1 정규형이라고 한다.
A relation in which the intersection of each row and column contains one and only one value.
<br>

### 제 2 정규형

릴레이션 R이 제 1 정규형이고 기본키가 아닌 속성이 기본키에 완전한 함수 종속일 때 제 2 정규형이라고 한다.
A relation that is in first normal form and every non-primary key attribute is fully functionally dependent on the primary key.
<br>

### 제 3 정규형

릴레이션 R이 제 2 정규형이고 기본키가 아닌 속성들이 기본키에 비이행적으로 종속할 때(직접 종속) 제 3 정규형이라고 한다. 이행적 종속이란 A -> B, B -> C가 성립할 때 A -> C가 성립되는 함수 종속성을 말한다.
A relation that is in first and second normal form and in which no non-primary key is transitively dependent on the primary key.

e.g.

* before: 계절학기(학생번호, 강좌이름, 수강료)
* after: 계절학기(학생번호, 강좌이름), 수강료(강좌이름, 수강료)

즉, before 에서는 '수강료' 속성이 기본키인 '학생번호' 에 종속하지 않고 '강좌이름' 에 종속하고 있었다.

<br><br>

# 출처

* MySQL로 배우는 데이터베이스 개론과 실습
