---
title: 버블 정렬 알고리즘 (Bubble Sort Algorithm)
subtitle: 알고리즘 및 자료구조
catalog: true
tags:
  - Algorithm
catagories:
  - Algorithm
date: 2017-05-13 20:26:15
header-img:
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 버블 정렬 알고리즘에 관하여 정리해보는 시간을 가지려 합니다.


## 버블 정렬 알고리즘이란? (Bubble Sort Algorithm)

옆에 있는 수를 비교해서 큰 수를 뒤로 보내는 알고리즘

(매번 연속된 두개의 인덱스 값을 비교하여 정한 기준의 값을 뒤로 넘겨 정렬하는 방법)

**중요포인트(기본적인 개념)**

* 한번 사이클이 돌때마다 가장 큰 값이 맨 뒤로 간다는 점만 기억하라!

* 계속해서 사이클이 돌면서 정렬이 된다고 보면 된다.

**버블 정렬의 장점**

* 알고리즘이 단순하기 때문에 자주 사용된다.

**버블 정렬의 단점**

* 시간복잡도가 n의 제곱으로 늘어나기 때문에 시간이 굉장히 오래 걸린다.

**수행 과정 (프로세스)**

* 배열의 인접한 두 수 (n번과 n+1번)를 비교하여 n번이 더 크면 둘의 위치를 바꾼다.

* 즉, 더 큰값을 뒤로 돌린다.

* 이를 반복하여 가장 큰값을 맨뒤로 보내고 이를 처음부터 마지막의 앞까지 반복하여 정렬을 진행한다.

버블 정렬 알고리즘은 1부터 비교를 시작하여 n-1개, n-2개, n-3,... 1개씩 비교를 반복하여

선택 정렬과 같이 배열이 어떻게 되어있던지간에 전체 비교를 진행해야하므로 **시간복잡도는 O(n^2)이다.**

## 코드

**자바로 짜본 버블정렬은 아래코드와 같습니다.**

<pre>
<code>
public class BubbleSort {

	public void sort(int[] data){

		int size = data.length; // 배열에 있는 데이터 길이

		int i,j,temp;

		for (i = 0; i < size; i++) // 0 ~ 9
		{
			for (j = 0; j < (size -1) - i; j++) // (0 ~ 8) - i
			{
        // 핵심!
        // 다음 인덱시에 위치한 데이터와 비교하여 데이터가 더 크면 자리교환을 한다.
				if (data[j] > data[j+1])
				{
					temp = data[j];
					data[j] = data[j+1];
					data[j+1] = temp;
				}
			}
		}
	}

	public static void main(String[] args) {

		BubbleSort bubble = new BubbleSort();

		int[] data = {10,1,4,5,3,6,2,7,9,8};

		bubble.sort(data);

		for (int i = 0; i < data.length; i++) {
			System.out.print(data[i]+" ");
		}
	}
}
</code>
</pre>


## 결과

**핵심 부분**

```
if (data[j] > data[j+1])
{
  temp = data[j];
  data[j] = data[j+1];
  data[j+1] = temp;
}
```

**결과**

```
1 2 3 4 5 6 7 8 9 10
```
