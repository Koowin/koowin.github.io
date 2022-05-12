---
title:  "싱글톤 패턴과 컨테이너"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - spring

date: 2022-05-09
last_modified_at: 2022-05-09
sitemap:
  changefreq: daily
  priority: 1.0
---

# 개요

앞서, 스프링 컨테이너는 Bean 들을 등록해놓고 관리한다는 것을 배웠습니다.

스프링 컨테이너에서는 기본적으로 이러한 Bean 들을 싱글톤(singleton)으로 등록하고 관리합니다.

싱글톤이란 무엇이고, 어떤 장점과 단점이 있을까요?



# 싱글톤이란?

싱글톤 패턴이란, 인스턴스를 오직 하나만 생성할 수 있는 클래스를 말합니다.

무상태(stateless) 객체나 설계상 유일해야하는 시스템 컴포넌트에서 주로 사용합니다.

# 싱글톤을 만드는 방식

이펙티브 자바에서 설명하는 싱글톤을 만드는 대표적인 방법은 3가지가 있습니다.

그 중 열거타입을 이용한 방식이 대부분의 상황에서 바람직하다고 설명하고 있습니다.

간단하게 만드는 방식만 소개하겠습니다.



## 정적 필드를 통해 접근하도록 하는 방식

```java
public class Singleton {
  public static final Singleton INSTANCE = new Singleton();
  private Singleton() { ... }

  public void doSomething() { ... }
}
```



## 정적 팩터리 메서드를 public static 멤버로 제공하는 방식

```java
public class Singleton {
	private static final Singleton INSTANCE = new Singleton();
	private Singleton() { ... }
	public static Singleton getInstance() { return INSTANCE; }
  
  public void doSomething() { ... }
}
```



## 원소가 하나인 열거 타입을 이용하는 방식

```java
public Enum Singleton {
  INSTANCE;
  
  public void doSomething() { ... }
}
```



# 싱글톤의 장점

* 인스턴스가 절대적으로 한 개만 존재하는 것을 보증한다.
* 단 하나의 인스턴스만 생성하기 때문에 메모리 낭비를 방지하고 생성 시간을 줄인다.

# 싱글톤의 단점

* 싱글톤 패턴을 구현하기 위해 코드가 길어진다.
* `싱글톤 객체`를 사용하는 객체는 구체 클래스에 의존하게 되므로 DIP 를 위반한다. 또한 OCP 원칙을 위반할 가능성이 높다.



# 싱글톤과 컨테이너

스프링 컨테이너는 위와 같은 싱글톤의 단점을 해결하면서 장점만을 취해 관리합니다.

싱글톤을 구현하기 위한 추가 코드 작성이 필요하지 않으며, 의존성 주입을 통해 DIP, OCP 원칙을 지킬 수 있습니다.

그러면서 메모리와 성능 효율성을 챙길 수 있습니다.



# 주의할 점

싱글톤 패턴을 이용하면 단 하나의 객체를 생성하여 여러 곳에서 활용합니다. 따라서, 상태를 유지하지 않는, 무상태(stateless)로 설계해야합니다.

다음과 같은 사항들을 주의해서 설계해야합니다.

* 특정 클라이언트에 의존적인 필드가 존재하면 안된다.
* 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다.
* 가급적 읽기만 가능해야한다.

# 출처

* 스프링 핵심 원리 기본편 (김영한, 인프런)
* 이펙티브 자바, 23p