---
layout: single
title:  "Regular Expressions"
---



# Java - 정규 표현식



## 동기  

프로그래머스의 한 문제를 해결한 뒤 다른 사람의 풀이를 보니 정규식을 이용하여 쉽게 해결하는 방법이 있었다.  



문제: https://programmers.co.kr/learn/courses/30/lessons/72410

1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.

2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
... (생략) ...




나는 이 문제를 다음과 같이 접근했었다.

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

정규식을 사용한 풀이는 다음과 같다.
```java
String temp = new_id.toLowerCase();
temp = temp.replaceAll("[^-_.a-z0-9]","");
```
정규식이 자바 문자열 처리에 꼭 필요하다는 생각이 들어 이 기회에 정리해보기로 하였다.



## 문법
다음의 문서들을 보고 기초적인 문법만 정리하였다.
https://docs.oracle.com/javase/7/docs/api/java/util/regex/Pattern.html
https://codechacha.com/ko/java-regex/
더 많은 정보가 필요할 경우 해당 문서를 참조하자.



### Character classes
|||
|---|---|
|[abc]|a,b,c 중 하나|
|[^abc]|a,b,c를 제외한 문자 하나|
|[a-zA-Z]|a~z 혹은 A~Z 중 하나|
|[a-z&&[^bc]|a~z 중 b,c를 제외한 문자 하나|


### Predefined character classes
|||
|---|---|
|.|아무 문자|
|\d|숫자: [0-9]와 동일|
|\D|숫자가 아닌 문자: [^0-9]와 동일|
|\s|공백 문자: [ \t\n\x0B\f\r]와 동일|
|\S|공백 문자를 제외한 문자: [^\s]|
|\w|알파벳, _, 숫자 문자: [a-zA-Z_0-9]와 동일|
|\W|[^\w]|

재미있는 점은 "\대문자 == not \소문자"라는 점이다.




### Greedy quantifiers  

|||
|---|---|
|X?|X가 없거나 한번이거나|
|X*|X가 0 혹은 여러번|
|X+|X가 한번 혹은 여러번|
|X{n}|X가 정확히 n번|
|X{n,}|X가 최소 n번|
|X{n,m}|X가 최소 n번 최대 m번|  


주의할 점은 X{n,m}에서 'm 미만'이 아닌 'm 이하'라는 점이다.



## 정규식과 관련된 String methods

|Method|Description|
|---|---|
|String.matches(regex)|String이 regex와 일치하면 true 리턴|
|String.split(regex)|regex와 일치하는 것을 기준으로 String을 분리하여 배열로 리턴|
|String.replaceFirst(regex, replacement)|regex와 가장 먼저 일치하는 것을 replacement로 변환|
|String.replaceAll(regex, replacement)|regex와 일치하는 모든 것을 replacement로 변환|