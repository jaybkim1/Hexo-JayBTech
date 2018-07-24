---
title: HashMap 과 Hashtable 의 차이
subtitle: 알고리즘 및 자료구조
catalog: true
tags:
  - Algorithm
catagories:
  - Algorithm
date: 2017-06-10 20:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 HashMap 과 Hashtable 에 관하여 정리해보는 시간을 가지려 합니다.

## 들어가기에 앞서...

JAVA 에서 기본적인 자료 구조를 제공하기 위한 환경을 Java Collection Framework 라고 한다.

아래 이미지는 Java Collection Framework 의 상속 기본 구조이다.

![102210_0507_javacollect1](https://user-images.githubusercontent.com/20435620/30408953-fe7e7616-993c-11e7-90b1-746435906c41.png)


HashMap 과 Hashtable 은 자바에서 제공하는 Map 인터페이스를 구현한 클래스들 입니다.

HashMap 과 Hashtable은 비슷한 역할을 하는 것 같아보이면서도 다르게 구현되어 있습니다.

둘다 Map 인터페이스 콜렉션들이기 때문에 기본적으로 데이터를 **Key(키)** 와 **Value(값)** 로

관리하는 자료구조 입니다.

Map 자료구조는 키를 이용해 데이터를 추출하기 때문에 검색에 용이합니다.

하나씩 살펴보도록 하겠습니다.

이 둘의 관계는 Vector 와 ArrayList 의 관계와 비슷하다고 볼 수 있다.

## HashMap

HashMap 은 Map 인터페이스 계열의 대표적인 클래스이며

데이터를 집어 넣을 때의 put() 메서드, 데이터를 추출 할 때 사용 하는 get() 메서드를 사용합니다.

HashMap은 주요 메소드에 **synchronized** 키워드가 없습니다.

Hashtable과 다르게 **key, value에 null 을 입력할 수 있습니다.**

아래 사용법을 보시죠.

### 간단한 사용법

<pre>

HashMap 을 이용한 데이터 저장 및 출력

<code>
HashMap<String, Integer> map = new HashMap<String, Integer>();

		map.put("a", new Integer(1));
		map.put("b", new Integer(2));
		map.put("c", new Integer(3));

		System.out.println(map.get("a"));
		System.out.println(map.get("b"));
		System.out.println(map.get("c"));
</code>

HashMap Iterator

<code>
import java.util.HashMap;
import java.util.Map.Entry;

public class HashMapBasic {
	public static void main(String[] args) {
		HashMap<String, Integer> hm = new HashMap<>();

		// 값 입력
		hm.put("key", 0);

		// HashMap은 값에 null을 허용한다.
		hm.put("key2", null);


		// HashMap은 키값에 null을 허용한다.

		hm.put(null, 0);

		// 값 출력
		hm.get("key");

		// 반복 처리 with keySet
		for( String s : hm.keySet() ){
			System.out.println(hm.get(s));
		}

		// 반복 처리 with entrySet
		for( Entry<String, Integer> s : hm.entrySet() ){
			System.out.println(s.getKey()+" "+s.getValue());
		}
	}
}
</code>

</pre>

## Hashtable

Hashtable은 put, get과 같은 주요 메소드에 **synchronized** 키워드가 선언 되어 있습니다.

또한 **key, value에 null을 허용하지 않습니다.** 아래의 코드는 기본적인 사용법입니다.

사용방법은 HashMap과 같이 데이터를 삽입할땐 put() 메서드를,

데이터를 추출할땐 get() 메서드를 사용합니다.

<pre>
<code>
import java.util.Hashtable;

public class HashTableBasic {
	public static void main(String[] args) {
		Hashtable<String, Integer> ht = new Hashtable<>();

		ht.put("key", 0);

		// Hashtable은 값에 null을 허용하지 않는다.

		try{
			ht.put("key2", null); // error!
		} catch( Exception e ){
			e.printStackTrace();
		}


		// Hashtable은 키값에 null을 허용하지 않는다.

		try{
			ht.put(null, 0); // error!
		} catch( Exception e ){
			e.printStackTrace();
		}

		// 해당 키 값을 가져온다.
		ht.get("key"); // 0
	}
}
</code>
</pre>

## 차이점 정리

**1. 동기화 (Synchronization) 여부**

* HashMap : 동기화를 지원하지 않는다 (thread-not-safe)

* Hashtable : 동기화를 지원한다. (thread-safe)

즉,

**HashMap은 멀티쓰레드 환경에서 사용하지 않는 걸 권장한다.**

<pre>
<code>
사용할 경우 Collections.synchronizedMap(hashMap) 등 을 이용한 동기화 처리 필수!
</code>
</pre>

**동시 접근이 불가능한 HashMap이 필요할 경우, Java 5 에 나온 ConcurrentHashMap을 사용하면 된다.**

멀티쓰레드 프로그래밍 환경에서는 HashMap 을 쓰면 안되고 Hashtable 을 써야 한다는 것!

단일 쓰레드 환경에서 Hashtable 을 쓰더라도 별 문제는 없는데,

HashTable 은 동기화 처리라는 비용때문에 HashMap에 비해 더 느리기 때문.

**2. NULL 허용 여부**

* HashMap : Value 에 Null 값 허용

* Hashtable && ConcurrentHashMap : Value 에 Null 값 허용 안함


## MultiThread 환경 테스트

아래 소스코드는 [여기](http://jdm.kr/blog/197)서 가져왔다.

아래의 코드는 실제로 동기화를 위해선 어떤 콜렉션을 써야하는지, 왜 그래야 하는지에 대한 코드 테스트이며

위에서 서술한 콜렉션들을 10개의 스레드에서 각각 1000번을 반복하며 랜덤한 값을 입력할 때

엔트리의 사이즈를 비교하는 코드입니다. (성능 테스트는 아니다)

종료 후 결과를 보면 HashMap 만 Entry 사이즈가 다른 것을 확인 할 수 있다.

<pre>
<code>
import java.util.Collections;
import java.util.HashMap;
import java.util.Hashtable;
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.TimeUnit;

public class MultiThreadTest {

    private static final int MAX_THREADS = 10;

    private static Hashtable<String, Integer> ht = new Hashtable<>();
    private static HashMap<String, Integer> hm = new HashMap<>();
    private static HashMap<String, Integer> hmSyn = new HashMap<>();
    private static Map<String, Integer> hmSyn2 = Collections.synchronizedMap(new HashMap<String, Integer>());
    private static ConcurrentHashMap<String, Integer> chm = new ConcurrentHashMap<>();


		public static void main(String[] args) {

			 ExecutorService es = Executors.newFixedThreadPool(MAX_THREADS);

	         for( int j = 0 ; j < MAX_THREADS; j++ ){
	                 es.execute(new Runnable() {
	                         @Override
	                         public void run() {
	                                 for( int i = 0; i < 1000; i++ ){

	                                         String key = String.valueOf(i);

	                                         ht.put(key, i);
	                                         hm.put(key, i);
	                                         chm.put(key, i);
	                                         hmSyn2.put(key, i);

	                                         synchronized (hmSyn) {
	                                                 hmSyn.put(key, i);
	                                         }
	                                 }
	                         }
	                 });
	         }

	         es.shutdown();
	         try {
	                 es.awaitTermination(Long.MAX_VALUE, TimeUnit.SECONDS);
	         } catch (InterruptedException e) {
	                 e.printStackTrace();
	         }

	         System.out.println("Hashtable size is "+ ht.size());
	         System.out.println("HashMap size is "+ hm.size());
	         System.out.println("ConcurrentHashMap size is "+ chm.size());
	         System.out.println("HashMap(synchronized) size is "+ hmSyn.size());
	         System.out.println("synchronizedMap size is "+ hmSyn2.size());


	//         for( String s : hm.keySet() ){
	//                 System.out.println("["+s+"] " + hm.get(s));
	//         }

		}
}
</code>
</pre>

<pre>
<code>
Hashtable size is 1000
HashMap size is 1075
ConcurrentHashMap size is 1000
HashMap(synchronized) size is 1000
synchronizedMap size is 1000
</code>
</pre>

위의 콘솔 결과를 보듯이 HashMap에 대한 부분은 동기화가 이루어지지 않아 엔트리 사이즈가

비정상적으로 나오는 것을 알 수 있습니다.

하지만 HashMap을 쓰더라도 synchronized 블록을 선언해 주면 정상으로 동작을 합니다.

따라서 동기화 이슈가 있다면 일반적인 HashMap을 쓰지 말거나 쓰더라도 동기화를 보장하는

HashMap 콜렉션 또는 synchronized 키워드를 이용해 동기화 처리를 반드시 해주는 것이 좋아보입니다.


## 참고한 자료

* http://d2.naver.com/helloworld/831311

* http://jdm.kr/blog/197

* http://darksilber.tistory.com/entry/HashMap-HashTable-HashSet-%EC%9D%98-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EC%99%B8-%EA%B8%B0%ED%83%80
