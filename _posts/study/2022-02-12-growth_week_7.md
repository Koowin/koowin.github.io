---
title:  "Growth Study: 22.02.12.토"

toc: true
toc_label: "Contents"
toc_icon: "bars"
toc_sticky: true

categories:
  - study

date: 2022-02-12
last_modified_at: 2022-02-12
---

# 개인발표

 Spring 프로젝트를 시작하기 앞서 Spring이 무엇인가? 에 대한 주제로 공부를 하기 시작하였습니다. IOC, DI, AOP, POJO 등 처음 보는 용어들이 눈에 들어왔는데,



## 의존성

 의존성이 무엇인가에 대해 설명하기 위해 이번 공통 과제로 나온 체스 게임을 약간 변형하여 예로 들어 설명해보겠습니다. Game 은 하나의 기물만을 움직여보는 아주 간단한 객체입니다.

다음과 같이 King, Game 이 정의되어 있다고 해보겠습니다.

```java
public class King{
	public void move(){
		...
	}
}
```

```java
public class Game{
    private King piece;
	
    public Game(){
		piece = new King();
	}
    
    public void apply(){
        piece.move();
    }
}
```

Game 객체에서는 King 기물을 움직이기 위해 apply 라는 메소드를 사용합니다. 현재 Game 내에 King 객체가 new 를 통해 생성되어 있습니다. 이러할 경우 'Game 은 King 에 의존성이 있다' 라고 합니다.

만약 누군가 필요에 의해 King 의 move 메소드를 삭제하거나 이름을 바꾸면 어떻게 될까요? Game 에서 piece.move(); 라인 또한 바뀌어야할 것입니다.

이러한 문제점을 고치기 위한 것이 의존성 역전 원칙을 준수하는 것입니다.

<br/>

## 의존성 역전 원칙

 의존성 역전 원칙이란 "고수준 모듈은 저수준 모듈의 구현의 의존해서는 안 된다. 저수준 모듈이 고수준 모듈에서 정의한 추상 타입에 의존해야한다."는 원칙입니다.

 마찬가지로 위 예를 들어 설명해보겠습니다. 다음과 같이 Piece라는 interface를 생성하여보겠습니다.

```java
public interface Piece{
    move();
}
```

 이 인터페이스를 이용한다면 위의 King 객체와 Game 객체는 다음과 같이 바뀔 것입니다.

```java
public class King implements Piece{
	@Override
	public void move(){
		...
	}
}
```

```java
public class Game{
	private Piece piece;
    
    public Game(){
        piece  = new King();
    }
    
	pulbic void apply(){
		piece.move();
	}
}
```

Game 은 더 이상 King 에 의존하지 않고 Piece 인터페이스에 의존하여 move() 를 호출하게 됩니다. 즉, King 과의 결합도가 낮아져 King 의 변화에 덜 취약하게 되었습니다.

 하지만 또 하나의 문제가 생깁니다. 만약 piece 를 필요에 따라 King 기물 뿐만 아니라 Queen, Bishop, Rook, Kinght, Pawn 등의 기물들로 변경하여 사용하고 싶을 때는 어떻게 할까요? 역시 마찬가지로 Game 생성자 내의 코드를 수정하여 다른 기물들로 바꿔주어야 할 것 입니다. 이러한 문제점을 해결하기 위해 의존성 주입이 필요합니다.

<br/>

## 의존성 주입

 Spring 프레임워크의 3가지 핵심 프로그래밍 모델 중 하나가 의존성 주입(Dependency Injection, DI)입니다. DI란 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴으로, 인터페이스를 사이에 둬서 클래스 레벨에서는 의존관계가 고정되지 않도록 하고 런타임 시에 관계를 동적으로 주입하여 유연성을 확보하고 결합도를 낮출 수 있게 해주는 장점이 있습니다.

```java
public class Game{
	private Piece piece;
    
    public Game(Piece piece){
		this.piece = piece;
    }
    
	pulbic void apply(){
		piece.move();
	}
}
```

 Game 내의 코드를 수정할 필요 없이 Game 에 Piece 를 '주입'하여 사용하는 것입니다. Game 을 생성할 시점에 King 뿐만 아니라 필요에 따라 다른 기물들을 매개변수로 넣어준다면 유연하게 주입받은 기물을 사용하는 것입니다.

<br/>

 다양한 의존성 주입 방법이 있지만, Spring 에서 권장하는 생성자 주입으로 설명하였습니다. 만약, 다른 의존성 주입 방법들이 궁금하다면 [다른 분이 작성하신 글](https://mangkyu.tistory.com/125)에 잘 정리되어 있습니다.

<br/><br/>

# 출처

* 📄https://velog.io/@emawlrdl/Spring-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC-60k5hr47w2
* 📄https://devlog-wjdrbs96.tistory.com/165
* 📄https://mangkyu.tistory.com/150