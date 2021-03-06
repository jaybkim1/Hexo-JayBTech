---
title: List 를 순회하는 방법
subtitle: 자바에서의 다양한 List 순회 방법
catalog: true
tags:
  - Java
catagories:
  - Java
date: 2017-05-01 21:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 자바에서 여러가지 방법으로 List를 순회하는 방법을 정리해보는 시간을 가지려 합니다.

## 리스트

아래와 같이 List에 5 가지의 과자 문자열을 가지고 있다고 할 때 하나하나의 과자를 출력해보려고 합니다.

```
	List<String> fruits = new ArrayList<>(Arrays.asList("자갈치", "새우깡", "오레오", "빼빼로", "치토스"));
```


## 일반적으로 사용되는 for loop 돌리기

가장 일반적인 for 문 돌리기로 List 안에 있는 과자 원소들을 출력하는 방법입니다.

```
	for (int i = 0; i < fruits.size(); i++) {
		System.out.println(fruits.get(i));
	}
```

하지만 이 방법은 E get(int index) 메소드를 가지는 List 타입의 객체 대상으로만 사용할 수 있습니다.

상위 타입인 *Collection* 이나 *Set* 과 같은 **이종 타입의 객체** 대상으로는 사용이 불가한 방법입니다.


## Iterator

아래와 같이 Iterator 를 사용하는 방법도 있습니다.

```
	for (Iterator<String> iter = fruits.iterator(); iter.hasNext(); ) {
	  System.out.println(iter.next());
	}
```

Iterator 를 사용하면 Collection 을 순회할 수 있을 뿐만 아니라 순회 도중에 특정 원소를 안전하게 삭제할 수도 있습니다.


## 향상된 for loop (Java 5 이상)

Java5 에서 도입된 for-each문 이라고도 불리는 향상된(Enhanced) For 루프문을 사용하면 좀 더 깔끔하게 코드를 작성할 수 있습니다.

```
	for (String fruit : fruits) {
	  System.out.println(fruit);
	}
```


## Stream API (Java 8 이상)

Java8 이상을 사용하신다면 스트림을 이용해서 다음과 같이 루프문을 사용하지 않고도 명료한 한 줄 코드를 작성할 수 있습니다.

```
	fruits.stream().forEach(System.out::println);
```

이상으로 자바에서 컬렉션을 순회할 때 사용할 수 있는 다양한 옵션에 대해서 알아보았습니다.

## 정리하면서 ...

Iterator 나 향상된 for loop 으로 순회하는 방법은 알고 있었지만 아무래도 가장 기본적인 for loop 에

적응 되어 있다보니 기본적인 것만 사용해왔습니다.

마지막 방법인 Stream API 는 한줄로 끝나버리니 신선하네요.

아무래도 코드가 굉장히 간결해지겠죠?

이렇게 다양한 방법을 알아두고 적용해봐야 다른 사람이 작성한 코드를 검토할 때 도움이 될 것 같아 정리해봤습니다.


## 참고한 블로그

* [자바 공식홈페이지] : [http://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html](http://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html)

* 대부분의 내용은 DaleSeo님의 [리스트를 순회하는 방법]을 참고하였습니다 : [http://www.daleseo.com/how-to-traverse-list-in-java/](http://www.daleseo.com/how-to-traverse-list-in-java/)
