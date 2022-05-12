---
title:  "Regular Expressions"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - java

date: 2022-01-02
last_modified_at: 2022-01-18
sitemap:
  changefreq: daily
  priority: 1.0
---

# 개요

<details>
<summary><span style="color:LightSkyBlue">동기 접기/펼치기</span></summary>
[프로그래머스: 신규 아이디 추천 (Lv.1)](https://programmers.co.kr/learn/courses/30/lessons/72410)

위 문제를 해결하고 다른 사람의 풀이를 보니 많은 사람들이 정규식을 사용하여 풀이하였습니다. 정규식의 존재 정도만 알고 있었는데, 문자열 관련 문제를 쉽게 풀기 위해 정규식을 잘 정리하여 활용해보자고 마음먹었습니다.

문제에 대한 간략한 설명과 풀이입니다.
> 1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
>
> 2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
> ... (생략) ... 

저는 이 문제를 다음과 같이 접근했었습니다.

```java
if(ch >= 'A' && ch <= 'Z'){
                stringBuilder.append((char)(ch+32));
                continue;
            }
            if((ch >= 'a' && ch <= 'z') || (ch >= '0' && ch <= '9')){
                stringBuilder.append(ch);
                continue;
            }
```



이 코드를 정규식을 사용하여 간단하게 표현하면 다음과 같습니다.

```java
String temp = new_id.toLowerCase();
temp = temp.replaceAll("[^-_.a-z0-9]","");
```

</details>



자바 도큐먼트와 블로그 등을 참고하여 작성하였으나 부족한 부분이 있는 것 같아 추가로 알고리즘 개정 4판 (로버트 세지웍, 케빈 웨인) 을 공부하여 정리하였습니다.

# 연산자

 정규 표현식에 사용되는 기초 연산자들입니다.

| 연산자        | 예   | 설명                                                         |
| ------------- | ---- | ------------------------------------------------------------ |
| Concatenation | AB   | 연결 된 문자. A와 B가 연결 된 길이 2인 문자열 한 개의 집합.  |
| Or            | A\|B | A 또는 B. 집합 {A, B}.                                       |
| Closure       | A*   | 자기 자신과 임의의 횟수만큼 반복 연결하여 만들어지는 언어. 0을 포함한다. |

# 축약어

패턴을 압축적으로 표현하기 위한 확장 규칙들입니다.



## 문자 집합 표현

| 이름       | 표기법                          | 예        | 설명                     |
| ---------- | ------------------------------- | --------- | ------------------------ |
| 와일드카드 | .                               | A.B       | 임의의 문자 한개         |
| 집합 지정  | []으로 둘러 쌈                  | [AEIOU]*  | 그 문자들 중 임의의 문자 |
| 범위       | []으로 둘러쌈, -으로 구분       | [A-Z]     | 문자의 범위 표현         |
| 역집합     | 앞첨자 ^를 붙이고 []으로 둘러쌈 | [^AEIOU]* | 그 문자들이 아닌 문자    |

<br/>

## 클로저 축약어

| 표기법       | 예     | 설명              |
| ------------ | ------ | ----------------- |
| 곱셈 기호(*) | A*     | 0 혹은 여러번     |
| 덧셈 기호(+) | A+     | 1번 혹은 여러번   |
| 물음표(?)    | A?     | 0 or 1            |
| 중괄호({})   | A{n}   | 정확히 n번        |
|              | A{n,}  | 최소 n번          |
|              | A{n,m} | 최소 n번 최대 m번 |

*주의: A{n,m} 은 m을 포함.

<br/>

## 이스케이프 시퀀스

| 표기법 | 설명                                                    |
| ------ | ------------------------------------------------------- |
| \d     | 숫자: `[0-9]`와 동일                                    |
| \D     | 숫자가 아닌 문자: `[^0-9]`와 동일                       |
| \s     | 공백 문자: `[\t\n\x0B\f\r]`와 동일                      |
| \S     | 공백 문자를 제외한 문자: `[^\s]`와 동일                 |
| \w     | 알파벳, 언더스코어(_), 숫자 문자: `[a-zA-Z_0-9]`와 동일 |
| \W     | `[^\w]`와 동일                                          |

# 정규식과 관련된 String methods

|Method|Description|
|---|---|
|String.matches(regex)|String이 regex와 일치하면 true 리턴|
|String.split(regex)|regex와 일치하는 것을 기준으로 String을 분리하여 배열로 리턴|
|String.replaceFirst(regex, replacement)|regex와 가장 먼저 일치하는 것을 replacement로 변환|
|String.replaceAll(regex, replacement)|regex와 일치하는 모든 것을 replacement로 변환|

# 관련 코테 문제들

- [프로그래머스: 신규 아이디 추천 (Lv.1)](https://programmers.co.kr/learn/courses/30/lessons/72410)

# 참고한 문서들

- [https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html](https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html)
- [https://codechacha.com/ko/java-regex/](https://codechacha.com/ko/java-regex/)
- 📘 로버트 세지웍, 케빈 웨인, 『알고리즘 개정 4판』
