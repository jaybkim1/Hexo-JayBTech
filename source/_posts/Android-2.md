---
title: 안드로이드 6.0 마시멜로 버전 이후 권한 방식 문제
subtitle: 안드로이드 6.0 마시멜로 버전 이후 부터 변경된 권한 방식에 대한 이해와 요청 방식
catalog: true
tags:
  - Android
catagories:
  - Android
date: 2017-05-10 21:26:15
header-img:
comments: true
---


## 들어가기에 앞서...

안녕하세요?

철학적인 개발자 JayB 입니다.

이 글을 보시는 분들은 아마 안드로이드 6.0 이상 권한 문제를 해결하기 위해 오셨을 겁니다.

바로 적용을 해보기 전에 간단한 배경 및 역사에 대해서 알아봐야 합니다.

**이미 아시는 분들은 맨 아래 Github 링크로 가셔서 소스부터 보셔도 됩니다.**

안드로이드 6.0 Marshmellow는 2015년 5월에 Google I/O 에서 최초로 공개가 되었습니다.

매번 버전이 업그레이드 될 때 마다 구글은 개선된 사항이나 새로운 기능들을 알려줍니다.

뭐가 달라졌을까요? [한번 살펴볼까요?](https://developers-kr.googleblog.com/2015/06/m.html)

개발자들에게 큰 영향을 끼치는 핵심중에 핵심!

**권환획득 방식이 변경** 됬다고 합니다.

이렇게 변경될 때마다 골치아프지만...어쩌겠어요...

구글신들이 방향성을 제시하면 따를 수밖에..................

일단 아래 **안드로이드 플랫폼 버전별 점유율** 을 한번 보시죠.

[플랫폼 버전별 점유율](https://user-images.githubusercontent.com/20435620/29756581-f315ad40-8bdf-11e7-82b0-4884812c8a52.PNG)

[공식홈페이지 참조](https://developer.android.com/about/dashboards/index.html?hl=ko)

2015년 1.2% 내외 였지만 기준 **2017년 8월 8일 기준 45.8% (6.0 이상)** 이나 되는 걸 보실 수 있습니다.

이 동적 권한 문제는 개발자들을 골치아프게 합니다.

앞으로는 어느 어플을 개발하더래도 무조건 거쳐가야 될 부분이라는 거죠.

어떻게 하면 좀 더 효율적으로 소스코드를 짜고 권한 획득을 얻을 수 있을지 알아보도록 하겠습니다.

## 안드로이드 6.0 버전 이전 권한 획득 방식

안드로이드 6.0 버전 이전 까지만 하더래도 권한을 관리하는 부분은 개발자들에겐 다소 어렵지 않은 부분이었습니다.

사용할 권한들을 Manifest.xml 파일에 선언해주면 사용자가 앱을 설치하는 시점에 한번에 동의를 받으면 그 이후엔 문제없었기 때문입니다.

이로 인해, [악용하는 사건](http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=105&oid=277&aid=0003573684) 들이 발생했습니다.

권한 어플 악용 관련 내용 참고

[관련 내용](http://systemin.tistory.com/entry/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%95%B1-%EA%B6%8C%ED%95%9C-%EB%B6%80%EC%9E%91%EC%9A%A9%EB%8F%84%EC%B2%AD-%EC%9C%84%ED%97%98%EC%84%B1)

구글은 이를 해결하려고 안드로이드 6.0 마시멜로 버전 이후 부터 개선한 것이구요.

이제 이해 하셨죠?


## 모든 권한을 체크해야만 할까요?

안드로이드 6.0 이상 버전부터는 설치 할 때 권한 허용 여부를 묻지 않도록 했습니다.

앱을 사용시에 해당 권한이 필요할 때 마다 사용자로부터 권한을 허가받도록 변경했습니다.

또한, 사용자가 권한을 허용했더라도 얼마든지 설정에 가서 허용을 풀 수 있도록 해놨구요.

구글은 사용자에게 좀 더 사용자의 핸드폰 보안에 대한 선택권(?) 을 준거죠.

그래서 **개발자들은 좀 더 신경써야 될 부분이 늘어난 거죠.**

![좌절](https://user-images.githubusercontent.com/20435620/29756639-5920cf02-8be0-11e7-93ea-ef4a2c7ff588.jpg)

..........................

.................................

..........................................

하지만, **Manifest.xml 에 명시한 모든 권한에 대해 하나하나 요청을 해야 되는건 아닙니다.**

[공식홈페이지]((https://developer.android.com/guide/topics/permissions/requesting.html)) 에 보시면 구글이 정의한 **Dangerous Permission** 들만 권한을 체크하고 요청해주면 됩니다.

아래 이미지는 공식홈페이지에서 캡처해온 이미지 입니다.

![권한](https://user-images.githubusercontent.com/20435620/29756655-852a689c-8be0-11e7-9c4b-734f7227c8f1.PNG)


## 이제 본격적으로 권한을 체크하고 요청하는 방법에 대해 알아볼까요?


### Manifest 파일에 명시

먼저 요청할 권한들을 Manifest 파일에 명시해줘야 합니다.

**권한 부여 방법 설명이 끝난 후 Github 에 프로젝트를 올릴 예정이니 코드를 먼저 보실분은 맨 아래 링크로 가셔서 보시면 됩니다.**


* **CAMERA**

* **READ_EXTERNAL_STORAGE**

* **WRITE_EXTERNAL_STORAGE**

* **ACCESS_FINE_LOCATION**

```
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
```


### 권한 체크하기

사용자가 이미 해당 권한을 부여했는지 안했는지 확인하기 위해 권한을 체크해야 합니다.

그렇기 위해서, 아래 함수들을 사용해야 합니다.

[ContextCompat.checkSelfPermission()](https://developer.android.com/reference/android/support/v4/content/ContextCompat.html#checkSelfPermission(android.content.Context, java.lang.String))

```
if (Build.VERSION.SDK_INT >= 23)
{
		if (CAMERA_PEMISSION != PackageManager.PERMISSION_GRANTED && READ_STORAGE_PERMISSION != PackageManager.PERMISSION_GRANTED &&
						WRITE_STORAGE_PERMISSION != PackageManager.PERMISSION_GRANTED && LOCATION_PERMISSION != PackageManager.PERMISSION_GRANTED)
		{
				// Permissions are not granted yet


		}
		else
		{
				// Permissions are already granted

		}
}
```


### 권한 허가 요청하기

[requestPermissions()](https://developer.android.com/reference/android/support/v4/app/ActivityCompat.html#requestPermissions(android.app.Activity, java.lang.String[], int))

>Requests permissions to be granted to this application.
These permissions must be requested in your manifest, they should not be granted to your app, and they should have protection level #PROTECTION_DANGEROUS dangerous,
regardless whether they are declared by the platform or a third-party app.

```
// Permissions are not granted yet 부분에 아래 소스코드 넣기

ActivityCompat.requestPermissions(getParent(),
			 new String[]{Manifest.permission.CAMERA, Manifest.permission.READ_EXTERNAL_STORAGE,
							 Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.ACCESS_FINE_LOCATION},
								 REQUEST_PERMISSION);
```



### 권한 허가 요청 후 결과 값 가져오기

[onRequestPermissionsResult()](https://developer.android.com/reference/android/support/v4/app/ActivityCompat.OnRequestPermissionsResultCallback.html#onRequestPermissionsResult(int, java.lang.String[], int[]))

>This interface is the contract for receiving the results for permission requests.

Callback 함수입니다.

권한 허가가 됬으면 다음 화면으로 넘기면 되겠죠?

```
@Override
	 public void onRequestPermissionsResult(int requestCode,String permissions[], int[] grantResults) {
			 switch (requestCode) {
					 case REQUEST_PERMISSION:

							 if (grantResults.length > 0 &&
											 grantResults[0] == PackageManager.PERMISSION_GRANTED) {

									 Log.i("TAG", "Permissions are granted");

									 Intent intent = new Intent(getApplicationContext(), MainActivity.class);
									 startActivity(intent);

							 } else {

									 Log.i("TAG", "Permissions are denied");


							 }
							 return;
			 }
	 }
```

## Github 에 올려놓은 [프로젝트 공유](https://github.com/jaybkim1/PermissionExample)

[Github 소스 코드 보러가기](https://github.com/jaybkim1/PermissionExample)


**아래는 제가 Github에 올려놓은 프로젝트 화면을 캡처한 이미지 입니다**

![Preview](https://user-images.githubusercontent.com/20435620/29760207-7fe0126c-8bfc-11e7-9251-5ea1000f205a.jpg)

![Request Permissions](https://user-images.githubusercontent.com/20435620/29760213-8dace988-8bfc-11e7-91b3-89c3fa72bc7d.jpg)



![만족](https://user-images.githubusercontent.com/20435620/29760287-449e89b2-8bfd-11e7-885c-20d5fe00b977.jpg)



## 마무리...

안드로이드 6.0 버전 부터 변화된 권한 방식에 대해서 알아봤습니다.

글은 쓸수록 늘고 있다는 걸 느끼는 날이네요.

이해가 안되는 부분이나 좀 더 설명이 필요한 부분은 댓글을 달아주시면 최대한 빨리 답변 드리도록 하겠습니다.

그럼 전 이만...
