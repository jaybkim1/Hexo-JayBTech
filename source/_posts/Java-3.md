---
title: 프로세스와 스레드의 차이
subtitle: 기술면접의 단골 질문인 프로세스와 스레드의 차이점
catalog: true
tags:
  - Java
catagories:
  - Java
date: 2017-06-05 21:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 가장 기본적인 개념이지만 간과할 수 없는 핵심적인 개념! 프로세스와 스레드의 차이에 대해 정리해보는 시간을 가지려 합니다.

## 들어가기에 앞서...

기술면접의 단골질문중에 하나죠.

참고로 이 질문은 구글 면접 질문에도 나왔다고 합니다.

가장 기본적이면서도 핵심적인 질문.

> 프로세스와 쓰레드의 차이점에 대해 설명해주세요.

띠로링!

![긁적긁적](https://user-images.githubusercontent.com/20435620/30306330-77f79540-97b2-11e7-9fa6-b27e0d086481.png)

음...? 나 이거 분명 알았는데 어떻게 설명 해야 되지?

가만 있어보자... -_-;;

이 글을 다 읽고 저 처럼 당황하는 분이 없길 바라며 프로세스와 스레드의 차이점에 대해 정리해봅니다.

개발을 하다보면 기능만 뚝딱 만들고 개념적인 부분이나 이론적인 부분은 간과하고 넘어갈때가 있는 것 같습니다.

하지만, 이는 개발자로 계속 삶을 살아간다면 언젠간 다시 부메랑 처럼 돌아오게 됩니다.

예를 들어,

기술면접을 볼 때 내가 기술에 대해 어느정도 알고 있다를 설명해야 될 경우나

다른 누군가에게 이 개념에 대해 설명을 해줘야 하는 상황이 생길때

그때 제대로 볼걸. 이라는 후회가 밀려오게 됩니다.

ㅜㅜ

다른얘기로 빠질거 같아, 이제 본론으로 들어가 보도록 하겠습니다.

프로세스와 스레드에 대해 알아보기전에 먼저 **프로그램과 프로세스** 부터 알아야 합니다.

## 프로그램과 프로세스

컴퓨터를 해보셨으면 프로그램이 뭔지는 어느정도 머릿속에 그려지시죠?

프로그램은

> 어떤 작업을 위해 실행할 수 있는 파일

입니다.

예를 들어, 제가 좋아하는 스타크래프트 게임을 할때 Starcraft.exe 파일을 실행시켜야 하죠?

스타크래프트 **프로그램** 을 실행하는 겁니다.

프로세스는

> 메모리에 올라와 CPU를 할당받고 프로그램이 실행되고 있는 상태

또는

> 프로세스는 운영체제로부터 자원을 할당받는 작업의 단위. 쉽게 말해, 컴퓨터에서 실행중인 컴퓨터 프로그램을 의미합니다.

입니다.  

즉, 프로세스는 동적인 개념으로 **실행된 프로그램** 을 말하는 겁니다.

예를 들어, 메모장을 4개를 킨다고 해봅시다.

메모장이라는 프로그램이 총 4번 실행되었고 그에 따라 총 4개의 프로세스가 메모리 상에 올라가 있는겁니다.

그럼 이제 스레드에 대해서 알아볼까요?

## 스레드의 정의

스레드는

> 프로세스가 할당받은 자원을 이용하는 실행의 단위

입니다.

> 기본적으로 하나의 프로세스가 생성되면 하나의 스레드가 같이 생성되는데 이를 메인 스레드라고 부릅니다,
  스레드를 추가로 생성하지 않는 한모든 프로그램 코드는 메인 스레드에서 실행이 됩니다.

또한, 프로세스는 여러개의 스레드를 가질 수 있는데 이를 **멀티 스레드** 라고 합니다.

자, 정리를 해보자면

**프로그램** 은 어떤 작업을 위해 실행 하는 파일.

**프로세스** 는 프로그램이 실행되고 있는 상태. 프로세스는 실행이 됬을때 **운영체제 (OS)로 부터 자원(메모리와 같은 주소 공간)을 할당** 을 받습니다.

**스레드** 는 한개의 **프로세스 내에서 동작되는 여러 실행의 흐름.**  

이해하셨나요?

그럼 이제 프로세스와 스레드의 공통점과 차이점에 대해 알아보도록 합시다.

## 프로세스와 스레드의 공통점과 차이

###공통점

멀티프로세서와 멀티스레드 양쪽 모두 **여러 흐름이 동시에 진행** 된다는 공통점을 가지고 있습니다.

###차이점

멀티프로세서에서 각 프로세스는 독립적으로 실행되며 각각 별개의 메모리를 차지하고 있지만 멀티스레드는 프로세스 내의

메모리를 공유해 사용할 수 있습니다.

프로세스 간의 전환 속도보다 스레드 간의 전환 속도도 빠릅니다. (스레드간의 속도 Win !)

## 멀티 프로세스 vs 멀티 스레드로

왜 멀티 프로세스 (여러 프로세스)로 할 수 있는 작업들을 굳이 하나의 프로세스에서 멀티 스레드(여러 스레드)로 나눠가면서 할까요?

쭉 읽어보면서 대충 눈치 채셨겠지만 생각하시는게 맞습니다.

> 효율적인 시스템 작업을 위해서

멀티 스레드를 사용합니다.

상식적으로 생각해봐도 프로그램을 여러개 키는 것보다 그 프로그램안에서 해결할 수 있다면 하나늬 프로그램안에서 여러 작업을 하는게 좋겠죠?

멀티 프로세스로 실행되는 작업을 멀티 스레드로 실행할 경우, **프로세스를 생성하여 자원을 할당하는 시스템 콜** 이 줄어들어 **자원을 효율적으로

관리할 수 있습니다.**

이뿐만 아니라 프로세스 간의 통신보다 스레드 간의 통신이 비용적으로 저렴하며작업들 간의 통신의 부담이 줄어들게 됩니다.

이처럼 스레드를 활용하면 자원의 효율성이 증가하기도 하지만 스레드 간의 통신시 데이터를 주고받는 방법은 메모리 공간을 공유하므로 데이터 세그먼트,

즉 전역 변수를 이용하여 구현하게 되는데, 공유하는 전역 변수를 여러 스레드가 함께 사용하려면 충돌현상이 발생하게 됩니다.

따라서, 스레드 간에 통신할 경우에는 충돌 문제가 발생하지 않도록 **동기화 문제** 를 프로그래머가 직접 해결해줘야 합니다.

이 때문에 *멀티스레드 프로그래밍은 프로그래머의 주의* 를 요구합니다.

## 스레드의 장점

* 시스템의 throughput이 향상된다.  

* 시스템의 자원 소모가 줄어든다  

* 프로그램의 응답 시간이 단축된다.  

* 프로세스 간 통신 방법에 비해 스레드 간의 통신 방법이 훨씬 간단하다.


## 스레드의 단점

* 여러 개의 스레드를 이용하는 프로그램을 작성하는 경우에는 주의 깊게 설계해야 한다.     
	미묘한 시간 차나 잘못된 변수를 공유함으로써 오류가 발생할수 있다.

* 프로그램 디버깅이 어렵다.  

* 단일 프로세서 시스템에서는 효과를 기대하기 어렵다.

-------------------------------------------------------------------------------------------------------------

**프로세스와 스레드의 차이점에 대한 질문의 요지를 곰곰히 생각해보면 다음과 같은 개념과 이해가 있는지에 대해 물은 것 입니다.**

* 프로세스와 스레드의 차이를 알고 있나요? 어떤 차이점이 있을까요?

* 운영체제와 어떤 밀접한 관계를 가지고 있고 운영체제가 할당한 자원을 어떻게 사용되는지에 대해서도 알고 있나요?

* 멀티프로세스와 멀티스레드에 대해 알고 있나요?

* 위 질문에 이어서 멀티스레드 환경에서 프로그래밍한 경험은 있나요?

* 그에 대한 장 단점은 자세히 알고 있나요?

* 멀티스레드 환경에서 동기화 문제를 경험했봤나요? 했다면 어떻게 해결했나요?


> 프로세스와 쓰레드의 차이점에 대해 설명해주세요.

이 질문 하나로 위 질문들과 같이 다양한 질문이 연이어 나올 수 있기 때문에

프로세스와 쓰레드의 차이점에 대한 질문은 아주 **기본적** 이지만 **핵심적** 인 질문입니다.

이제 프로세스와 스레드의 차이에 대해 좀 감이 오셨나요?

많은 부분이 연관되어 설명되야 되기 때문에 최대한 핵심적인 부분만 정리해봤습니다.

감이 안오셨다면 위에서 부터 다시 한번 읽어보시고 다른 사이트들도 참고해보시기 바랍니다.


## 참고한 블로그

* [사용자수준 쓰레드와 커널수준 쓰레드의 차이?](https://kldp.org/node/295)

* [프로세스와 스레드](https://lalwr.blogspot.kr/2016/02/process-thread.html)

* [프로세스와 스레드 ](https://medium.com/@kill5038/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-process-%EC%99%80-%EC%8A%A4%EB%A0%88%EB%93%9C-thread-833b971b9790)
