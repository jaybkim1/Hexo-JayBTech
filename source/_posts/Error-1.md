---
title: Atom Helper 로 인한 극도에 치달은 CPU 사용량
subtitle: Atom Editor 업그레이드 한 후 극도에 치달은 CPU 사용량을 해결하는 방법에 대해 정리해보려고 합니다
catalog: true
tags:
  - Error
  - 삽질
catagories:
  - Error
  - 삽질
date: 2017-06-23 21:26:15
header-img:
comments: true
---


안녕하세요?

철학적인 개발자 JayB 입니다.

오늘은 제가 자주 사용하는 Atom Editor 를 사용하면서 CPU 사용량이 미칠듯이 치솟는 현상을 경험하여

해결한 방법에 대해서 정리해보려고 합니다.

하마터면, 제 소중한 맥북이 타버릴뻔 했네요ㅜㅜ

## 발생시기 추정

저 같은 경우 이 현상은 **Atom Editor 를 업그레이드** 하면서 발생한 걸로 판단되지만 확실하진 않습니다.

이전에는 아무렇지 않게 사용했었는데 업그레이드를 저번주에 하고 발생한걸로 보아 그리 추정합니다.

오늘 날짜 2017년 9월 16일로 최신 버전인 **1.20.0** 버전을 사용중에 있습니다.

NodeJS 를 검토하면서 여러가지 테스트를 하기 위해 Atom Editor 를 켰고

어느 순간부터 갑자기 제 맥북에서 팬 돌아가는 소리가 커지기 시작했습니다.

...??

잉 ? 왜이러지?

당황했습니다...

![당황](https://user-images.githubusercontent.com/20435620/30512457-2de33b86-9b2b-11e7-9bfa-6dd874cdfc46.png)

단순히 프로젝트가 무겁다라고 생각 하기 힘든 작업을 하고 있었기에

바로 생각이 든건...

>지금까지 내가 너무 막 사용했나?

음...

일단, **Activity Monitor** 어플리케이션을 이용하여 CPU 사용량과 메모리를 확인합니다.

아래 이미지를 한번 보시죠.

*위 이미지는 상황 발생시 해결하는데 집중하느라 캡처하지 못해 비슷한 상황을 겪은 외국분이 올린 이미지를 가져왔습니다*

<img width="336" alt="a2d1148b-3d92-4bac-aaf4-5f91c911e523" src="https://user-images.githubusercontent.com/20435620/30512441-ce4dec20-9b2a-11e7-9f27-2b8c19ecf91c.png">

Atom Helper 보이시나요?

**저 같은 경우 100% 가 훌쩍 넘어 200% 까지 가더군요.**

이건 정말 아니다 싶어 구글링을 합니다.

열심히 찾아본 결과 아래와 같은 링크를 찾을 수 있었고 생각보다 많은 분들이 저와 같은 상황을 경험하고 있었더군요.

* https://www.bountysource.com/issues/4121842-atom-helper-high-cpu-usage

* https://github.com/atom/atom/issues/3426

음...그래서 어떻게 해결했다는거지?

쭈욱 읽어본 결과 **상황에 따라 다르다**

그럼 내가 확인할 수 있는 최선책은 일단 _Preferences_ 에 가서 _Packages_ 쪽을 봤습니다.

제가 사용하고 있는 **Packages 들을 한번 다 Disable** 해봤습니다.

결과는?

> 해결되지 않았습니다.

이게 아닌가 보군.

다시 돌려놓고 원인을 찾기 위해 좀 더 뒤져봤습니다.

> Core Packages !!!

_Core Packages_ 부분에 눈이 들어왔고 제가 사용하고 있는 코어 패키지들은 뭐가 있는지 하나하나 자세히 봤습니다.

## Disable github, git-diff (Core Packages)

git-diff, github 보이시나요?

![iotwxq](https://user-images.githubusercontent.com/20435620/30512480-026c0306-9b2c-11e7-88e1-fb72f79a2562.png)

저는 이 두 패키지를 Disable 시켰봤더니 CPU 사용량이 바로 낮아지더군요.

> 해결!

제 추측이지만, Atom Editor 에서 제가 사용하는 git 관련 소스파일들을 참조하고 있었던 것 같습니다.

이 2개의 패키지에 대해 시간이 없는 관계로 자세히 살펴보는 것 까진 하지 않았습니다.

나중에 여유가 생기면 해봐야죠.

아시는분이 있다면 댓글로 알려주시면 감사하겠습니다 ^^

일단 해결은 됬으니 마음에 안정이 됩니다.

그럼 다시 열코하러~!
