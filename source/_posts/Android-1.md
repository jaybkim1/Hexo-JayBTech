---
title: XML과 JSON
subtitle: 데이터 파싱시 사용되는 텍스트 포맷형식인 XML과 JSON
catalog: true
tags:
  - Android
catagories:
  - Android
date: 2017-04-30 21:26:15
header-img:
comments: true
---


## 들어가기에 앞서...

이 포스팅에서 다룰 주제는 XML과 JSON 입니다.

XML 과 JSON 의 개념은 한국관광공사 오픈 API를 이용해 음식점 데이터를 파싱해서 제가 구축해놓은 DB에 그 데이터들을 넣으면서

배웠던 개념이지만 막상 설명을 하려니 머뭇거리게 되어 정리해보려 합니다.

## XML 과 JSON 은 언제 사용 할까?

XML 과 JSON 은 뭘까? (아래 자세히 정리)

> 서로 다른 언어들간에 데이터를 주고 받는 여러 방법이 있는데 대표적인 것이 XML인데, XML은 문법이 복잡하고,
엄격한 표현규칙으로 인해서 json 대비 데이터의 용량이 커진다는 단점이 있다.
즉, XML과 JSON 둘다 데이터를 담는 텍스트 포멧이라는 겁니다.
그럼 각각 어떻게 다른지 알아 보도록 합시다.

데이터를 보낼때 쓰는 텍스트 포맷 형식이라고 하면 잘 이해가 되지 않는 분들이 있을 수 있습니다.

왜 데이터를 구조화할까요?

*그 이유는 시스템과 시스템간의 데이터를 교환하기 위해서 입니다.*

DB, 웹 페이지, 안드로이드와 같이 한 시스템에서 다른 시스템으로 데이터를 송/수신할 때 데이터가 구조화되어 있어야 합니다.

처음에는 데이터를 바이너리 형태로 송/수신을 했는데, 운영 체제마다 다른 인코딩 방식과 개발 언어마다 다른 자릿수 표현방식으로 인해

여간 불편함 점이 한둘이 아니였답니다......

그리하여 XML 포맷 형식이 1996년에 나오게 되었고 시스템간의 통신은 보다 쉬워졌다고 합니다.

하지만 XML 을 사용하다 보니 개선해야 될 사항이 여러가지가 발견된겁니다...

*바로 tag 속성의 반복이지요. (사용해보시면 알게 됩니다)*

XML의 tag 구조를 개선하기위해 JSON 포맷 형식이 1999년 12월에 나오게 됩니다.

저는 음식검색 어플을 개발할때 XML 과 JSON 을 이용하여 대량의 데이터를 가져오면서 엄청난 삽질을 했던 기억이 납니다 ㅜㅜ

XML 형식으로 된 대량의 데이터를 안드로이드로 가져와보고, JSON 형식의 된 데이터도 가져와보고.

XML 의 데이터를 JSON 으로,
JSON 형식으로된 데이터를 XML 로 변환도 해보면서 개념을 이해했던 기억이 납니다.

시간이 지나니 개념 설명에 있어 부족한 느낌이 들어 오늘 한번 이 포스팅에 정리해보려고 합니다.


## XML (Extensible Markup Language) 이란?

XML은 HTML과 매우 비슷한 문자 기반의 마크업 언어(text-based markup language)입니다.

이 언어는 사람과 기계가 동시에 읽기 편한 구조로 되어 있습니다.

**XML은 HTML처럼 데이터를 보여주는 목적이 아닌, 데이터를 저장하고 전달할 목적으로만 만들어졌습니다.**

또한, XML 태그는 HTML 태그처럼 미리 정의되어 있지 않고, 사용자가 직접 정의할 수 있습니다.

포맷은 아래와 같이 생겼습니다.

[1] 간단한 구조

```
<dog>
    <name>식빵</name>
    <family>웰시코기<family>
    <age>1</age>
    <weight>2.14</weight>
</dog>
```

[2] 좀 더 복잡한 구조

```
<widget>
    <debug>on</debug>
    <window title="Sample Konfabulator Widget">
        <name>main_window</name>
        <width>500</width>
        <height>500</height>
    </window>
    <image src="Images/Sun.png" name="sun1">
        <hOffset>250</hOffset>
        <vOffset>250</vOffset>
        <alignment>center</alignment>
    </image>
    <text data="Click Here" size="36" style="bold">
        <name>text1</name>
        <hOffset>250</hOffset>
        <vOffset>100</vOffset>
        <alignment>center</alignment>
        <onMouseUp>
            sun1.opacity = (sun1.opacity / 100) * 90;
        </onMouseUp>
    </text>
</widget>
```

XML 에 대해 좀 더 자세하게 알고 싶다면 https://www.w3schools.com/xml/xml_whatis.asp 에 있는 내용을 읽어보도록 해요.


## JSON (JavaScript Object Notation) 이란?

JSON은 경량의 데이터 교환 형식으로 JavaScript에서 숫자와 배열등을 만드는 형식을 차용해서 이것을 다른 언어에서도 사용할 수 있도록 한 텍스트 형식이다.

공식홈페이지: http://www.json.org/

포맷은 아래와 같이 생겼습니다.

[1] 간단한 구조

```
{
    "name": "식빵",
    "family": "웰시코기",
    "age": 1,
    "weight": 2.14
}
```

[2] 좀 더 복잡한 구조

```
{"widget": {
    "debug": "on",
    "window": {
        "title": "Sample Konfabulator Widget",
        "name": "main_window",
        "width": 500,
        "height": 500
    },
    "image": {
        "src": "Images/Sun.png",
        "name": "sun1",
        "hOffset": 250,
        "vOffset": 250,
        "alignment": "center"
    },
    "text": {
        "data": "Click Here",
        "size": 36,
        "style": "bold",
        "name": "text1",
        "hOffset": 250,
        "vOffset": 100,
        "alignment": "center",
        "onMouseUp": "sun1.opacity = (sun1.opacity / 100) * 90;"
    }
}}  
```

JSON 에 대해 좀 더 자세하게 알고 싶다면 ![여기 W3SCHOOLS](https://www.w3schools.com/js/js_json_intro.asp)에 있는 내용을 읽어보도록 해요.

## JSON 과 XML 의 공통점

*  둘 다 데이터를 저장하고 전달하기 위해 고안되었습니다.

*  둘 다 기계뿐만 아니라 사람도 쉽게 읽을 수 있습니다.

*  둘 다 계층적인 데이터 구조를 가집니다.

*  둘 다 다양한 프로그래밍 언어에 의해 파싱될 수 있습니다.


## JSON 과 XML 의 차이점

*  JSON은 종료 태그를 사용하지 않습니다. (즉, 포맷형식이 다릅니다)

*  JSON의 구문이 XML의 구문보다 더 짧습니다.

*  데이터를 파싱할때 JSON 형식으로된 데이터가 XML 보다 더 빨리 읽고 쓸 수 있습니다. (속도면에선 크게 차이가 나지 않습니다)

*  XML은 배열을 사용할 수 없지만, JSON은 배열을 사용할 수 있습니다.


## JSON 의 사용성

XML 문서는 XML DOM(Document Object Model)을 이용하여 해당 문서에 접근합니다.
하지만 JSON은 문자열을 전송받은 후에 해당 문자열을 바로 파싱하므로, XML보다 더욱 빠른 처리 속도를 보여줍니다.
따라서 HTML과 자바스크립트가 연동되어 빠른 응답이 필요한 웹 환경에서 많이 사용되고 있습니다.

직접 안드로이드에서 사용해본 결과 JSON 이 훨씬 편하다는걸 느꼈습니다.
JSON 을 사용할때에도 여러가지의 형식 (object, array, value ...) 들이 있기 때문에 상황에 따라
필요한 형식으로 사용하면 됩니다.

## XML 이나 JSON 에 대해 좀 더 알아보고 싶다면...

* [생활코딩] : [https://opentutorials.org/course/49/3473](https://opentutorials.org/course/49/3473)

* [JSON Editor Online] : [http://jsoneditoronline.org/](http://jsoneditoronline.org/)

* [JSONmate] : [http://jsonmate.com/](http://jsonmate.com/)
