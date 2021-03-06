---
title: GitHub Pages 커스텀 도메인 설정하기
catalog: true
header-img: github-pages.png
tags:
  - Git
catagories:
  - Git
date: 2017-05-03 21:26:15
subtitle:
comments: true
---


## 들어가기에 앞서...

대부분의 내용은 이 [블로그](http://blog.saltfactory.net/setting-domain-name-in-github-pages-via-cname/) 를 참고하여 정리하였습니다.

위 블로그 외에도 여러 자료를 참고하여 커스텀 도메인을 적용하였습니다.

그 과정중에 **개인적으로 경험했던 햇갈렸던 부분** 에 대해 기록해놓으려고 포스팅하게 되었습니다.

이 자료가 저 처럼 GitHub 블로그를 운영함에 있어 처음 커스텀 도메인을 등록하시려는 분에게 도움이 되길 바라며

최대한 **자세히** 설명하도록 하겠습니다.

GitHub Pages를 사용하여 사이트를 운영하게되면 기본적으로 GitHub 에서 .github.io 도메인 네임을 제공합니다. (호스팅 서버를 구입할 필요가 없으니 완전좋죠?)

예를들어, 본인의 Github 아이디가 jaybkim1 이라면 http://jaybkim1.github.io 로 만들어지게 됩니다.

이번 포스팅에서는 기본적으로 주어지는 위 도메인 이름 말고 본인만의 특별한 *커스텀 도메인네임* 을 사용하고 싶은 사람을 위한 포스팅입니다.

## 1. 도메인네임 (Domain Name) 구입

**필자는 [가비아](https://www.gabia.com/)에서 도메인주소를 구입하였기 때문에 가비아를 기준으로 설명하도록 하겠습니다.**

가장 먼저 해야할 일은 도메인 서비스에 도메인네임을 등록하는 것 입니다.

국내 대표적인 도메인 등록 서비스는 아래와 같습니다. 개인적으로 사용하기 편한것을 사용하시면 됩니다.

* [가비아](https://www.gabia.com/)

* [후이즈](https://domain.whois.co.kr/)

도메인을 구입하는 방법은 직접 사이트로 이동하신 후 회원가입을 하고 원하는 도메인 주소를 검색한 후 사용하지 않고 있는 주소라면

구매하시면 됩니다.

도메인주소를 구입하셨다면

다음 !

![next](https://user-images.githubusercontent.com/20435620/29655513-46993f96-88ec-11e7-9e51-7596891ca2bd.png)


## 2. GitHub DNS Provider IP 주소 등록

GitHub의 DNS Provider IP 주소는 **[GitHub 홈페이지](https://help.github.com/articles/setting-up-an-apex-domain/)** 에 잘 설명되어있습니다.

본인의 github jekyll repository 로 가서 **Settings** 로 들어갑니다.

스크롤을 조금 내리시면 아래와 같이 GitHub Pages 항목 아래 Custom domain **Learn More** 이 보일겁니다. (아래 이미지 첨부)

![0](https://user-images.githubusercontent.com/20435620/29654146-00819792-88e7-11e7-841c-718b5d887681.PNG)

클릭해서 들어간 후 **Setting up an apex domain** 을 클릭하고 들어가면

아래와 같은 이미지에 DNS Provider 를 설정하는 방법에 대해 잘 설명되어있습니다.

![2](https://user-images.githubusercontent.com/20435620/29654214-53502326-88e7-11e7-96ed-43980a5df2f5.PNG)

이제 아래 2개의 IP 주소가 어디에 나와있는지 아시겠죠?

* 192.30.252.153

* 192.30.252.154

위 2개의 IP 주소중 **한개** 를 선택하여 자신의 도메인네임의 호스트 설정에서 자신의 호스트 이름에 IP 주소를 위의 것 중에 하나로 입력해야 됩니다.

저는 이 부분에서 조금 해맸습니다.

가비아에서 도대체 어디로 가야 호스트 설정 (관리자페이지) 갔는데 어디서 설정을 해야되나 계속 검색하면서 삽질을 하다가

네임플러스를 등록해야 된다는 걸 알게 되었고 메뉴얼을 뒤지기 시작했습니다.

메뉴얼을 보면 (2017년 8월 24일 기준) 아래 이미지에 설명된 것 처럼 분명 네임플러스 등록하는 부분이 있는데 저는 안보이는 것이었습니다 ㅜㅜ...

![3](https://user-images.githubusercontent.com/20435620/29654331-ba46a4a6-88e7-11e7-80ec-47f3d9d4aa8d.PNG)


가비아 측에 문의를 해보니 아래와 같은 답변을 얻을 수 있었습니다. (근무시간이라 그런지 답변이 굉장히 빨랐습니다)

>
안녕하십니까? 가비아 입니다.
>
부가서비스 개편되어 현재 메뉴얼 업데이트 중입니다.
>
가비아 로그인 후 my가비아 > 도메인 옆 [서비스정보] > 하단 dns레코드 [설정]을 통해 추가 및 변경할 수있습니다.
>

가비아 홈페이지에서 My가비아로 이동 하면 구입한 도메인 1건이 보이실 겁니다.

*'서비스 정보'* 를 누르시면 도메인 관리 페이지로 넘어갑니다.

페이지 왼쪽 구간에 *'부가서비스 설정'* 을 누르시고 *체크박스 클릭 후 'DNS 레코드 설정'* 을 들어간 후

아래 이미지 처럼 GitHub DNS Provider IP 주소를 입력하시면 됩니다.

A 레코드를 추가했다고 해서 바로 적용이 되는건 아닙니다. 

해당 DNS 서비스 업체에서 네트워크 설정을 하고 전파시키는데에 길게는 몇시간이 소요되니 기다려보시거나

[DNS Propagation Checker](https://mxtoolbox.com/SuperTool.aspx)와 같은 도구를 이용하여 A 레코드 추가가 잘 됬는지 확인해볼 수도 있습니다.

![2](https://user-images.githubusercontent.com/20435620/29654574-b55c5bd8-88e8-11e7-8904-819b2188ce18.PNG)

잘 따라오셨나요?

그럼 다음!

![next](https://user-images.githubusercontent.com/20435620/29655513-46993f96-88ec-11e7-9e51-7596891ca2bd.png)



## 3. CNAME 파일 등록

본인의 github jekyll repository 로 가서 CNAME (파일명 CNAME) 을 등록해줘야 합니다.

[https://github.com/jaybkim1/jaybkim1.github.io](https://github.com/jaybkim1/jaybkim1.github.io)로 가셔서 CNAME 파일을 확인해보시고

본인이 구입한 도메인 주소로 변경하시면 됩니다.

**여기서 잠깐!**

CNAME 은 대체 도메인 이름을 사용하는 기술입니다.

CNAME를 통해 생성한 페이지의 Custom 도메인을 사용할 수 있습니다.

> CNAME 파일을 올려놓으면 GitHub 의 Settings --> GitHub Pages 부분에 아래와 같은 이미지 처럼 Custom Domain 란이 채워져있는걸 확인하실 수 있습니다.

![4](https://user-images.githubusercontent.com/20435620/29654857-d864182c-88e9-11e7-86be-fe867eef834f.PNG)


## 마무리

커스텀 도메인 등록을 처음 하시는 분들을 위해 저처럼 해매지 않고 바로 하실 수 있게끔 최대한 자세히 설명을 해봤는데

잘 따라오셨나요? (잘 따라 오셨길... )

부족한 부분이 있다면 알려주시면 바로 업데이트 하도록 하겠습니다.
