---
title: 'String, StringBuffer, StringBuilder 의 차이점'
catalog: true
tags:
  - Java
catagories:
  - Java
date: 2017-07-15 22:26:15
subtitle:
header-img:
---


안녕하세요?

철학적인 개발자 JayB 입니다.

## 들어가기에 앞서...

오늘은 제가 알고리즘 문제를 풀 때 문제가 의도하는 상황에 맞게 문자를 자유자재로 수정해야 되거나 문자열을 가지고

이것저것 해야 될 때 자주 사용하는 StringBuffer 에 대해서 알아보려고 합니다.

StringBuffer를 사용할 줄 알면 당연히 조사해보면 나오는 StringBuilder 라는 API와의 차이는 무엇인지

알아야 겠죠?

정리를 해보지 않으면 기억에 오래 머물지 않을 것 같아 정리하게 되었습니다.

## 불변객체와 가변객체 (String vs StringBuffer 와 StringBuilder)

일단 String 과 StringBuffer 또는 StringBuilder 의 차이를 알려면

**불변객체** 와 **가변객체** 의 개념부터 알아야 됩니다.

* [불변객체](https://docs.oracle.com/javase/tutorial/essential/concurrency/immutable.html)

> 객체 지향 프로그래밍에 있어서 불변객체(immutable object)는 생성 후 그 상태를 바꿀 수 없는 객체를 말한다

* [가변객체](https://ko.wikipedia.org/wiki/%EB%B6%88%EB%B3%80%EA%B0%9D%EC%B2%B4)

> 가변(mutable) 객체로 생성 후에도 상태를 변경할 수 있다.

용어가 어렵지 사실 쉽게 이해할 수 있다. 반대 개념이고 객체안에 저장된 값을 수정할 수 없거나 수정할 수 있거나.

수정할 수 없다면 불변객체!

수정할 수 있다면 가변객체!

예를 들어, 불변객체 String 으로 문자를 수정해야 될 경우를 보시면 됩니다.

banan (바나나) 라는 문자에 a 가 빠져있습니다. 문자 a 를 추가하기 위해선 String 에 정의된

banan 를 지우고 다시 생성해야 됩니다. 그러므로, 프로그래밍적 자원과 비용이 많이 소모 됩니다.

```
String = "banan";
String = "banana";
```

반면, 가변객체 StringBuffer 나 StringBuilder 로 위와 같은 사항을 해결해야 된다면

```
append() 함수
```

를 사용하면  쉽게 해결이 가능합니다.

```
StringBuffer sb = new StringBuffer();
sb.append("banan");
sb.append("a");
```

이제 불변객체와 가변객체의 차이를 아셨나요?

그렇다면, StringBuffer 와 StringBuilder 와의 차이는 뭘까요?

## StringBuffer 와 StringBuilder 의 차이

* [StringBuffer](http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuffer.html)

> A thread-safe, mutable sequence of characters. A string buffer is like a String,
  but can be modified. At any point in time it contains some particular sequence of characters, but the length and content of the sequence can be changed through certain method calls. String buffers are safe for use by multiple threads.

* [StringBuilder](http://docs.oracle.com/javase/7/docs/api/java/lang/StringBuilder.html)

> A mutable sequence of characters. This class provides an API compatible with  
  StringBuffer, but with no guarantee of synchronization. This class is designed for use as a drop-in replacement for StringBuffer in places where the string buffer was being used by a single thread (as is generally the case).
  Instances of StringBuilder are not safe for use by multiple threads. If such synchronization is required then it is recommended that StringBuffer be used.

영어로 머리가 아파오시나요? 어쩔 수 없습니다.

개발하려면 영어와 친숙해져야 합니다 ...

핵심은 이러합니다.

**StringBuffer** 와 **StringBuilder** 둘다 가변객체입니다.

차이점은 아래와 같습니다.

* A thread-safe vs no guarantee of synchronization

StringBuffer는 멀티스레드 환경에서 StringBuffer 인스턴스에 접근해서 조작해도 그 값에 대한 접근이 가능하다는

얘기입니다. 반면, StringBuilder 는 그렇지 않다는 거죠.

> Instances of StringBuilder are not safe for use by multiple threads.
  If such synchronization is required then it is recommended that StringBuffer be used.

위 문구를 보면 멀티스레드 환경에서는 StringBuilder 인스턴스는 안전하지 않으니 동기화가 필요할 시

StringBuffer 를 사용하라고 권장하고 있군요.

멀티스레드 환경이 뭔지 잘 모르신다구요? 구글링을 생활화 하셔야 됩니다.

구글링을 통해 멀티스레드 환경에 관련된 여러 자료를 숙지하신 후 다시 보시면 이해가 쉽게 되실 겁니다.

## 이 글을 마치며...

오늘은 String, StringBuffer, StringBuilder 에 관련하여 알아보았습니다.

정리한 후 머릿속에 제대로 저장이 됬는지 확인을 해보기 위해 저는 제가 쓴 글을 여러번 읽고

수정하는 절차를 가집니다.

제가 미처 찾지 못한 오타나 잘못된 정보가 있다면 아래 댓글로 달아주시기 바랍니다.

확인하는 즉시 수정하도록 하겠습니다.

이상 철학적인 개발자 JayB 였습니다.

