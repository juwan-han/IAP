## Mobile Service > IAP > 콘솔 사용 가이드

IAP는 Console에서 앱과 아이템을 등록한 후 SDK를 사용할 수 있습니다.

## IAP 상품 활성화 및 Appkey 발급

```
IAP 서비스를 사용하기 위해서는 Console (https://toast.com/console)에서
[Mobile Service] > [IAP] 을  클릭하여 활성화합니다.
```

![[그림 1 IAP 상품 활성화]](http://static.toastoven.net/prod_iap/iap_n_52.png)
<center>[그림 1 IAP 상품 활성화]</center>

```
[그림 2-1]의 'URL & Appkey'를 클릭하여 AppKey를 확인하거나 클립보드에 복사합니다.
```

![[그림 2-1 URL & Appkey 메뉴]](http://static.toastoven.net/prod_iap/iap_n_53.png)
<center>[그림 2-1 URL & Appkey 메뉴]</center>


![[그림 2-2 AppKey 확인]](http://static.toastoven.net/prod_iap/iap_n_54.png)
<center>[그림 2-2 AppKey 확인]</center>

## 스토어 등록 – APP ID 획득

```
1. [App] 탭 선택 > [추가] 버튼 클릭  
2. [Store ID]에서 스토어 선택  
   스토어 연동을 위한 정보 입력 예시 (Google Play)  
    - Store APP ID : Google Play에 등록한 어플리케이션의 패키지명  
    - Google In App Purchase License Key : Google Play에 등록한 어플리케이션의 Public Key  
    - Google API Client ID : OAuth 인증을 위한 Google API 프로젝트의 Client ID  
    - Google API Client Secret : OAuth 인증을 위한 Google API 프로젝트의 Client Secret  
    - Refresh Token For Google OAuth : Google Play Developer 계정을 통해 획득한 Refresh Token  
3. [추가] 버튼 클릭  
4. [APP ID] 확인
```

> [참고]  
> APP ID 획득을 위한 [스토어 연동 정보](./console-guide/#store-interlocking-information)    

![[그림 3 스토어 등록]](http://static.toastoven.net/prod_iap/iap_n_32.png)
<center>[그림 3 스토어 등록]</center>

## 아이템 등록

```
1. [Item] 탭을 선택합니다.  
2. [Store ID] 선택 > [+ Add] 버튼을 클릭합니다.  
3. [Item Name]란에 아이템 이름을 입력합니다.  
4. [Store Item ID]란에 Google Play와 같은 스토어에 등록한 아이템 ID를 입력합니다.  
5. [상태]를 선택합니다.  
6. [추가] 버튼을 클릭하고, 등록한 [ITEM ID]를 확인합니다.  
```

![[그림 4 아이템 등록]](http://static.toastoven.net/prod_iap/iap_n_33.png)
<center>[그림 4 아이템 등록]</center>

## 스토어 상품유형

```
각 스토어 개발자 센터에서 등록한 InAppProducts의 상품유형([표 1])을 참고하여 아이템을 등록합니다.
```

|Store|	상품유형|
|---|---|
|Google Play|	관리되는 제품|
|App Store|	소모품 (consumable)|
|T-Store (One store)|	소멸성 (consumable) 상품|

<center>[표 1] 스토어 상품 유형</center>

> [주의]  
> 명시되지 않은 상품유형으로 결제진행 시의 시스템 에러 및 재산상의 피해는 책임지지 않습니다.

## 결제 정보 조회

```
1. [Transaction] 탭을 클릭합니다.  
2. [Store ID]를 선택합니다.  
3. [Date]에서 시작일과 종료일 조건을 선택합니다.  
4. [정렬순서]에서 정렬 조건을 선택합니다.
5. [검색] 버튼을 클릭합니다.  
```

![[그림 5 결제 정보 조회]](http://static.toastoven.net/prod_iap/iap_n_44.png)
<center>[그림 5 결제 정보 조회]</center>

> [참고]
> 결제 상태   
>  - Reserved : 결제 준비 완료   
>  - Success : 결제 완료   
>  - Failure : 결제 검증 실패  
>  - Refund : 환불 완료

> 결제 상태에 따른 상황  
>  - Reserved : IAP 서버에 결제 예약 요청은 완료되었으나 검증 요청이 오지 않은 경우
>  - Failure : 스토어에서 결제를 진행했으나 결제검증에서 오류가 난 경우  
>  - Success : 스토어 결제 성공
>  - Refund : 관리자가 수동으로 마켓에서 환불처리됬음을 업데이트한 경우


## 결제 상태 조회
```
아래와 같은 상황일 경우 결제상태를 변경할 수 있습니다.

1. 결제과금은 실제로 이루어졌으나 IAP 내부 이슈로 결제상태가 정확히 반영되지 않았을 경우 ('Success' 상태로 변경)
   1.1 'Success' 상태로 변경하기 위해선 그림 7과 같이 영수증 정보와 결제가 이뤄진 가격, 통화를 기입해야 합니다.

2. 결제과금 완료 후 consume처리를 하지 않아 유저가 아이템을 받지못하여 환불처리를 했을경우 ('Refunded' 상태로 변경)
   2.1 'Refunded' 상태로 변경되었을 경우 client의 미소비 결제내역 조회 API에서 조회되지 않습니다.

변경이 가능한 결제상태는 아래와 같이 상태 컬럼 우측에 [수정] 버튼이 노출됩니다.
```
![[그림 6 결제 상태 수정]](http://static.toastoven.net/prod_iap/iap_45.png)
<center>[그림 6 결제 상태 수정]</center>
 
![[그림 7 결제 상태 수정]](http://static.toastoven.net/prod_iap/iap_46.PNG)
<center>[그림 7 결제 성공 상태로 수정시 추가정보 기입]</center>




## 결제 통계 조회

```
1. [Statistics] 탭을 클릭합니다.  
2. [통화]를 선택합니다.  
3. [<][>] 버튼으로 스토어별 '이달의 총 수입', '일별 상세내역'을 월별로 조회할 수 있습니다.  
```

![[그림 6 결제 통계 조회]](http://static.toastoven.net/prod_iap/iap_n_35.png)
<center>[그림 6 결제 통계 조회]</center>

## Store interlocking information

스토어의 인앱결제를 구현하려면 스토어에서 발급하는 애플리케이션 키를 IAP 웹콘솔에 입력하여야 합니다. 
마켓별로 발급하는 애플리케이션 키 값은 아래 표를 참고합니다.

## Google Play

### Google Play 스토어 연동 정보

| 필드 | 설명                                             |
| ---------------------------------- | ---------------------------------------------- |
| Market ID                          | 스토어 리스트에서 GG 선택                                 |
| Market App ID                      | Google Play에 등록한 애플리케이션의 패키지명                  |
| Google In App Purchase License Key | Google Play에 등록된 애플리케이션의 Public KEY(RSA)       |
| Google API Client ID               | Google API Project의 OAuth Client ID            |
| Google API Client Secret           | Google API Project의 OAuth Client Secret        |
| Refresh Token For Google OAuth     | Google Play Developer 계정을 통해 획득한 Refresh Token |

<center>[표 1] Google Play 스토어 연동을 위한 앱 등록 필드</center>

| 필드        | 설명                              |
| -------------- | ------------------------------- |
| Item Name      | 아이템에 대한 제목 또는 설명                |
| Market Item ID | Google Play 개발자 콘솔에 등록한 인앱상품 ID |

<center>[표 2] Google Play 스토어 연동을 위한 아이템 등록 필드</center>

### Google Play 개발자 콘솔의 애플리케이션 Public Key 확인

```
Google Play 개발자 콘솔 메뉴의 [애플리케이션 - 서비스 및 API] 선택
```

![](http://static.toastoven.net/prod_iap/iap_8.jpg)

> [참고]  
> [Android Developers - 인앱 결제 관리](http://developer.android.com/google/play/billing/billing_admin.html)

### Google API 개발자 콘솔에서 OAuth 클라이언트 정보 확인

```
Google Play 개발자 콘솔과 동일한 계정으로 Google API 콘솔에 프로젝트를 생성합니다. 아래의 링크를 참조하여 OAuth 인증에 필요한 아래의 정보를 생성합니다.  
1) Client ID  
2) Client Secret  
3) Refresh Token  
```

> [참고]  
> [Android Developers - Authorization](https://developers.google.com/identity/protocols/OAuth2WebServer)

<br/>

1. https://console.developers.google.com/apis/credentials 에서 OAuth 클라이언트 생성 (웹 에플리케이션)
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_g_01.png)
<center>[그림 1] Client ID 및 Client Secret 생성 1</center>

2. 승인된 redirection url에 https://developers.google.com/oauthplayground 입력
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_g_02.png)

3. oauthplayground 설정 > Use your own OAuth credentials 사용
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_g_03.png)

4. Step 1에서 https://www.googleapis.com/auth/androidpublisher 입력하여 Authorization code 코드 발급
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_g_04.png)

5. Step 2에서 Exchange authorization code for tokens 버튼을 눌러 토큰 발급
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_g_05.png)

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
        <activity android:name="com.nhnent.mobill.api.core.IAPActivity"
	        android:configChanges="keyboardHidden|orientation|screenSize|locale|layoutDirection"
	        android:theme="@android:style/Theme.Translucent.NoTitleBar"
	        android:windowSoftInputMode="adjustResize|stateHidden" />
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
1. 'Google Developers Console' 에 등록된 프로젝트가 Google Play Developer API가 활성화 되어있는지 확인합니다.
  - https://console.developers.google.com 접속  
  - [API 및 인증] > [API] 메뉴 접근  
  - [모바일 API] > [Google Play Developer API] 접근  
  - API 사용 중지 상태확인
```

![[그림 5] Google Developers Console 내부의 Google Play Developer API 메뉴](http://static.toastoven.net/prod_iap/iap_36_1.png)
<center>[그림 5] Google Developers Console 내부의 Google Play Developer API 메뉴</center>

![[그림 6] Google Play Developer API 활성화 확인](http://static.toastoven.net/prod_iap/iap_37.png)
<center>[그림 6] Google Play Developer API 활성화 확인</center>

```
2. 'Google Play Developer Console' 에서 프로젝트 ID와 연결되어있는지 [API 액세스] 메뉴를 통해 확인합니다.  
  - https://play.google.com/apps/publish 접속
  - 좌측메뉴의 [설정] > [API 액세스] 메뉴 접근  
  - 프로젝트가 연결되어있는지 확인
```

![[그림 7] Google Play Developer API 활성화 확인](http://static.toastoven.net/prod_iap/iap_38.png)
<center>[그림 7] Google Play Developer API 활성화 확인</center>

```
3. 'Google Play Developer Console' 의 계정 소유자가 Google Developers Console의 프로젝트에 권한이 있는 사용자 이여야 합니다.  
  - https://console.developers.google.com 접속
  - 좌측 [권한]메뉴 접근  
  - 계정 확인
```

![[그림 8] 인앱상품 ID 확인](http://static.toastoven.net/prod_iap/iap_39.jpg)
<center>[그림 8] 인앱상품 ID 확인</center>

```
4. 'Google Play Developer Console' 인앱상품에서 Market Item ID와 일치하는 상품이 등록이 되어있어야 합니다.  
  - https://play.google.com/apps/publish 접속
  - 좌측 [인앱 상품]메뉴 접근  
  - 인앱 상품의 ID 확인
```

## 원스토어 통합개발자센터(구 T스토어)

### 통신3사 통합개발자센터에 대한 안내

원스토어 통합개발자 센터는 올레마켓 / U+스토어 / T스토어 / 네이버 앱스토어 통합 센터입니다. 
인앱결제를 위한 연동방법은 기존과 동일하게 제공되기 때문에 원스토어 연동 정보를 통해 퍼블리싱이 가능합니다.

> [참고]
> 2016년 6월 1일 이후로는 네이버 앱스토어는 원스토어로 양도 되었습니다.
> [네이버앱스토어 개발자센터 공식카페](http://cafe.naver.com/naverappdev/10658)

### 원스토어 연동 정보

[표 3] 원스토어 연동을 위한 앱 등록 필드

| 필드         | 설명                             |
| ------------- | ------------------------------ |
| Market ID     | 스토어 리스트에서 TS 선택                 |
| Market App ID | 스토어에 등록한 AID (Application ID) |

[표 4] 원스토어 연동을 위한 아이템 등록 필드

| 필드        | 설명                      |
| -------------- | ----------------------- |
| Item Name      | 아이템에 대한 제목 또는 설명        |
| Market Item ID | 원스토어에 등록한 In-App 상품의 ID |

### 원스토어 개발자 센터에서 AID와 In-App ID 발급

```
원스토어 개발자 센터에서 아래의 정보를 확인 합니다.  
1) AID : 원스토어 개발자 센터에서 생성한 애플리케이션의 ID  
2) In-App ID : 생성한 애플리케이션에 등록한 In-App 상품의 ID
```

### Android 원스토어 라이브러리 추가

IAP Android SDK의 다운로드 받고 원스토어 연동을 위해서는 추가적으로 아래와 같이 프로젝트에 라이브러리를 추가해야합니다.

\- Download한 SDK패키지에서 /libs/tstore 폴더의 파일을 애플리케이션 프로젝트의 /libs 에 복사합니다.

![[그림 9 원스토어 라이브러리의 추가]](http://static.toastoven.net/prod_iap/iap_41.png)
<center>[그림 9 원스토어 라이브러리의 추가]</center>

> [참고]  
> Unity 프로젝트에서 Library 추가   
> Download 한 SDK패키지에서 /libs/tstore 폴더의 파일을 /Plugins/Android/iap/libs 에 복사합니다.  

### AndroidManifest.xml 설정 예시

원스토어 연동을 위해서는 아래와 같이 AndroidManifest.xml 설정 정보를 추가 합니다.

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
- Android: 샘플 어플리케이션의 /AndroidManifest-tstore-example.xml 참조  
- Unity: 유니티 플러그인의 /Plugins/Android/AndroidManifest-iap-tstore-template.xml 참조  
- 원스토어는 결제시 개발환경을 아래와 같이 지원합니다. AndroidManifest.xml 를 통해 설정가능합니다.  
  * iap:plugin_mode: 개발(development), 운영(release)
```

> [참고]  
> [원스토어 개발자 센터 개발도구](http://dev.onestore.co.kr/devpoc/reference/view/Tools)

<br/>
> [참고]  
> 원스토어 인앱 SDK 업데이트   
> 안드로이드 6.0이 공개됨에 따라 원스토어에서는 최신 인앱 SDK (v.15.01.00) 을 적용해야함을 강력권고 하고있습니다. 
> OneStore 개발자 센터를 통해 앱을 등록하기 위해서는 최신 인앱 SDK을 적용해야만 앱을 등록할 수 있습니다.    
> [원스토어 Reference](http://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?noticeId=26472)

<br/>
> [참고]  
> [네이버 앱스토어 영업 양수도 관련 서비스 주요 변경사항](http://cafe.naver.com/naverappdev/10658)

## 애플 앱스토어

### 앱스토어 연동 정보

| 필드         | 설명                          |
| ------------- | --------------------------- |
| Market ID     | 스토어 리스트에서 AS 선택              |
| Market App ID | 앱스토어에 등록한 애플리케이션의 Bundle Id |

| Web Console <br/> 아이템 등록 필드        | 설명               |
| -------------- | ---------------- |
| Item Name      | 아이템에 대한 제목 또는 설명 |
| Market Item ID | 앱스토어 등록한 제품 ID   |

### 앱스토어 개발자 센터에서 Bundle Id 및 In-App 제품ID 확인

```
iTunes Connect 를 통해 아래의 정보를 확인 합니다.  
1) Bundle Id : iTunes Connect를 통해 등록한 애플리케이션의 Bundle Id  
2) 제품 ID : iTunes Connect를 통해 등록한 In-App 상품의 제품ID
```

> [참고]  
> In App Purchase 테스트를 하기 위해 iTunes Connect에 어플리케이션 및 상품등록을 완료했다고 가정합니다.   
> [iTunes Connect](http://itunesconnect.apple.com)  
