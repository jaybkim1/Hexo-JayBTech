---
title: Disqus 삽질 
catalog: true
subtitle: We were unable to load Disqus. If you are a moderator please user out troubleshooting guide.
header-img:
tags:
  - Disqus 
  - 삽질
catagories:
  - Disqus
  - 삽질
date: 2018-07-24 23:26:15
comments: true
---

### # 참고

본 글에선 Hexo 테마를 설치하는 방법이나 Hexo 를 왜 사용하게 되었는지에 대한 부분은 다루지 않으니 궁금하시다면 구글링을 하여 원하는 부분을 찾으시길 바랍니다. 

조금만 검색을 해보시면 Hexo 공식사이트나 다른 블로그에 좋은 정보들을 얻을 수 있습니다.

<br>
### # 이 글의 목적

제가 사용하고 있는 이 Hexo 테마 블로그에 Disqus 댓글 기능을 연동하면서 제가 직접 경험한 삽질에 대해서 기록하여 다른 분들은 이런 삽질을 하지 않았으면 하는 공유 차원에서 글을 작성하게 되었습니다.

아래와 같은 에러 메세지가 출력된다면 제가 경험하고 해결한 방법을 참고하세요.

<p style="color: red;"> "We were unable to load Disqus. If you are a moderator please user out troubleshooting guide."</p>

### # 댓글을 달기 위해 시도한 프로세스 정리

아래는 많은 튜토리얼이나 글을 보면 아래와 같은 방식으로 hexo 테마에 Disqus 댓글기능을 쉽게 추가하는 걸 볼 수 있다.

1. Disqus 홈페이지 https://disqus.com 가서 계정을 생성한다.  
<br>

2. Disqus Admin 페이지에 가서 Site 를 생성한 후 Website 이름과 URL 을 작성하고 Shortname 을 복사한 후 _config.yml 파일에 disqus_username 부분에 붙여넣어준다.
Hexo 테마 중에 Disqus 를 지원하지 않는 테마라면 직접 Disqus Admin Installation Guide에서 제공하는 소스코드를 이용해서 커스텀하게 넣어줘야 한다.
<br>

![1](https://user-images.githubusercontent.com/20435620/43147321-b9163c14-8f9d-11e8-94cb-9fa7a57db374.png)

![2](https://user-images.githubusercontent.com/20435620/43147347-cc1a0a70-8f9d-11e8-9074-a4dd959e0b51.png)


이렇게 쉬운데 왜 작동을 안하는지 이유가 뭘까? 라는 의문을 가지며 개발자 답게 하나하나씩 검토하기 시작했다.

첫번쨰로 테마를 개발한 분의 미숙으로 인해 Disqus 기능이 추가될 때 휴먼에러가 있지 않을까? 하는 생각에 테마 source 폴더에 가서 댓글이 달리는 해당 ejs 파일에 Disqus 소스코드를 뜯어보았다. 아주 문제없이 잘 들어가있었다.

![3](https://user-images.githubusercontent.com/20435620/43147611-6ed89524-8f9e-11e8-8310-c93e0462b40f.png)


두번째로 원초적인 방법으로 Disqus shortname 이 제대로 동작을 하는지 알아보기 위해 Admin -> Installation -> Universal Code를 이용하여 아래와 같이 간단한 html 을 작성하여 테스트를 해보았다.

테스트 방법은 [생활코딩](https://opentutorials.org/course/2473/13865) 동영상 강좌를 참고하세요.

처음 테스트 당시엔 브라우저에 파일 경로 drag 방식으로 끌어다가 실행했기 떄문에 제대로 동작하지 않았다. (이때 뭐지?...멘붕이 왔다. Disqus 에 문제가 있나? 내 아이디에 문제가 있나?)

![4](https://user-images.githubusercontent.com/20435620/43147764-c130f384-8f9e-11e8-8754-53d5f06f8826.png)


생각이 많아지고 미궁속으로 빠지게 되었지만 디버깅을 해보면서 깨닫게 되었다.

"브라우저에 localhost 환경을 갖추어 되는구나!" http-server 를 이용하여 브라우저에서 localhost로 실행을 해보니 아주 잘 작동했다.

너무 바보 같다.

http-server가 생소하신 분은 윈도우면 WAMP 맥OS 환경이면 MAMP 솔루션을 구글에 검색하여 설치하여 사용법을 익히고 www/ 폴더에 작성한 html을 넣어 localhost 로 브라우저에서 실행해보시길 바랍니다.

### # 해결 방법

너무나도 간단하게 이것 저것 만지다가 해결됬다.

_config.yml 파일에 보면 url 을 넣는 부분이 있다.

저 url 부분에 CNAME 처럼 jaybdev.net 으로 넣었었는데 아래 이미지와 같이 

http:// 또는 https:// 를 넣어줬어야 했다.

이런...

![screen shot 2018-07-25 at 12 14 20 am](https://user-images.githubusercontent.com/20435620/43148195-c3840594-8f9f-11e8-87c4-0222c4beedc8.png)

개발자로 살아가면서 수 많은 에러를 경험하고 디버깅을 하게 되지만 이런 어처구니 없이 쉬운 삽질은 오랜만에 경험하게 되었다.
