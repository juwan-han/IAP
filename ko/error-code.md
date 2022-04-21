## Mobile Service > IAP > 오류 코드

> [공지]<br>
> 구독 결제를 지원하는 신규 IAP SDK가 [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)로 출시됐습니다. <br>
> 기존 IAP SDK는 신규 기능을 개발하지 않을 예정입니다.

## Client API 에러 타입

| 에러 코드 | 타입 | 설명 |
| ---------- | ----- | ----- |
| 100 |  NETWORK_TIMEOUT |  네트워크 오류 |
| 101 |  AUTHORIZATION_ERROR |  플랫폼 인증 오류 |
| 102 |  UNSUPPORTED_DEVICE |  지원하지 않는 디바이스 |
| 103 |  UNSUPPORTED_MARKET |  지원하지 않는 스토어 |
| 104 |  USER_CANCEL |  사용자가 결제 도중 취소 했을 경우 |
| 105 |  IAP_INITIALIZED_ERROR |  IAP 초기화가 올바르지 않은 경우, 초기화 정보를 확인하도록 한다. |
| 106 |  IAP_SERVER_UNKNOWN_ERROR |  IAP 서버 HTTP Response 20x가 아닌 HTTP Status일 때 |
| 107 |  IAP_RESPONSE_ON_FAILED |  IAP API의 response 실패 |
| 108 |  INAPP_INITIALIZED_ERROR |  스토어 결제 라이브러리 초기화 오류 |
| 109 |  INAPP_PURCHASE_ERROR |  스토어 결제 오류 - 구매 요청시 |
| 110 |  INAPP_VERIFY_SIGNATURE_ERROR |  스토어 결제 오류 - 서명 검증시 |
| 111 |  INAPP_CONSUME_ERROR |  스토어 결제 오류 - 결제 내역 소모시 |
| 112 |  INAPP_VERIFY_CONSUME_ERROR |  스토어 결제 검증 오류 - 영수증 검증 시 |
| 115 |	 INAPP_ONGATE_CASH_INSUFFICIENT_ERROR |  ONGATE 캐시 부족 |
| 117 |  IAP_IN_PROGRESS_ERROR | IAP API가 아직 처리 중일 때 새로운 요청이 들어오면 해당 에러가 발생할 수 있으며, 클라이언트는 필요에 따라 무시하거나 재요청할 수 있음 |
| 118 |  FORCED_TERMINATION_ERROR | Activity가 강제 종료시 |
| 119 |  INAPP_PURCHASE_ERROR_ALREADY_PURCHASED_AT_OTHER_ACCOUNT | 같은 상품을 다른 계정으로 이미 구매하고 지급이 경우 |
| 120 |  INAPP_DEVELOPER_ERROR | 개발 과정에서 발생 수 있는 오류, 결제 플로우 진행 중 필수 정보가 없거나 잘못된 인수가 활용되는 경우 |
| 201 |  INAPP_ONESTORE_NEED_UPDATE | OneStore 앱 업데이트가 필요한 경우 |
| 202 |  INAPP_ONESTORE_NEED_LOGIN | OneStore 앱 로그인이 필요한 경우 |

## Server API 에러타입

|에러 코드|	타입|	설명|
|---|---|---|
|1100|	INVALID_PARAMETERS|	파라미터 정보 오류|
|2111|	HTTP_CONTENT_TYPE_NOT_SUPPORT|	Content-Type 오류 – Request 요청시Content-Type이 application/json 아닌 경우|
|2112|	HTTP_REQUEST_METHOD_NOT_SUPPORT|	HTTP Method 오류 – Request 요청시 잘못된 HTTP Method로 요청시|
|5000|	CONSUME_FAILED|	Consume 실패|
|5018|	ALREADY_CONSUMED|	이미 소비된 결제건|



## Web Console 에러타입

|에러 코드|	타입|	설명|
|---|---|---|
|1100|	INVALID_PARAMETERS|	파라미터 정보 오류|
|5003|	INVALID_AUTHENTICATED|	스토어 인증정보 오류|
|5013|	MARKET_GOOGLE_INVALID_REQUEST|	Google 연동정보 오류|

## 트러블 슈팅

|에러 코드|	설명|
|---|---|
|1100|	파라미터 정보 오류|
|2111, 2112|	IAP Server에 Request 요청시 Content-type, HTTP Method를 확인합니다.<br/> [링크](./api-guide-for-toast-sdk) |
|5003, 5013|	스토어 연동정보를 아래 절차로 발급받았는지 확인합니다. <br/> [링크](./console-guide) |
|5000| - PurchaseToken이 잘못되었는지 확인합니다. <br/> - 클라이언트를 통한 결제가 앞서 잘 진행되었는지 확인합니다.|
