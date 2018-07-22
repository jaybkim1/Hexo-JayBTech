---
title: 구글 기술면접 문제에도 나온 Anagram
subtitle: 알고리즘 및 자료구조
catalog: true
tags:
  - Algorithm
catagories:
  - Algorithm
date: 2017-06-11 22:26:15
header-img:
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 구글 기술면접에도 나왔던 문제인 Anagram 문제에 관하여 정리해보는 시간을 가지려 합니다.

## 들어가기에 앞서...

구직활동을 하면서 어느 기업에서 코딩테스트를 보게 되었는데 Anagram 문제를 풀게 되었습니다.

평소 알고리즘 문제를 많이 풀어보지도 않았고 알고리즘에 대해 큰 이해가 없었습니다.

그냥 아주 기본적인 기본문제들만 풀어본 정도 ? 였지요...

Anagram 문제를 풀게 됬을 때 주어진 시간안에 풀긴 풀었지만 알고보니 가장 원초적인 방식으로 풀게 되었습니다.

두 문자열을 알파벳으로 쪼개어 array에 담고 2 중 for 문을 돌려 검사하는 방식으로 하다보니

시간복잡도가 O(n2) 이 나오게끔 풀었답니다.

집에 와서 열심히 구글신과 스택오버플로우신님을 통해 다른 사람들이 작성한 다양한 방법들을 보며 리뷰를 하였고

알고리즘에 대한 이해와 다양한 방법들이 존재한다는 걸 배웠답니다.

배운건 정리를 해봐야 머릿속에 잘 남겠죠?

그럼 Anagram 이 뭔지 부터 한번 알아봅시다.

## Anagram 이란?

서로 다른 두 문자열이 있을때 두 문자열의 알파벳을 재배열하였을때 같은 단어 혹은 문장.

예를 들어,

along 과 laong 은 Anagram 입니다.

table 과 abtel 은 Anagram 입니다.

문제 !

> Anagram 인지 확인하는 프로그램을 만드시오. (Anagram 일 경우 true, 아닐 경우 false 를 리턴)

전 JAVA 를 주 언어로 사용하고 있기에 JAVA 로 한번 짜보겠습니다.

일단 프로세스가 어떻게 될 지 정리해보고 프로그램을 만들어보겠습니다.

## 프로세스 (Anagram 을 처음 접했을때)

이 프로세스는 제가 실제로 이 문제를 접했을때 생각했던 프로세스 입니다.

1. 글자 길이를 먼저 비교한다.

2. 대소문자를 구분하지 않게 한다.

3. 첫번째 단어 String 을 알파벳 char 형태로 쪼개어 array 에 담는다.

4. 두번째 단어 String 을 알파벳 char 형태로 쪼개어 array 에 담는다.

5. 첫번째 array 를 for 문을 돌려 두번째 array[0 ~ n]에 같은 문자가 있는지 확인한다.

위와 같은 방식으로 했을 경우 시간복잡도가 for문이 2개가 중첩되기 때문에 O(n2) 가 나오게 됩니다.

## 프로세스 (Anagram 문제 검토 후)

1. 글자 길이를 먼저 비교한다

2. 대소문자 무시를 위해 문자열 대문자를 소문자로 변환한다.

3. 문자열을 char[] 형태로 변환한다. 이때, String 의 **toCharArray()** 메소드를 활용한다.

4. 문자열 내 알파벳 정렬을 한다. 이때, **Arrays.sort()** 메소드를 활용한다.

5. char[] 형태를 String 형태로 변환한후 **equals()** 메소드로 문자열을 비교한다.

위와 같은 방식은 기본적으로 유사한 문제를 접해보면서 bold 로 된 3개의 메소드를 활용해보았을때 생각할 수 있는 프로세스다.

맞다, 많은 문제를 접해보고 다른 사람이 작성한 코드를 봐야 된다.

위에서 사용된 3개의 메소드가 각각 어떤 역할을 하는지 자세히 알고 싶다면 구글링을 해보길 바랍니다.

## 아래 소스코드에서 사용된 메소드 미리 파악하기

* replaceAll(): 공백 제거할때 사용되는 함수 trim() 과는 차이가 있다. 아래 블로그 참조

  http://all-record.tistory.com/87

* toCharArray(): 문자 배열로 변환해주는 함수

  http://caronjuni.tistory.com/entry/toCharArray

* toLowerCase(): 문자열을 소문자로 변환해주는 함수

  https://opentutorials.org/course/50/99

* Arrays.sort(): 입력된 배열을 정렬해주는 함수

  http://emflant.tistory.com/210


## 자바로 짜본 Anagram 프로그램

<pre>

Anagram 인지 확인하는 프로그램을 만드시오. (Anagram 일 경우 true, 아닐 경우 false 를 리턴)

<code>
import java.util.Arrays;
import java.util.Scanner;

public class AnagramProgram {

	public static boolean isAnagram(String s1, String s2){

				//공백을 전부 다 제거한다
				s1 = s1.replaceAll("\\s", "");
				s2 = s2.replaceAll("\\s", "");

			  // 두 문자열의 길이를 미리 체크
        if ( s1.length() != s2.length() ) {
            return false;
        }

				// 두 단어다 소문자로 변환 후 char 형식으로 변환해주는 toCharArray() 메서드 활용
        char[] c1 = s1.toLowerCase().toCharArray();
        char[] c2 = s2.toLowerCase().toCharArray();

        // Arrays.sort() 메서드를 활용한 알파벳 정렬 (알파벳순으로 정렬)
        Arrays.sort(c1);
        Arrays.sort(c2);

        // char[] --> String 으로 변환
        String sc1 = new String(c1);
        String sc2 = new String(c2);

        // 문자열 비교
        return sc1.equals(sc2);
	}

	public static void main(String[] args) {

		AnagramProgram anagram = new AnagramProgram();

		String first;
		String second;

		Scanner input = new Scanner(System.in);

		// 문장을 받을 수도 있기에 nextLine() 활용
		System.out.print("첫번째 단어 입력:");
		first = input.nextLine();

		System.out.print("두번째 단어 입력:");
		second = input.nextLine();

		System.out.println("Anagram ? "+anagram.isAnagram(first,second));
	}
}
</code>

</pre>

## 결과

<pre>
<code>
첫번째 단어 입력:ana ls
두번째 단어 입력:naa sl

Anagram ? true
</code>
</pre>

## 다양한 방법

다양한 방법으로 소스코드를 짤 수 있지만 핵심은 동일합니다.

Anagram 의 특성을 먼저 이해하고 그에 따른 프로세스가 있다는 거죠.

다른 사람들이 작성한 소스코드도 참고를 해보면 내가 생각해내지 못했던 다양한 방법들이 존재한다는걸 알 수 있습니다.

* http://javaconceptoftheday.com/anagram-program-in-java/

아래 StackOverflow 에 채택된 해답중 HashMap 을 사용하여 시간복잡도를 O(n) 으로 줄이는 소스코드를 제안한 분도 있군요.

* https://stackoverflow.com/questions/15045640/how-to-check-if-two-words-are-anagrams


## 정리를 끝마치며...

이 문제를 풀면서 또 한번 깨달았습니다.

알고리즘 문제는 많이 풀어봐야 된다는걸...

코딩테스트는 어떤 문제를 접할 지 모릅니다.

개발자로 살아가면서 앞으로 많은 테스트를 보게 될 거라 예상 됩니다.

단순히 코딩테스트를 떠나 앞으로 웹이나 앱을 만들때 다양한 사회적 문제를 풀어나가게 될겁니다.

문제를 어떻게 풀어나갈지에 대한 고민, 프로세스적으로 좀 더 나은 프로세스를 생각할 수 있는 

개발자가 되기 위해 좀 더 노력해야겠다고 다짐합니다.

다음엔 무슨 문제를 풀게 될지 기대되는군요 ㅎㅎ
