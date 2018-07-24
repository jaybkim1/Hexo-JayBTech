---
title: 자주 사용하는 PHP 유효성 체크
subtitle: 유효성 검사
catalog: true
tags:
  - PHP
catagories:
  - PHP
date: 2017-07-05 22:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 제가 지금까지 개발하면서 PHP로 각종 유효성 체크를 할 때 사용했던 함수나 정규표현식을 기록해놓기 위해

정리해보려고 합니다. 매번 구글링을 하면서 사용하기엔 번거롭기 때문이지요.

제 블로그에 모아놓으면 나중에 실무에서 사용하게 될 때 편하지 않을까 싶기도 하구요.

일단, 정규표현식의 개념부터 한번 집고 넘어갈겸해서 정규표현식이 무엇인지, 언제 사용되는지에 대해서 먼저

알아보도록 하겠습니다.

## 정규표현식의 정의와 사용 목적 (Regular Expression)

생활코딩에서 egoing 님이 잘 정리해주셨네요.

> 정규 표현식은 문자열을 처리하는 방법 중의 하나로 특정한 조건의 문자를 검색하거나 치환하는 과정을 매우 간편하게
  처리할 수 있도록 하는 수단이다.

말 그대로 특정한 조건의 문자를 검색하거나 치환하는 겁니다.

예를 들어, 문장중에 영어만 추출하거나 한글만 추출하거나 또는 특수문자가 중간에 끼어있다면 그 특수문자를

제거하고 다른 특수문자로 치환한다거나 할때 사용합니다.

이해하셨나요?

[생활코딩으로 바로가기](https://opentutorials.org/module/6/5141)


## PHP 에서 사용해본 각종 예외처리


### 영어와 한글 길이 제한두기

[strlen() 함수](http://php.net/manual/kr/function.strlen.php) 를 이용하면 됩니다.

> 문자열 길이를 얻습니다 (PHP 4, PHP 5, PHP 7)

<code>
strlen() 함수를 이용하면 영어 같은 경우는 한 알파벳을 1 로 처리하지만 한글은 한글자당 3 으로 처리합니다.
</code>

예를 들어, 한글을 두글자나 세글자로만 가능하게 처리를 해야 된다고 할 경우 아래와 같이 처리하면 됩니다.

<code>
if (5 < strlen($Hangul) && strlen($Hangul) < 10) {
  // Code...
}
</code>

### 한국식 생년월일 포맷 형식에 맞게 처리하기

[preg_match()](http://php.net/manual/kr/function.preg-match.php) 를 사용하면 됩니다.

> 정규표현식 매치를 수행 (PHP 4, PHP 5, PHP 7)

예를 들어, 생년월일의 포맷 형식이 **yyyy-mm-dd** 로 되어 있을 경우 아래와 같이 처리하면 됩니다.

<code>
if (preg_match("/^[0-9]{4}-(0[1-9]|1[0-2])-(0[1-9]|[1-2][0-9]|3[0-1])$/",$birthday)) {
  // Code...
}
</code>

### 영어 알파멧만 가능하게끔 처리하기

이것도 역시 preg_match() 함수를 사용하면 됩니다.

<code>
if (preg_match("/[a-zA-Z]/",$variable)){
  // Code...
}
</code>

### 한글만 가능하게끔 처리하기

이것도 역시 preg_match() 함수를 사용하면 됩니다.

<code>
if ("/[\xA1-\xFE][\xA1-\xFE]/", $variable){
  // Code...
}
</code>

### 위치(위도,경도)를 위도와 경도로 처리하기

위치에 위도와 경도를 같이 저장해놨을 경우 분리해주는 부분 역시 php에서 제공하는

preg_match() 함수로 처리가 가능합니다.

<code>
preg_match('/([0-9.-]+).+?([0-9.-]+)/', $location, $matches);
$latitude=(float)$matches[1];
$longitude=(float)$matches[2];
</code>

### 생년월일로 나이 구하기

<code>
$birthday = "19900701";

$birthday = date("Y", strtotime($birthday)); // 생년
$currentyear = date("Y"); // 현재년도
$age = $nowyear-$birthday+1;
</code>

### Haversine Formula 를 이용하여 두 지점의 거리 계산하기

<code>
function haversineGreatCircleDistance($latitudeFrom, $longitudeFrom,
  $latitudeTo,$longitudeTo, $earthRadius)
{
  $latFrom = deg2rad($latitudeFrom);
  $lonFrom = deg2rad($longitudeFrom);
  $latTo = deg2rad($latitudeTo);
  $lonTo = deg2rad($longitudeTo);

  $latDelta = $latTo - $latFrom;
  $lonDelta = $lonTo - $lonFrom;

  $angle = 2 * asin(sqrt(pow(sin($latDelta / 2), 2) +
    cos($latFrom) * cos($latTo) * pow(sin($lonDelta / 2), 2)));

  return intval($angle * $earthRadius / 1000) ; // meter 에서 km 로 변환
}
</code>

### 2개의 배열(array) 안에 있는 값(values)들을 비교하기

예를 들어, 아래와 같이 2개의 array 가 있다고 가정해보겠습니다.

이땐 [array_intersect() 함수](http://php.net/manual/kr/function.array-intersect.php )를 사용합니다.

> 배열의 교집합을 계산  (PHP 4, PHP 5, PHP 7)

<code>
$arr1 = array('banana','apple','watermelon');
$arr2 = array('apple','orange','banana');


$chk = array_intersect($arr1, $arr2);
if (count($chk) > 0) {
    var_dump($chk);
    //there is at least one equal value
}
</code>
