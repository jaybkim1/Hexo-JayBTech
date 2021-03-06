---
title: REST가 모야? REST API?
subtitle: REST의 개념과 RESTful한 아키텍처 설계에 대한 이해
catalog: true
tags:
  - Web
catagories:
  - Web
date: 2017-04-28 21:26:15
header-img:
comments: true
---


## 들어가기 전에...

최근들어 채용공고를 보면 지원자격에 RESTful API 가 종종 들어가 있는걸 보고 RESTful API에 맞게 설계했나요? 라는 질문도 면접에서 심심찮게 들어본 경험이 있다.

웹 개발 당시 RESTful 하게 아키텍처를 설계하기 위해 많은 글을 읽고 참고하며 적용을 한다고 했지만 그 당시에도 다른 사람을 가르칠 정도로 개념이 머릿속에 자리잡히진 못했던 것 같다.

시간이 흐르니 설명하기 힘들정도로 개념에 대해 잊어버린 것 같아 정리해볼 겸 구글링을 하던 중 잘 정리해놓은 글이 있어 가져와봤다.

아래 내용은 spoqa 기술 블로그의 2012년도 초에 작성된 [REST 아키텍처를 훌륭하게 적용하기 위한 몇 가지 디자인 팁](https://spoqa.github.io/2012/02/27/rest-introduction.html)의

내용을 참고하여 작성되었습니다.



최근의 서비스/애플리케이션의 개발 흐름은 멀티 플랫폼, 멀티 디바이스 시대로 넘어와 있습니다.

단순히 하나의 브라우저만 지원하면 되었던 이전과는 달리, 최근의 서버 프로그램은 여러 웹 브라우저는 물론이며, 아이폰, 안드로이드 애플리케이션과의 통신에 대응해야 합니다.

그렇기 때문에 매번 서버를 새로 만드는 수고를 들이지 않기 위해선 **범용적인 사용성을 보장하는 서버 디자인** 이 필요합니다.

REST 아키텍처는 Hypermedia API의 기본을 충실히 이행하여 만들고자 하는 **시스템의 디자인 기준을 명확히 확립하고 범용성을 보장** 하게 해줍니다.

이번 글에선 **현대 서비스 디자인을 RESTful하게 설계하는 기초적인 내용** 에 대해 정리하려고 합니다.

## REST란 무엇인가?

REST는 Representational state transfer의 약자로, 월드와이드웹과 같은 분산 하이퍼미디어 시스템에서 운영되는 소프트웨어 아키텍처스타일입니다.

2000년에 Roy Fielding에 의해 처음 용어가 사용되었는데, 이 분은 HTTP/1.0, 1.1 스펙 작성에 참여했었고 아파치 HTTP 서버 프로젝트의 공동설립자이기도 합니다.

REST는 HTTP/1.1 스펙과 동시에 만들어졌는데, HTTP 프로토콜을 정확히 의도에 맞게 활용하여 디자인하게 유도하고 있기 때문에 디자인 기준이 명확해지며,

의미적인 범용성을 지니므로 중간 계층의 컴포넌트들이 서비스를 최적화하는 데 도움이 됩니다. **REST의 기본 원칙을 성실히 지킨 서비스 디자인은 “RESTful 하다.”** 라고 흔히 표현합니다.

무엇보다 이렇게 잘 디자인된 API는 서비스가 여러 플랫폼을 지원해야 할 때, 혹은 API로서 공개되어야 할 때,

설명을 간결하게 해주며 여러 가지 문제 상황을 지혜롭게 해결하기 때문에 (버전, 포맷/언어 선택과 같은) REST는 최근의 모바일, 웹 서비스 아키텍처로서 아주 중요한 역할을 하고 있습니다.


## 중심 규칙

REST에서 가장 중요하며 기본적인 규칙은 아래 두 가지입니다.

* URI는 정보의 자원을 표현해야 한다.
* 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)으로 표현한다.

1번 사용자에 대해 정보를 받아야 할 때를 예를 들면, 아래와 같은 방법은 좋지 않습니다.

```
GET /users/show/1
```

이와 같은 URI 방식은 REST를 제대로 적용하지 않은 구 버전의 Rails에서 흔히 볼 수 있는 URL입니다.

이 URI은 자원을 표현해야 하는 URI에 /show/ 같은 불필요한 표현이 들어가 있기 때문에 적절하지 않습니다.

본다는 것은 GET이라는 HTTP Method로 충분히 표현할 수 있기 때문이죠. 최근의 Rails는 아래와 같이 변경되었습니다.

```
GET /users/1
```

자원은 크게 **Collection** 과 **Element** 로 나누어 표현할 수 있으며,

아래 테이블에 기초한다면 서버 대부분과의 통신 행태를 표현할 수 있습니다.


![rest](https://user-images.githubusercontent.com/20435620/29902278-115dc7f6-8e38-11e7-922a-866f70c05e2b.PNG)


이 외에도 PATCH 라는 HTTP Method에도 주목하시기 바랍니다.

PUT이 해당 자원의 전체를 교체하는 의미를 지니는 대신, PATCH는 일부를 변경한다는 의미를 지니기 때문에 최근 update 이벤트에서 PUT보다 더 의미적으로 적합하다고 평가받고 있습니다.

Rails도 4.0부터 PATCH가 update 이벤트의 기본 Method로 사용될 것이라 예고하고 있습니다.


## 입력 Form은 어떻게 받아오게 하지?

위의 예시를 통해 많은 행태를 표현할 수 있습니다만 새로운 아이템을 작성하거나 기존의 아이템을 수정할 때 작성/수정 Form은 어떻게 제공할지에 대한 의문을 초기에 많이 가집니다.

정답은 Form 자체도 정보로 취급해야 한다는 것입니다. 서버로부터 “새로운 아이템을 작성하기 위한 Form을 GET한다”고 생각하시면 됩니다.

Rails 에선 기본적인 CRUD를 제공할 때 아래와 같은 REST 인터페이스를 구성해줍니다.


![rest1](https://user-images.githubusercontent.com/20435620/29902298-31b4f10a-8e38-11e7-95ae-a4c0ec66b9c3.PNG)


## 모바일 환경에 따라 다른 정보를 보여줘야 한다면?

접속하는 환경에 따라 다른 정보를 보여줘야 할 때가 있습니다. 가령 모바일 디바이스에서 볼 때 다른 사용자 인터페이스를 제공한다든지 하는 경우인데요.

일부 애플리케이션은 독립적인 모바일 웹서비스를 개발한 후 단지 이를 이동시켜주기만 할 때가 있는데, 이는 어떤 경우에 좋지 못한 사용성을 보여줍니다.

모바일 뷰와 일반 웹페이지 뷰의 URI가 달라서 같은 정보를 공유할 때 각 환경에 적절한 디자인과 인터페이스로 보이지 않기 때문입니다.

모바일에서 블로그를 구경하던 도중, 컴퓨터를 이용하고 있는 친구에게 자신이 보고 있는 내용을 보내주고 싶을 때가 있습니다.

티스토리 블로그는 모바일 뷰의 URI가 기존 URI와 달라서, 친구가 해당 URI를 데스크탑에서 열어도 모바일에 최적화된 정보를 받을 수밖에 없게 됩니다.

이 URI를 데스크탑에서 열어보시기 바랍니다.

REST 하게 만든다면 URI는 플랫폼 중립적이어야 하며, 정보를 보여줄 때 여러 플랫폼을 구별해야 한다면 Request Header의 User-Agent 값을 참조하는 것이 좋습니다.

예를 들어 iPhone에서 보내주는 User-Agent 값은 아래와 같습니다.


```
Mozilla/5.0 (iPhone; U; CPU like Mac OS X; en) AppleWebKit/420+ (KHTML, like Gecko) Version/3.0 Mobile/1A543a Safari/419.3
```

대부분 브라우저, OS 플랫폼은 HTTP Request를 보낼 시 보내는 주체에 대한 설명을 User-Agent에 상세하게 포함하여 통신하고 있기 때문에 요청자의 환경을 정확히 알 수 있습니다.


## Ajax와 REST

최근 빠른 속도의 웹서비스를 구현하기 위해 서비스 전체를 Ajax 통신으로 구동되게끔 HTML5 애플리케이션을 만드는 일이 많습니다.

서비스 전체를 Ajax 기반으로 구동되게 개발한다면 중복된 콘텐츠를 여러 번 전달하지 않아도 되고, 브라우저 렌더링 과정이 간소화되므로 더욱 빠른 서비스를 구축할 수 있습니다.

하지만 Ajax 기반의 서비스는 초기에 URL에 관련된 문제가 있어 REST한 서비스를 만들 때 애로사항이 있었습니다

콘텐츠가 바뀌어도 URL은 그대로여서 친구에게 내가 보고 있는 콘텐츠를 보여줄 방법이 불편했기 때문이죠.

최근엔 두 가지 방법으로 이를 보완할 수 있습니다. 첫 번째는 #! 기법으로, 구형 브라우저에서도 # 이하의 URL을 Javascript로 자유자재로 변경할 수 있다는 점을 이용한 방법입니다.

방법은 아래와 같습니다.

Ajax 통신을 통해 이동되는 페이지의 URI는 현재 URI의 #! 이후에 붙인다. 페이지가 처음 열릴 때, #! 이후로 URI가 붙어있다면 해당 URI로 redirect를 해준다.

이와 같은 방법으로 Ajax 서비스를 만들면, 페이지를 이동한 이후에 URL을 친구에게 복사해서 전달해주어도 친구가 내가 보고 있는 콘텐츠를 볼 수 있으며,

구글에서 수집할 때 해당 #! 이하의 URL을 판별해서 제대로 수집해주기 때문에 검색엔진에도 성공적으로 노출될 수 있습니다.

하지만 위 방법의 단점은

1. 상대방이 Javascript를 지원하지 않는 브라우저를 이용하거나 Javascript 기능을 꺼 놓았을 때 제대로 된 콘텐츠를 볼 수 없다는 것이며,

2. URI가 몹시 보기 지저분해진다는 것입니다. 두 번째 방법은 pushState라는 새로운 표준을 이용한 방법으로, javascript의 pushState를 통해

Ajax 통신 후에 변경된 컨텐츠의 URI을 제대로 바꿔줄 수 있습니다.

하지만 최신 표준을 지원하는 브라우저에서만 정상적으로 구동되기 때문에, 하위 호환에 신경을 써야 한다는 단점이 있습니다.

pjax같은 프로젝트들이 하위 호환을 포함하여 이런 구현을 쉽게 하도록 도와주고 있습니다.


## 마치며

REST는 여러 가지 서비스 디자인에서 생길 수 있는 문제를 최소화해주고, HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 함께 가져갈 수 있게 해줍니다.

이번 글에서는 REST하지 않은 서버 설계를 통해 생길 수 있는 실질적인 문제들을 제시하고 REST 아키텍처가 이를 어떻게 해결해주는지 함께 보았습니다.

‘REST가 완전한 정답이냐?’라고 한다면 이에 대해서는 아직 논의가 남아있습니다.

구형 브라우저가 아직 제대로 지원해주지 못하는 부분이 분명히 있으며 (PUT, DELETE를 사용하지 못하는 점, pushState를 지원하지 않는 점)

브라우저를 통해 테스트할 일이 많은 서비스라면 쉽게 고칠 수 있는 URL보다 Header 값은 왠지 더 어렵게 느껴지기도 합니다.

만일, 만들고 있는 서비스의 API가 널리 쓰여야 한다면 REST를 완전하게 적용한 디자인이 더 독이 될 수 있습니다.

많은 개발자는 별로 똑똑하지 못하며, HTTP 프로토콜에 대한 이해가 부족하여서 API가 어렵게 느껴질 수 있기 때문입니다.

그러므로 Google을 포함한 많은 기업의 서비스 API가 REST 스타일을 완전히 따르고 있진 않습니다.

하지만 그럼에도 REST가 중요한 점은, 이를 제대로 구현하는 것이 서비스 디자인에 큰 부가이익을 가져다 줄 수 있으며,

많은 현대의 API들이 REST를 어느 정도로 충실하게 반영하느냐를 고민할 뿐이지 REST를 중심으로 디자인되고 있다는 점은 분명하기 때문입니다.

REST를 얼마나 반영할 지는 API가 어떤 개발자를 범위에 두는지, 개발 기간이 얼마나 되는지, 함께 하는 동료의 역량은 어떠한지 등을 고려해서 집단마다 다르게 반영하게 될 것입니다.
