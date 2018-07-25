---
title: node.js 앱의 인스턴스를 관리해주는 forever 명령어 정리
subtitle: forever
catalog: true
tags:
  - node.js
  - forever
catagories:
  - node.js
  - forever
comments: true
date: 2018-07-25 14:26:15
header-img:
---


## # forever 란?

> forever는 npm을 사용해서 npm install forever 명령어로 간단히 설치가 가능하다. 
> 아주 간단한 명령어를 통해서 node.js로 만든 앱을 실행시켜주고 예기치 않게 종료되었을때 다시 실행해주거나 
> stdout을 로그파일로 남겨주는 등의 관리를 해주는 툴입니다. 
> 결론적으로, 아직까지는 안정적인 것 같고 관리하고 편합니다.


## # forever 사용하면서 에러 및 실시간 요청 확인 하는 방법

**설치는 npm 모듈로 npm install 로 가능하다.**

<pre>
<code>
 $ sudo npm install forever
</pre>
</code>

**자주 쓰이는 모듈이기 때문에 -g 옵션으로 글로벌 설치를 하면 편리하다.**

<pre>
<code>
 $ sudo npm install forever -g
</pre>
</code>

**Help 명령어로 명령어들 파악하기**

<pre>
<code>
 $ forever --help
</pre>
</code>

## # 명령어 정리

**forever 가 가진 명령어들은 크게 아래와 같습니다.**

<pre>
<code>
$ forever --help를 통해 forever에서 사용할 수 있는 명령어 옵션들을 알 수 있습니다.
</pre>
</code>

**forever [start | stop | stopall | list | cleanlogs] [options] SCRIPT [script options]**

* start: script 를 데몬으로 시작

* stop: 데몬으로 시작한 script 중지

* stopall: 모든 forever scrtips 중지

* list: forever scripts 리스트 확인

* cleanlogs: forever 로그 파일 전부 삭제 


## # 사용 중인 명령어

**node 서버를 forever로 실행하면서 output 파일과 error 파일을 현재 폴더 기준 하위 폴더에 out.log 와 err.log 파일이 생성되게끔 하였습니다. 하위 폴더로 둔 이유는 -w 옵션을 사용하기 때문입니다. app.js 폴더 기준을 감지하고 있는데 로그가 계속 쌓이는것 까지 감지해서 forever가 오작동을 하면 안되겠죠? forever 를 이용한 app.js 노드 인스턴스 실행**

<pre>
<code>
$ forever start -w -o ../output.log -e ../error.log app.js
</pre>
</code>

* -w watch 파일 변경이 되었으면 감지하여 적용

* -o output 실시간 데이터 로그

* -e error 에러 로그

**실시간 데이터와 에러 감지: 이제 데몬으로 노드 서버가 돌고 있고 하위 폴더로 가서 실시간으로 제대로 실행이 되는지 확인해봅니다.**

<pre>
<code>
$ tail -f output.log error.log
</pre>
</code>
