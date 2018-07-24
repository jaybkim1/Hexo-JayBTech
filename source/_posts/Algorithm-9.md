---
title: 자바에서 sort()로 정렬하는 방법
subtitle: 알고리즘 및 자료구조
catalog: true
tags:
  - Algorithm
catagories:
  - Algorithm
date: 2017-06-13 22:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 자바에서 sort() 함수를 이용하여 여러가지로 정렬하는 방법에 대해 정리하는 시간을 가지려고 합니다.

## 들어가기에 앞서...

자바에서 정렬은 기본적으로 sort() 함수로 가능합니다.

정렬 알고리즘은 기초적이면서도 많이 사용되기 때문에 제대로 알고 적재적소에 사용하면 좋습니다.

## int 배열을 정렬해보는 간단한 예제

<pre>
<code>
int[] array = new int[] {9,10,2,1,4,3,5,7,6,8};

Arrays.sort(array);

for (int i = 0; i < array.length; i++) {
    System.err.print(array[i] + " ");
}
</code>
</pre>

자바는 위와 같이 정렬 함수를 제공한다. int 형 외에도 double, char, string 에 대해서도 적용이 가능하다.

int 형의 default 정렬 (natural ordering) 이 오름차순이다.

따라서, 결과값은 아래와 같다.

```
1,2,3,4,5,6,7,8,9,10
```

String 형으로 된 배열도 정렬해보자

## String 배열을 정렬해보는 간단한 예제

<pre>
<code>
String[] array = new String[] {"f","b","a","d","c","e","g"};

Arrays.sort(array);

for (int i = 0; i < array.length; i++) {
    System.err.print(array[i] + " ");
}
</code>
</pre>

String 형의 default 정렬은 알파벳순이다.

따라서, 결과값은 아래와 같다.

```
a,b,c,d,e,f,g
```

## Arrays.sort() / Collections.sort() 는 기본적으로 어떤 방법으로 정렬할까?

**sort() 를 실행하는 순간 내부적으로 compareTo() 라는 과정을 거쳐서 그 메소드의 내용에 따라 정렬을 한다.**

이때, 이 비교를 해주는 compareTo() 는 java.langComparable<T> 인터페이스에서 제공하기 때문에

커스텀을 하여 원하는대로 정렬을 할 수 있다.

## java.lang.Comparable<T> interface

```
int compareTo(T o) // Returns a negative integer, zero, or a positive integer
                   // as this object is less than, equal to, or greater than the given object
```

<pre>
<code>
Parameter o - 비교할 객체 (비교대상)

Return - int 값 (음수, 0, 양수)

음수 : 비교대상보다 작음

 0  : 비교대상과 같음

양수 : 비교대상보다 큼
</code>
</pre>

## 정렬 방식 직접 구현하는 방법

위에서 말한 것으로 개발자가 직접 정렬 방식을 커스텀하고 싶다면?

* java.util.Comparator<T> interface 를 implements 하는 클래스를 구현한다.

* compareTo() 메소드를 오버라이드 한다.


## 소스코드

아래 소스코드는 androidVersion 이라는 배열안에 안드로이드 버전이름과 버전 숫자를 넣었다.

이를, default 정렬인 오름차순으로 정렬한다.

```
import java.util.Arrays;
import java.util.Comparator;

public class AndroidVersion implements Comparable<AndroidVersion>{

	public String name;
	public int versionNum;

	public AndroidVersion(String name, int versionNum){
		this.name = name;
		this.versionNum = versionNum;
	}

	@Override
	public int compareTo(AndroidVersion other) {
		return name.compareTo(other.name);
	}

    // 이름 (알파벳순) 으로 비교
  	public static Comparator<AndroidVersion> nameComparator = new Comparator<AndroidVersion>(){                               
          public int compare(AndroidVersion name1, AndroidVersion name2){
              return name1.name.compareTo(name2.name);
          }
      };

    // 안드로이드 버전 (숫자 오름차순) 으로 비교
    public static Comparator<AndroidVersion> versionComparator = new Comparator<AndroidVersion>(){       
        public int compare(AndroidVersion versionNum1, AndroidVersion versionNum2){
            return versionNum1.versionNum - versionNum2.versionNum;
        }
    };

	public static void main(String[] args) {

		AndroidVersion [] androidVersion = new AndroidVersion[6];

		androidVersion[0] = new AndroidVersion("HoneyComb", 3);
		androidVersion[1] = new AndroidVersion("Marshmallo", 6);
		androidVersion[2] = new AndroidVersion("Lollipop", 5);
		androidVersion[3] = new AndroidVersion("Kitkat", 4);
		androidVersion[4] = new AndroidVersion("Nougat", 7);
		androidVersion[5] = new AndroidVersion("Oreo", 8);

		Arrays.sort(androidVersion, versionComparator);

    // 출력부분
		for (int i = 0; i < androidVersion.length; i++) {
			System.out.print(androidVersion[i].name + " " + androidVersion[i].versionNum+" ");
			System.out.println();
		}

	}
}
```

결과는 아래와 같습니다.

## 결과

```
HoneyComb 3
Kitkat 4
Lollipop 5
Marshmallo 6
Nougat 7
Oreo 8
```

오름차순으로 정렬된거 보이시나요?

그럼, 내림차순은 어떻게 할까요?

이 부분을

```
// 안드로이드 버전 (숫자 오름차순) 으로 비교
public static Comparator<AndroidVersion> versionComparator = new Comparator<AndroidVersion>(){       
    public int compare(AndroidVersion versionNum1, AndroidVersion versionNum2){
        return versionNum1.versionNum - versionNum2.versionNum;
    }
};
```

아래와 같이 변경해주시면 됩니다.

```
// 안드로이드 버전 (숫자 오름차순) 으로 비교
public static Comparator<AndroidVersion> versionComparator = new Comparator<AndroidVersion>(){       
    public int compare(AndroidVersion versionNum1, AndroidVersion versionNum2){

      if (versionNum1.versionNum > versionNum2.versionNum) {
        return -1; // 비교대상보다 작을경우 음수 return
      }else if (versionNum1.versionNum < versionNum2.versionNum) {
        return 1; // 비교대상보다 클 경우 양수 return
      }else{
        return 0; // 비교대상과 같을 경우 0 return
      }
    }
};
```

## 결과

```
Oreo 8
Nougat 7
Marshmallo 6
Lollipop 5
Kitkat 4
HoneyComb 3
```

오름차순 내림차순 뿐만 아니라 원하는 정렬방식이 있다면 그에 맞게 저 메소드 안을 구현하면 되겠죠?
