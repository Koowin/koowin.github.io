---
title:  "웹 보안 교육"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - uncategorized

date: 2022-02-08
last_modified_at: 2022-02-08
---

# 개요

 혼자 공부하기 위해 정리한 글입니다. 제가 이미 알고 있는 것은 생략하여 다른 독자를 고려하지 않았습니다. 양해 부탁드립니다.

## 웹 보안 이슈

OWASP - 정기적으로 웹 취약점을 조사해서 10개씩 발표하는 비영리 기구. 웹 보안과 관련된 트렌드를 알 수 있다.

* SQL 인젝션
* 스크립트 공격 (XSS, CSRF, SSRF)
* SSL/TSL
* Web Server 설정 문제 (Apache, IIS, Nginx)
* Client Side 문제 (쿠키, 세션)
* Compliance(규제) (개인정보보호법, GDPR, GS인증 등등)
* 검색엔진들이 지나치게 정보를 많이 가져감 (일반 사용자의 요청과는 다르게 웹서버들이 부하를 많이 받음)

<br/><br/>

# SQL 인젝션

## 주석 이용하기

Oracle, MS SQL :   --

MySQL, MariaDB :   #

<br/>

## 다중문 작성 예시

SELECT id, pw FROM member WHERE id='<span style="color:red">'; UPDATE ~~~ #</span>' and pw='       ';'

<br/><br/>

# DVMA

DVMA: Damn Vulnerable Web Application 의 약자.

웹 공격을 실습해 볼 수 있는 웹 서버. 다른 PC나 VMware에 설치하여 실습해보면 된다.

Security Level 을 설정하여 단계별로 실습해볼 수 있다. 처음에는 쉽게 설정해놓고 성공한다면 점차 Security Level을 높여서 연습해볼 수 있다. 단계: Low, Midium, High, Impossible

<br/><br/>

# SQL Injection

## Level: Low

![image-20220208111201009](../../assets/images/2022-02-08-web-secure/image-20220208111201009.png)

User ID에 자연수를 입력하여 Submit을 누르면 해당 사용자의 정보가 출력되는 간단한 페이지.

### 예상하는 sql 구문

SELECT * FROM ?? WHERE id = '';

### 공격 구문

#### 특수문자를 허용하는 경우

* SELECT * FROM ?? WHERE id = '<span style="color:red">' or 1=1 #</span>';
* SELECT * FROM ?? WHERE id = '<span style="color:red">' or 2>1 #</span>';
* SELECT * FROM ?? WHERE id = '<span style="color:red">' or 1 #</span>';

#### 입력란에 '#'을 허용하지 않는 경우

* SELECT * FROM ?? WHERE id = '<span style="color:red">' or 'a'='a</span>'; 

#### 입력란에 '='와 '#'을 허용하지 않는 경우

* SELECT * FROM ?? WHERE id = '<span style="color:red">' or 's'<'t</span>'; 



### Secure Coding 함수

SQL Injection 공격을 다 막기 위해서는 #, =, <, >, ', " 등을 모두 막아야한다.

공격 방어를 쉽게 해주는 것이 Secure Coding 함수. DBMS 에서 제공.

<span style="color:skyblue">e.g.</span> mysqli_real_escape_string()

<br/><br/>

# SQL Injection (Blind)

물어보거나 에러를 유발시켜서 DB명, Table명, Column명을 알아내어 새로운 SQL문을 만들어내는 것.

### 1단계) DB 정보 알아내기

<span style="color:orange">database()</span> : DB명 조회 함수

<span style="color:orange">version()</span> : 버전 확인

<span style="color:orange">user()</span> : 사용자 이름

<span style="color:orange">@@version</span> : 버전 확인

<br/>

### 2단계) Table명 알아내기

information_schema라는 DB에 저장되어 있음.

' UNION SELECT table_name, null FROM information_schema.tables WHERE table_schema='dvwa' #

<br/>

### 3단계) Column명 알아내기

' union select column_name, null from information_schema.columns WHERE table_name='users' #

<br/>

### 4단계) 원하는 정보 알아내기

' union select user, password from users #

![image-20220208134107362](../../assets/images/2022-02-08-web-secure/image-20220208134107362.png)

Hash Algorihtm을 어떤 것을 사용하였을까?

문자열 개수 32개, 16진수로 표현되었으니 32 * 16 = 128bit

128bits 결과가 나오는 알고리즘은 MD5임. Hash Algorithm을 알게된다면 레인보우 테이블을 이용하여 쉽게 암호 유추가 가능함. (MD5(128bit), SHA1(160bit) 등은 안정성에 문제가 있음)

e.g. admin의 암호

![image-20220208134656395](../../assets/images/2022-02-08-web-secure/image-20220208134656395.png)

안전하게 비밀번호 저장하기 : 안정성이 높은 Hash 알고리즘(SHA-2(256bit) 이상) 사용 및 Salt 사용

<br/>

## Salt란?

사용자마다 서로 다른 랜덤 값을 부여한 것을 Salt라고 한다. 사용자의 비밀번호를 저장할 때 사용자가 입력한 비밀번호에 해당 Salt를 더해 Hash하여 저장한다. Salt를 사용함으로써 얻는 장점은 첫 번째로 레인보우 테이블을 이용한 공격을 방어할 수 있고, 두 번째로 같은 암호를 사용하는 서로 다른 두 사용자의 Hash값이 달라지기 때문에 한 명의 암호를 알게 되어도 같은 해시 값을 가지는 다른 사람의 암호를 알기 어렵게 한다.

<br/><br/>

# Broken Authentication

## 인증의 종류

1) 지식 기반

   e.g. 비밀번호, 암구어, 미리 정해놓은 질의 응답, 패턴

2) 소유 기반

   e.g. 열쇠, Key Pair, OTP, 공동인증서, 신용카드 휴대폰인증

3) 생체 기반

   e.g. 지문, 얼굴, 홍채 등

4) 위치 기반

   e.g. GPS, 툥신사 기지국 기반, IP주소(Wi-Fi) 등등

안전한 인증이란?

MFA(Multi-Factor Authentication) : 다양한 종류를 활용한 인증방법

e.g. 휴대폰 은행 앱 (휴대폰 + 지문 + 비밀번호) = 소유 + 생체 + 지식

<br/>

## Cookie vs Session

| Cookies                                                      | Session                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 사용자의 웹 브라우저에 저장됨                                | 서버에 저장됨                                                |
| 사용자가 지우거나 타이머에 의해 설정된 시점까지 사용자의 브라우저 안에서 정보를 유지할 수 있다. | 브라우저가 열러있는 동안에 사용 가능하다. 사용자는 세션을 임의로 중단시킬 수 없고, 브라우저를 닫으면 세션은 없어질 것이다. |
| 스트링으로만 저장됨                                          | 오브젝트 형태로 저장 가능                                    |
| 나중에 참조하기 위해 쿠키를 저장할 수 있다.                  | 나중에 재사용하기 위해 저장할 수 없다.                       |
| 사용자에 의해 조작 가능                                      | 사용자가 세션 조작 불가능                                    |
| 보안 측면에서 비교적 안전하지 않음                           | 보안 측면에서 비교적 안전함                                  |

<br/><br/>

# XSS

XSS(Cross Site Scripting): 악의적인 스크립트를 웹서버에 업로드 하고, 그 웹서버에 방문한 Web Browser를 공격하는 기법

## DVMA XSS 실습

![image-20220208162955077](../../assets/images/2022-02-08-web-secure/image-20220208162955077.png)

해당 칸에 script를 넣어서 실행되는지 실습해보는 연습 예제이다.

<br/>

## DVMA (Level.Low)

`<script>alert('test')</script>`

보안 수준이 가장 낮은 상태로 설정되었을 때는 스크립트를 넣으면 다음과 같이 알람 창이 활성화된다.

![image-20220208163402306](../../assets/images/2022-02-08-web-secure/image-20220208163402306.png)

<br/>

## DVMA (Level.Medium)

Level.Low 에서 입력하였던 스크립트를 그대로 입력하면 잘 실해오디지 않는다. 연습 페이지의 우측하단 소스 보기를 클릭하면 다음과 같은 소스를 볼 수 있다.

```php
<?php

// Is there any input?
if( array_key_exists( "name", $_GET ) && $_GET[ 'name' ] != NULL ) {
    // Get input
    $name = str_replace( '<script>', '', $_GET[ 'name' ] );

    // Feedback for end user
    echo "<pre>Hello ${name}</pre>";
}

?>
```

단순히 `<script>`라는 문자열을 빈 문자열로 바꿔준다.

따라서 다음과 같이 script에 대문자가 포함된 스크립트를 넣으면 된다.

`<ScRiPt>alert('test')</script>`

<br/>

## DVMA (Level.High)

<br/>
