---
title: 추상(Abstract)클래스와 인터페이스(Interface)
subtitle: 객체지향 OOP를 활용하기 위한 중요한 두가지 개념
catalog: true
tags:
  - Java
catagories:
  - Java
date: 2017-04-25 21:26:15
header-img:
comments: true
---


## 들어가기에 앞서...

이 포스팅에서 다룰 주제는 추상클래스와 인터페이스 입니다.

자바에서는 객체지향을 본격적으로 활용하기 위해서는 자바의 객체지향 개념을 더욱 더 깊게 이해하고 적용할 필요가 있습니다.

자바에서는 C언어나 여타 원시적인 프로그래밍 언어에서는 제공하지 않았던 특수한 기능들을 제공합니다.

대표적으로 추상 (Abstract)의 개념이 있으며 그와 비슷하지만 조금 다른 개념인 인터페이스 (interface)의 개념이 존재합니다.

자바에서는 이러한 다양한 설계 기법들을 제공하기 때문에 개발 자체에서는 안정성과 확장 가능성을 보장받을 수 있게 됩니다.

## 추상클래스 Abstract Class

추상적이다? 라는 의미는 무엇을 의미할까요?

> 구체성이 없이 사실이나 현실에서 멀어져 막연하고 일반적인 또는 그런 것.

> Abstraction is a process of hiding the implementation details and showing only functionality to the user.

**A process of hiding the implementation details and showing only functionality to the user**

자바에서는 일종의 *미완성 클래스* 라고 할 수 있는 추상클래스를 제공합니다.

추상클래스에서는 직접적으로 객체 인스턴스 (Instance) 를 생성할 수 없습니다.

하지만, 새로운 클래스를 작성하는데 밑바탕이 되는 역할을 해준다는 것에서 의미가 있습니다.

어느 정도 *미리 설계로서 틀을 갖추고 클래스를 작성 할 수 있게 한다* 는 기능적인 측면에서 의미가 있습니다.

아래 그림을 한번 보면 이해가 빠를겁니다.

[추상클래스](https://user-images.githubusercontent.com/20435620/29594140-dfa93a50-87e9-11e7-9a3f-c82f2d7e464f.png)

직사각형, 원, 삼각형 전부 다 모양이라는 SHAPE 추상클래스를 가르키고 있고

*SHAPE 추상클래스* 안에는 넓이를 구하는 *calculateArea()* 라는 함수와 출력할 수 있는 *display()* 라는 함수가 있습니다.

이렇게 공통적으로 가지는 함수를 추상클래스에 명시해두고 추상클래스를 상속받으면 그 함수들을 사용할 수 있게 되어

여러 클래스에서 다 정의할 필요 없이 사용이 가능합니다.

즉, *미리 어떤 클래스를 구현하기 전에 저런 함수들을 사용할거다* 라고 *설계* 를 하면 되는 것입니다.

추상클래스는 반드시 상속을 받아야 하며 상속받은 모든 추상 메소드를 반드시 구현을 해주어야 합니다.


## 인터페이스 (Interface)

추상클래스보다 더 추상적인 인터페이스

얼핏 보기에는 추상 클래스와 매우 흡사한 개념이라고 느껴지실 수 있습니다.

처음 추상클래스와 인터페이스를 접했을때 멘붕이였던 기억이 ㅜㅜ

인터페이스는 *숙련된 자바 개발자들에게 아주 선호되는 설계 기능* 이면서 자바에서 *다중 상속을 구현* 하게 해주는 고급 기술이기도 합니다.

기본적으로 자바에선 다중상속을 할 수 없습니다.

예를 들면, 클래스 A, 클래스 B가 있고 메인클래스가 있다고 합시다.

메인클래스에서 클래스 A와 클래스 B를 다중상속할 수 없다는 의미입니다.

바로 이렇게 말이죠.

```
Main extends A, B (X)

public class Main extends A, B{

	public static void main(String[] args) {

	}

}
```

하지만, **인터페이스가 이를 가능** 하게 해줍니다.

인터페이스는 extends 를 사용하지 않고 implements 를 사용합니다.

```
Main implements A, B (O)

public class Main implements A, B{

	public static void main(String[] args) {

	}

}
```

추상클래스는 이것저것 메소드안에 살을 부칠수 있는 반면,

인터페이스는 딱 정해놓은 메소드만 가져올 수 있습니다.

## 정리를 해보자면...

**인터페이스는 팀 프로젝트의 동시 작업에 유리하고 일반적으로 추상클래스 보다 요구되는 설계의 기준이 높아서 더 체계적** 이라는 평을 받는다.

* 좀 더 엄격한 설계!

* 좀 더 체계적!

* 인터페이스 안에선 설계만 해야되는 것 !

즉, 메소드만 정의 할 수 있다는 겁니다.

제가 미처 찾지 못한 오타나 잘못된 정보가 있다면 아래 댓글로 달아주시기 바랍니다.

확인하는 즉시 수정하도록 하겠습니다.

이상 철학적인 개발자 JayB 였습니다.


## 정리하면서 참고한 블로그 및 강좌

* [생활코딩 - 추상클래스] : [https://opentutorials.org/course/1223/6062](https://opentutorials.org/course/1223/6062)

* [생활코딩 - 인터페이스] : [https://opentutorials.org/course/1223/6063](https://opentutorials.org/course/1223/6063)

* [JAVA의 다형성 - 인터페이스와 추상클래스] : [http://enter.tistory.com/122](http://enter.tistory.com/122)

* [인터페이스] : [https://www.youtube.com/watch?v=XkSWgIQ2zkk](https://www.youtube.com/watch?v=XkSWgIQ2zkk)
