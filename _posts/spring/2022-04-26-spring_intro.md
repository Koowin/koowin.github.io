---
title:  "Spring Framework Intro"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - spring

date: 2022-04-26
last_modified_at: 2022-04-26
sitemap:
  changefreq: daily
  priority: 1.0
---



# 스프링의 핵심 개념, 컨셉

자바 언어 기반의 프레임워크 -> 객체 지향 언어가 가진 강력한 특징을 살려내는 프레임워크

즉, 좋은 객체 지향 애플리케이션을 개발할 수 있게 도와주는 프레임워크





# 객체 지향 프로그래밍?

프로그램 != 명령어 목록
프로그램 == '객체'들의 모임. 객체 끼리 서로 메시지를 주고받고 데이터를 처리 (협력)

장점 : 유연하고 변경이 용이



# 다형성

역할(인터페이스)과 구현(구현체)으로 구분.

클라이언트에 영향을 주지 않고 새로운 기능 제공 가능. '역할'을 지킨다면 서로 다른 '구현'을 대체할 수 있다.

클라이언트는 인터페이스만 알면 된다. 구현 대상의 내부 구조를 몰라도 된다. 내부 구조가 변경되어도 영향을 받지 않는다. 대상 자체를 변경해도 영향을 받지 않는다.



# 객체의 관계

혼자 있는 객체는 없다. 객체는 협력 관계.

e.g. 클라이언트: 요청, 서버: 응답.



# Java 언어의 다형성

'오버라이딩'에 의해 동작한다.

클라이언트는 인터페이스에 있는 메서드를 호출한다.
이 인터페이스의 메서드를 구현한(오버라이딩한) 구현체의 메서드가 실행된다.



# 한계점

인터페이스가 변하면 클라이언트, 서버 모두에 큰 변경이 발생한다.

따라서, 인터페이스를 안정적으로 잘 설계하는 것이 중요하다.



# 스프링과 객체 지향

다형성이 가장 중요. -> 스프링이 다형성을 극대화해서 이용할 수 있게 도와준다.

여기서 등장하는 개념이 제어의 역전(IoC), 의존관계 주입(DI)



# 출처

* 스프링 핵심 원리 기본편 (김영한, 인프런)