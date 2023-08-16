## Mobile Service > IAP > 개요

NHN Cloud In-App Purchase(이하 NHN Cloud IAP)는 주요 서비스 플랫폼(Apple App Store, Google Play, ONE Store)을 아우르는 통합 인앱 결제 서비스입니다.


## 주요 기능

NHN Cloud IAP는 다음과 같은 기능을 제공합니다.

* Google Play, Apple AppStore, ONE store 의 인앱 결제를 단일 인터페이스로 제공합니다. 따라서 주요 스토어별 결제 연동 스펙을 완벽하게 학습하지 않아도 쉽게 적용할 수 있습니다.
* NHN Cloud IAP에서 별도로 운용하는 결제 검증 서버로 결제 보안 및 안정성을 확보할 수 있습니다.
* Google Play Store, Apple App Store의 구독, Promotion 기능을 제공합니다.
* 웹콘솔에서의 다양한 기능(결제내역 조회기능 등)으로 고객 문의에 대한 원활한 대응이 가능합니다.


## 지원 스토어

| 플랫폼 | 스토어 |
| --- | --- |
| Android | Google Play Store|
| Android | ONE store|
| iOS | Apple App Store|

## 지원 상품 유형

| Store | 스토어 상품유형| NHN Cloud IAP 상품유형|    
|---|---|---|
| Google Play Store| One-time, Subscriptions | CONSUMABLE, AUTO_SUBSCRIPTION |
| App Store| Consumable, Auto-Renewable | CONSUMABLE, AUTO_SUBSCRIPTION |
| ONE Store|	Managed product | CONSUMABLE|

## 서비스 용어


| 용어 | 설명 |
| --- | --- |
| AppKey | NHN Cloud 사용자 프로젝트와 상품간 1:1 매칭키. 프로젝트당 하나의 IAP용 AppKey를 발급함 |
| 스토어(Store) | Apple App Store, Google Play Store 같은 앱을 판매하는 곳 |
| 결제내역(Payment) | 사용자가 결제한 내역 |
| 결제요청(Purchase) | 앱 내에서 혹은 스토어에서 아이템을 구매함 |
| 결제소비(Consume) | 사용자에게 아이템을 지급한 후 결제를 소비하는 것 |
| Payment Access Token | 사용자 애플리케이션 서버가 결제를 소비할 때 사용하는 인증토큰 |

## 서비스 구조

IAP 서비스는 다음 그림과 같이 IAP SDK, User Application Server, IAP Server, Store 4가지로 구성됩니다.

![[그림 1 IAP 서비스 구조 - Server To Server Model]](http://static.toastoven.net/prod_iap/iap_n_1.png)
<center>[그림 1 IAP 서비스 구조 - Server To Server Model]</center>

![[그림 2 IAP 서비스 구조 - Build-in Model]](http://static.toastoven.net/prod_iap/iap_n_23.png)
<center>[그림 2 IAP 서비스 구조 - Build-in Model]</center>

| 컴포넌트 | 설명 |
| ----- | --- |
| NHN Cloud IAP SDK | IAP Android SDK입니다. 인앱 결제를 위하여 사용자ID 등록, 결제요청을 수행합니다. <br>결제 수행시 스토어(Google Play Store, Apple App Store등)의 인앱 결제 화면으로 이동합니다. |
| User Application Server | 사용자 애플리케이션 서버입니다. <br>IAP 서버를 통하여 클라이언트가 요청한 결제내역을 확인한 후 결제소비를 진행하고 아이템 전달을 수행합니다. |
| User Application Client | 사용자 애플리케이션에 서버가 존재하지 않는다면, 애플리케이션의 클라이언트에서 결제소비를 진행하고 아이템에 대한 권한을 부여하게 됩니다. |
| IAP Server | NHN Cloud에서 제공하는 인앱 결제 서버입니다. |
| Store | Google Store, Apple App Store 등의 다양한 스토어입니다. 플랫폼별 스토어는 IAP 서버와 연동되어 있습니다. |


## IAP 결제 흐름도


![[그림 3 Server To Server Model 결제 흐름도]](http://static.toastoven.net/prod_iap/iap_n_28.png)
<center>[그림 3 Server To Server Model 결제 흐름도]</center>

![[그림 4 Build-in model 결제 흐름도]](http://static.toastoven.net/prod_iap/iap_n_29.png)
<center>[그림 4 Build-in model 결제 흐름도]</center>


| Step | Description |
| ---------- | ----------- |
| [1] | 결제 사용자 ID를 등록합니다. <br>결제 사용자는 개발사에서 사용자를 식별하고 아이템을 지급하는 대상이며 Google play나 App Store 계정이 아닙니다.<br>**[참조]** <br>API Step<br>Android : InternalInAppPurchase.InAppPurchase.registerUserId<br>iOS : TIAPurchase registerUserId: error: |
| [2] | 클라이언트에서 결제를 요청합니다.<br>**[참조]** <br>API Step<br>Android : InternalInAppPurchase..InAppPurchases.requestPurchase<br>iOS : TIAPurchase startPurchaseWithViewController: itemId: completionHandler |
| [3] | 스토어에서 결제를 진행합니다. |
| [4] | 스토어에서 결제를 마치고 결제 결과를 전달받습니다.<br>전달받은 결과를 이용해 User Application Server에서 item consume 진행을 합니다.<br>**[주의]** <br>애플리케이션 서버가 존재 하지 않는 모델은 결제 소비를 클라이언트에서 직접 검증 할 수 있으나, <br/> 보안성 확보를 위해 Server To Server로 결제 소비 후 아이템에 대한 권한을 부여하는 것을 강력하게 권장 합니다. |
| [4-1]| 스토어에서 전달받은 결과를 통해 IAP Server에 Consume 요청을 합니다. |
| [5] | Consume을 성공하면 사용자에게 item을 전달합니다. |
| [6] | 결제를 완료합니다. |
