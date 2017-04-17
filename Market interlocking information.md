## Common > IAP > Marker interlocking information

마켓의 인앱결제를 구현하려면 마켓이 발급하는 애플리케이션 키를 IAP 웹콘솔에 입력하여야 합니다. 마켓별로 발급하는 애플리케이션 키 값은 아래 표를 참고합니다.

## Google Play

### Google Play 마켓 연동 정보

| 필드 | 설명                                             |
| ---------------------------------- | ---------------------------------------------- |
| Market ID                          | 마켓 리스트에서 GG 선택                                 |
| Market App ID                      | Google Play에 등록한 애플리케이션의 패키지명                  |
| Google In App Purchase License Key | Google Play에 등록된 애플리케이션의 Public KEY(RSA)       |
| Google API Client ID               | Google API Project의 OAuth Client ID            |
| Google API Client Secret           | Google API Project의 OAuth Client Secret        |
| Refresh Token For Google OAuth     | Google Play Developer 계정을 통해 획득한 Refresh Token |

[표 1] Google Play 마켓 연동을 위한 앱 등록 필드

| 필드        | 설명                              |
| -------------- | ------------------------------- |
| Item Name      | 아이템에 대한 제목 또는 설명                |
| Market Item ID | Google Play 개발자 콘솔에 등록한 인앱상품 ID |

[표 2] Google Play 마켓 연동을 위한 아이템 등록 필드

### Google Play 개발자 콘솔의 애플리케이션 Public Key 확인

```
Google Play 개발자 콘솔 메뉴의 [애플리케이션 - 서비스 및 API] 선택
```

![](http://static.toastoven.net/prod_iap/iap_8.jpg)

> [참고]  
> [http://developer.android.com/google/play/billing/billing_admin.html](http://developer.android.com/google/play/billing/billing_admin.html)

### Google API 개발자 콘솔에서 OAuth 클라이언트 정보 확인

```
Google Play 개발자 콘솔과 동일한 계정으로 Google API 콘솔에 프로젝트를 생성합니다. 아래의 링크를 참조하여 OAuth 인증에 필요한 아래의 정보를 생성합니다.  
1) Client ID  
2) Client Secret  
3) Refresh Token  
```

> [참고]  
> [https://developers.google.com/android-publisher/authorization](https://developers.google.com/android-publisher/authorization)

<br/>

```
1. Client ID 및 Client Secret 생성
  
  1) https://console.developers.google.com 로 접근합니다.
  
  2) "사용자 정보 인증 > 사용자 인증 정보 만들기 > OAuth 클라이언트 ID" 메뉴로 진입합니다.
  
  3) 아래와 같이 선택 및 입력 합니다.
      - 애플리케이션 유형 : 웹 애플리케이션
      - 이름 : {임의로 지정}
      - 승인된 자바스크립트 원본 : http://localhost
      - 승인된 리디렉션 URI : http://localhost
  
  4) 생성 버튼을 누르면 Client ID와 Client Secret이 생성되며 화면에 노출됩니다.
```
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_47.png)
<center>[그림 1] Client ID 및 Client Secret 생성 1</center>

![[그림 2] Client ID 및 Client Secret 생성 2](http://static.toastoven.net/prod_iap/iap_48.png)
<center>[그림 2] Client ID 및 Client Secret 생성 2</center>

```
2. Refresh Token 생성
  
  1) 브라우저 URL 입력란에 아래와 같이 입력하고 마지막 {client_id} 부분을 위에서 발급받은 Client ID로 치환하고 실행합니다.
      https://accounts.google.com/o/oauth2/v2/auth?scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fandroidpublisher&access_type=offline&include_granted_scopes=true&state=state_parameter_passthrough_value&redirect_uri=http://localhost&response_type=code&client_id={client_id}
  
  2) 브라우저 실행화면에서 권한을 요청하면 "허용" 버튼을 클릭합니다.
  
  3) 브라우저 URL 입력란의 URL이 아래와 같이 변경되면, {code} 부분을 마지막 #을 제외하고 별도로 저장합니다.
      localhost/?code={code}
  
  4) 아래와 같이 HTTPS 요청을 하면 응답결과로 Refresh Token(refresh_token)을 취득할 수 있습니다.
      - URL : https://www.googleapis.com/oauth2/v4/token
      - Method : POST     
      - Headers : Content-Type = application/x-www-form-urlencoded
      - Body :
          grant_type = authorization_code
          code = {code}
          client_id = {client_id}
          client_secret = {client_secret}
          redirect_uri = http://localhost
```

![[그림 3] Refresh Token 생성 1](http://static.toastoven.net/prod_iap/iap_49.png)
<center>[그림 3] Refresh Token 생성 1</center>

![[그림 4] Refresh Token 생성 2](http://static.toastoven.net/prod_iap/iap_50.png)
<center>[그림 4] Refresh Token 생성 2</center>

### AndroidManifest.xml 설정 예시

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<!-- google iab permission -->
<uses-permission android:name="com.android.vending.BILLING" />

<application>
        <activity android:name="com.nhnent.mobill.api.core.IAPActivity"/>
        <meta-data android:name="com.toast.iap.config.appId" android:value="1000000" />
        <meta-data android:name="com.toast.iap.config.market" android:value="GG" />
</application>
```

```
* Android : 샘플 어플리케이션의 /AndroidManifest-google-example.xml 참조  
* Unity : 유니티 플러그인의 /Plugins/Android/AndroidManifest-iap-template.xml 참조
```

### Google Play 연동 주의사항

구글연동을 위해 주의해야 할 사항이 있습니다.    
아래와 같은 상황이 아닌 경우 웹콘솔을 통해 정상적인 앱, 아이템 등록이 불가할 수 있습니다.

```
1) 'Google Developers Console' 에 등록된 프로젝트가 Google Play Developer API가 활성화 되어있는지 확인합니다.  
[1] 'Google Developers Console' 접속  
https://console.developers.google.com  
[2] [API 및 인증] > [API] 메뉴 접근  
[3] [모바일 API] > [Google Play Developer API] 접근  
[4] API 사용 중지 상태확인
```

![[그림 5] Google Developers Console 내부의 Google Play Developer API 메뉴](http://static.toastoven.net/prod_iap/iap_36_1.png)
<center>[그림 5] Google Developers Console 내부의 Google Play Developer API 메뉴</center>

![[그림 6] Google Play Developer API 활성화 확인](http://static.toastoven.net/prod_iap/iap_37.png)
<center>[그림 6] Google Play Developer API 활성화 확인</center>

```
2) 'Google Play Developer Console' 에서 프로젝트 ID와 연결되어있는지 [API 액세스] 메뉴를 통해 확인합니다.  
[1] 'Google Play Developers Console' 접속  
https://play.google.com/apps/publish
[2] 좌측메뉴의 [설정] > [API 액세스] 메뉴 접근  
[3] 프로젝트가 연결되어있는지 확인
```

![[그림 7] Google Play Developer API 활성화 확인](http://static.toastoven.net/prod_iap/iap_38.png)
<center>[그림 7] Google Play Developer API 활성화 확인</center>

```
3) 'Google Play Developer Console' 의 계정 소유자가 Google Developers Console의 프로젝트에 권한이 있는 사용자 이여야 합니다.  
[1] 'Google Developers Console' 접속  
https://console.developers.google.com  
[2] 좌측 [권한]메뉴 접근  
[3] 계정 확인
```

![[그림 8] 인앱상품 ID 확인](http://static.toastoven.net/prod_iap/iap_39.jpg)
<center>[그림 8] 인앱상품 ID 확인</center>

```
4) 'Google Play Developer Console' 인앱상품에서 Market Item ID와 일치하는 상품이 등록이 되어있어야 합니다.  
[1] 'Google Developers Console' 접속  
https://play.google.com/apps/publish  
[2] 좌측 [인앱 상품]메뉴 접근  
[3] 인앱 상품의 ID 확인
```

## 티스토어 (원스토어 통합개발자센터)

### 통신3사 통합개발자센터에 대한 안내

티스토어개발자 센터는 올레마켓 / U+스토어 / T스토어를 통합한 원스토어 통합개발자 센터입니다. 인앱결제를 위한 연동방법은 기존과 동일하게 제공되기 때문에 티스토어연동 정보를 통해 3사의 마켓에 퍼블리싱이 가능합니다.

> [참고]
> 2016년 6월 1일 이후로는 네이버 앱스토어는 원스토어로 양도 됩니다.
> http://cafe.naver.com/naverappdev/10658

### 티스토어 마켓 연동 정보

[표 3] 티스토어 마켓 연동을 위한 앱 등록 필드

| 필드         | 설명                             |
| ------------- | ------------------------------ |
| Market ID     | 마켓 리스트에서 TS 선택                 |
| Market App ID | 티스토어에 등록한 AID (Application ID) |

[표 4] 티스토어 마켓 연동을 위한 아이템 등록 필드

| 필드        | 설명                      |
| -------------- | ----------------------- |
| Item Name      | 아이템에 대한 제목 또는 설명        |
| Market Item ID | 티스토어에 등록한 In-App 상품의 ID |

### 티스토어 개발자 센터에서 AID와 In-App ID 발급

```
티스토어 개발자 센터에서 아래의 정보를 확인 합니다.  
1) AID : 티스토어 개발자 센터에서 생성한 애플리케이션의 ID  
2) In-App ID : 생성한 애플리케이션에 등록한 In-App 상품의 ID
```

### Android 티스토어 라이브러리 추가

IAP Android SDK의 다운로드 받고 티스토어 연동을 위해서는 추가적으로 아래와 같이 프로젝트에 라이브러리를 추가해야합니다.

\- Download한 SDK패키지에서 /libs/tstore 폴더의 파일을 애플리케이션 프로젝트의 /libs 에 복사합니다.

![[그림 9 티스토어 라이브러리의 추가]](http://static.toastoven.net/prod_iap/iap_41.png)
<center>[그림 9 티스토어 라이브러리의 추가]</center>

> [참고]  
> Unity 프로젝트에서 Library 추가   
> Download 한 SDK패키지에서 /libs/tstore 폴더의 파일을 /Plugins/Android/iap/libs 에 복사합니다.  

### AndroidManifest.xml 설정 예시

티스토어 연동을 위해서는 아래와 같이 AndroidManifest.xml 설정 정보를 추가 합니다.

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<!-- Tstore configurations -->
<uses-permission android:name="android.permission.RECEIVE_SMS " />
<application>
....
        <!-- TStore configrations -->
        <activity android:name="com.skplanet.dodo.IapWeb" android:configChanges="orientation|screenSize|keyboardHidden|locale|layoutDirection" android:excludeFromRecents="true" android:windowSoftInputMode="stateHidden" />
<meta-data android:name="iap:api_version" android:value="3" />
<meta-data android:name="iap:plugin_mode" android:value="development" />
        <activity android:name="com.nhnent.mobill.api.core.IAPActivity"/>
        <meta-data android:name="com.toast.iap.config.appId" android:value="1000000" />
        <meta-data android:name="com.toast.iap.config.market" android:value="TS" />
</application>
```

```
\* Android : 샘플 어플리케이션의 /AndroidManifest-tstore-example.xml 참조  
\* Unity : 유니티 플러그인의 /Plugins/Android/AndroidManifest-iap-tstore-template.xml 참조  
\* 티스토어는 결제시 개발환경을 아래와 같이 지원합니다. AndroidManifest.xml 를 통해 설정가능합니다.  
\- iap:plugin_mode : 개발 – development / 운영 – release
```

> [참고]  
> TStore 개발자 센터 개발도구 Reference  
> [http://dev.onestore.co.kr/devpoc/reference/view/Tools](http://dev.onestore.co.kr/devpoc/reference/view/Tools)  

<br/>
> [참고]  
> OneStore (TStore) 인앱 SDK 업데이트   
> 안드로이드 6.0이 공개됨에 따라 OneStore에서는 최신 인앱 SDK (v.15.01.00) 을 적용해야함을 강력권고 하고있습니다. OneStore 개발자 센터를 통해 앱을 등록하기 위해서는 최신 인앱 SDK을 적용해야만 앱을 등록할 수 있습니다.    
> 자세한 내용은 아래 Reference 참조  
> [<http://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?noticeId=26472>](<http://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?noticeId=26472>)

## 네이버앱스토어

### 네이버 앱스토어 연동 정보

```
네이버 앱스토어의 영업 양도  
네이버 앱스토어 서비스가 2016년 6월 1일 자로 원스토어 주식회사에 양도될 예정으로  
2016년 5월 10일 부터는 네이버 앱스토어의 신규 앱, 아이템을 등록할 수 없으며, 기존의 네이버 앱스토어에 등록했던 상품들은 원스토어에 상품 맵핑작업을 진행하셔야 합니다.  
2016년 6월 1일 이후에도 네이버 앱스토어 IAP를 적용한 앱에서의 결제는 기존과 동일하게 결제 가능하며 네이버 앱스토어 서비스가 종료되는 연내에 결제도 종료될 예정입니다.  
```

> [참고]  
> [중요 공지] 네이버 앱스토어 영업 양수도 관련 서비스 주요 변경사항  
> http://cafe.naver.com/naverappdev/10658  

## 애플 앱스토어

### 앱스토어 연동 정보

| 필드         | 설명                          |
| ------------- | --------------------------- |
| Market ID     | 마켓 리스트에서 AS 선택              |
| Market App ID | 앱스토어에 등록한 애플리케이션의 Bundle Id |

| Web Console <br/> 아이템 등록 필드        | 설명               |
| -------------- | ---------------- |
| Item Name      | 아이템에 대한 제목 또는 설명 |
| Market Item ID | 앱스토어 등록한 제품 ID   |

### 앱스토어 개발자 센터에서 Bundle Id와 In-App 제품 ID확인

```
iTunes Connect 를 통해 아래의 정보를 확인 합니다.  
1) Bundle Id : iTunes Connect를 통해 등록한 애플리케이션의 Bundle Id  
2) 제품 ID : iTunes Connect를 통해 등록한 In-App 상품의 제품ID
```

> [참고]  
> In App Purchase 테스트를 하기 위해 iTunes Connect에 어플리케이션 및 상품등록을 완료했다고 가정합니다.   
> iTunes Connect : [<http://itunesconnect.apple.com>](http://itunesconnect.apple.com)  
