---
title: 선택 정렬 알고리즘 (Selection Sort Algorithm)
subtitle: 알고리즘 및 자료구조
catalog: true
tags:
  - Algorithm
catagories:
  - Algorithm
date: 2017-05-12 20:26:15
header-img:
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 선택 정렬 알고리즘에 관하여 정리해보는 시간을 가지려 합니다.

## 선택 정렬 알고리즘 이란 (Selection Sort Algorithm)?

가장 작은 숫자를 선택해서 제일 앞으로 보내기! [오름차순]

**선택 정렬의 장점**

* 데이터의 양이 적을 때 좋은 성능을 나타냄.

* 작은 값을 선택하기 위해서 비교는 여러번 수행되지만 교환횟수가 적다.

**선택 정렬의 단점**

* 100개 이상의 자료에 대해서는 속도가 급격히 떨어져 적절히 사용되기 힘들다.

**수행 과정 (프로세스)**

1. 주어진 데이터 중 최소값을 찾는다.

2. 최소값을 맨 앞에 위치한 값과 교환한다.

3. 정렬된 데이터를 제외한 나머지 데이터를 같은 방법으로 정렬.

선택 정렬 알고리즘은 n-1개, n-2개, n-3개,...  1개씩 비교를 반복하기 때문에

배열이 어떻게 되어있던지간에 전체 비교를 진행하므로 **시간복잡도는 O(n^2)** 이다.

## 코드

자바로 짜본 선택정렬은 아래코드와 같습니다.

<pre>
<code>
public class SelectionSort {

  public void sort(int[] data){
      int size = data.length;
      int min; //최소값을 가진 데이터의 인덱스 저장 변수
      int temp;

      for(int i=0; i<size-1; i++){

      	min = i; // 0   1   2   3

          for(int j=i+1; j<size; j++){ // j --> 1,2,3,4   2,3,4   3,4,4
              if(data[min] > data[j]){
                // min 은 가장 작은 숫자의 위치
              	min = j;
              }
          }

          // 최소값을 맨 앞에 위치한 값과 교환  
          temp = data[min];    
          data[min] = data[i];
          data[i] = temp;   
      }
  }

  public static void main(String[] args) {

  	SelectionSort selection = new SelectionSort();

        int data[] = {66, 10, 1, 99, 5};

        selection.sort(data);

        for(int i=0; i<data.length; i++){
            System.out.print(data[i]+" ");
        }
  }
}
</code>
</pre>

## 결과

**수행과정**

```
i = 0 일 때 {1,10,66,99,5}
i = 1 일 때 {1,5,66,99,10}
i = 2 일 떄 {1,5,10,99,66}
i = 3 일 때 {1,5,10,66,99}
```

**결과**

```
1,5,10,66,99
```

**Tip: 내림차순은 if 문에서 아래와 같이 부등호만 반대로 바꿔주면 끝!**

```
if(data[min] < data[j]){
  // min 은 가장 큰 숫자의 위치
  min = j;
}

결과

99 66 10 5 1
```
