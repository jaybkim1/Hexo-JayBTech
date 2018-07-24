---
title: 삽입 정렬 알고리즘 (Insertion Sort Algorithm)
subtitle: 알고리즘 및 자료구조
catalog: true
tags:
  - Algorithm
catagories:
  - Algorithm
date: 2017-05-14 20:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 삽입 정렬 알고리즘에 관하여 정리해보는 시간을 가지려 합니다.

## 삽입 정렬 알고리즘이란? (Insertion Sort Algorithm)

적절한 위치에 데이터 삽입하기

**중요포인트 (기본적인 개념)**

* 새로운 데이터를 기존의 데이터들 사이에 삽입한다는 것!

예를 들어,

5,4,3,2,1 과 같은 배열이 존재한다고 하자.

5,4,3,2,1
  ↑

두번째 index를 기준으로

이전 숫자와 대소비교를 한다.

그래서 자기의 위치를 찾는다.

**STEP 01.**

4,5,3,2,1

이렇게 정렬이 됩니다.

**STEP 02.**

그다음에는 3부터 시작하게 됩니다.

4,5,3,2,1
    ↑

5가 3보다 크므로 3이 들어갈 위치를 찾습니다.

3과 5비교 하여 정렬을 합니다. 4,3,5,2,1

그리고 3과 4를 비교하여 정렬을 합니다.

**결과**

결과 3,4,5,2,1

**수행 과정 (프로세스) 정리**

* 삽입 정렬은 두번째 인덱스에서 부터 시작한다.
  현재 인덱스는 별도의 std 라는 변수에 저장해주고, 비교 인덱스를 현재 인덱스 -1로 잡는다.

* 별도로 저장해 둔 삽입을 위한 변수와 비교 인덱스의 배열 값을 비교한다.

* 삽입 변수의 값이 더 작으면 현재 인덱스로 비교 인덱스의 값을 저장해주고 비교 인덱스를 -1 하여 비교를 반복한다.

* 만약 삽입 변수가 더 크면, 비교 인덱스 +1 에 삽입 변수를 저장한다.

삽입 정렬 알고리즘 또한 Big-O 표기법의 경우 n-1개, n-2개, n-3개,... 1개씩 비교를 반복하여

**시간복잡도는 O(n^2)이지만, 이미 정렬되어 있는 경우에는 한번씩 밖에 비교를 하지 않으므로 O(n)이다.**

배열 상황에 따라 다르다는 얘기다.

## 코드

**자바로 짜본 삽입정렬은 아래코드와 같습니다.**

<pre>
<code>
public class InsertionSort {

	public void sort(int[] data) {

		int size = data.length;

		for (int i = 1; i < size; i++) {

			int std = data[i];  // 기준
			int j = i - 1;   // 비교할 대상

			while (j >= 0 && data[j] > std) { // 처음 j = -1 이 못들어오게 방지
				data[j + 1] = data[j];   // 비교대상이 큰 경우 오른쪽으로 밀어냄
				j--;
			}
			data[j + 1] = std;  // 기준값 저장
		}
	}

	public static void main(String[] args) {

		InsertionSort insertion = new InsertionSort();

		int[] data = {5,3,6,1,2,10,9,7,4,8};

		insertion.sort(data);

		for (int i = 0; i < data.length; i++) {
			System.out.print(data[i] + " ");
		}
	}
}
</code>
</pre>


## 결과

**핵심 부분**

```
while (j >= 0 && data[j] > std) { // 처음 j = -1 이 못들어오게 방지
	data[j + 1] = data[j];   // 비교대상이 큰 경우 오른쪽으로 밀어냄
	j--;
}
data[j + 1] = std;  // 기준값 저장
```

**결과**

```
1 2 3 4 5 6 7 8 9 10
```
