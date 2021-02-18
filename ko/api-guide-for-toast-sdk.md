## Mobile Service > IAP > Server API 가이드

> [공지]
> 구독 결제를 지원하는 신규 IAP SDK가 [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)로 출시됐습니다.
> 기존 IAP SDK는 더 이상 신규 기능을 개발하지 않을 예정입니다.
> 본 문서는 [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/) 가이드입니다.

IAP를 연동할 때 개발사 서버에서 사용할 수 있는 API입니다.<br>



## Consume API

사용자 애플리케이션 서버는 아이템을 지급하기 전에 IAP 서버에게 결제를 소비 할 것을 알려야 합니다. <br>
결제 1건당 1번만 결제소비 가능하며, 결제의 상태가 정상이 아니면 소비되지 않습니다. <br>
소비 (Consume) 하지 않은 결제내역은 SDK의 미소비 결제 내역조회 API를 통해 조회됩니다.<br>
상품 타입이 CONSUMABLE인 결제만 consume 처리 됩니다.

> [참고]<br>
> 결제 1건당 1번 소비 가능하며, 결제소비 하지 않은 결제는 IAP에서 아이템을 지급하지 않은 것으로 간주합니다.<br>
> 클라이언트는 소비 되지 않은 결제건을 일괄 조회할 수 있습니다.

### Request

#### HTTP Request

```
POST https://api-iap.cloud.toast.com/v1/service/consume
```

#### HTTP Request Header

| Key | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |
| X-NHN-TCIAP-AppKey  | appKey |


#### Request Body

| 이름            | 자료형    | 설명              |
| ------------- | ------ | --------------- |
| paymentSeq | String | 결제 번호 |
| accessToken | String | API Access를 위한 토큰 정보 |


### Response

Response body에 JSON형태로 전달

#### Success

```json
{
   "header":{
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "SUCCESS"
    },
    "result":{
        "price": 1500,
        "currency": "KRW",
        "productSeq": 12345
    }
}
```

#### Error
```json
{
    "header":{
        "isSuccessful": false,
        "resultCode": 5018,
        "resultMessage": "error message"
    }
}
```


#### Header

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | true or false |
| resultCode |  Integer |  성공 및 실패의 상세코드 |
| resultMessage |  String |  상세 메시지 |

#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| price         | Float   | 결제의 가격 |
| currency      | String | 결제의 통화 |
| productSeq      | long | 결제의 아이템 번호 (console에 등록된 아이템 고유 번호) |



### Error Code

| Value | Description             |
| ------------- | ----------------------- |
| 5000 | CONSUME FAILED (예:파라미터 오류 등) |
| 5018 |  ALREADY CONSUMED|
| 9999 |  UNKNOWN ERROR|



## Consumable List API

결제가 완료되었으나 소비(consume) 되지 않은 결제내역을 Server API로 조회할 수 있습니다. <br>
해당 API로 미소비내역을 조회하여 소비되지 않은 내역들을 소비(consume) 할 수 있습니다.


### Request
#### HTTP Request

```
POST https://api-iap.cloud.toast.com/v1/service/consumable
```

#### HTTP Request Header

| Key | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |
| X-NHN-TCIAP-AppKey  | appKey |

#### Request Body

| 이름            | 자료형    | 설명              |
| ------------- | ------ | --------------- |
| marketId | String | 스토어코드 (GG : Google, AS : Apple, ONESTORE : 원스토어) |
| userChannel | String | 사용자채널 (GF) |
| userKey | String | 사용자 식별키 |




### Response
Response body에 JSON형태로 전달



#### Success

```json
{
    "header":{
        "isSuccessful": true,
        "resultCode": 0,
        "resultMessage": "success"
    },
    "result":[
        {
        "paymentSeq": "2016122110023124",
        "productSeq": 1000292,
        "currency": "KRW",
        "price": 1000,
        "accessToken": "oJgM1EfDRjnQY7yqhWCUVgAXsSxLWq698t8QyTzk3NeeSoytKxtKGjldTc1wkSktgzjsfkVTKE50DoGihsAvGQ"
        },
 
        {
        "paymentSeq": "2016122110023125",
        "productSeq": 1000292,
        "currency": "KRW",
        "price": 1000,
        "accessToken": "7_3zXyNJub0FNLed3m9XRAAXsSxLWq698t8QyTzk3NeeSoytKxtKGjldTc1wkSktgzjsfkVTKE50DoGihsAvGQ"
        }
    ]
}

```

#### Header

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | true or false |
| resultCode |  Integer |  성공 및 실패의 상세코드 |
| resultMessage |  String |  상세 메시지 |

#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| paymentSeq      | String | 결제번호 |
| productSeq      | long | 결제의 아이템 번호 (console에 등록된 아이템 고유 번호) |
| price         | Float   | 결제의 가격 |
| currency      | String | 결제의 통화 |
| accessToken      | String | API access를 위한 토큰 |



### Error Code

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|



## ActiveSubscription List API
앱별, 유저별로 만료되지 않은 구독 결제를 조회한다.


### Request
#### HTTP Request

```
POST https://api-iap.cloud.toast.com/v1/service/activeSubscriptionList
```

#### HTTP Request Header

| Key | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |
| X-NHN-TCIAP-AppKey  | appKey |  


#### Request Body

| 이름            | 자료형    | 설명              |
| ------------- | ------ | --------------- |
| marketId | String | 스토어코드 (GG : Google, AS : Apple, ONESTORE : 원스토어) |
| packageName | String | 앱의 packageName (예: com.nhnent.iap.google.sample) |
| userChannel | String | 사용자채널 (GF) |
| userKey | String | 사용자 식별키 |




### Response
Response body에 JSON형태로 전달



#### Success

```json
{
  "header": {
    "isSuccessful": true,
    "resultCode": 0,
    "resultMessage": "SUCCESS"
  },
  "result": [
    {
      "channel": "GF",
      "userId": "default_testUserx",
      "paymentSeq": "2018102610330423",
      "appId": "com.nhnent.iap.google.sample",
      "productId": "subs_p1w",
      "productType": "AUTO_RENEWABLE",
      "productSeq": 1002904,
      "currency": "KRW",
      "price": 1000,
      "paymentId": "GPA.3375-2193-1175-57698",
      "originalPaymentId": "GPA.3375-2193-1175-57698",
      "purchaseTimeMillis": 1540522998289,
      "expiryTimeMillis": 1541134994548,
      "productSeq" : 1000009
    }
  ]
}
```


#### Error
```json
{
    "header":{
        "isSuccessful": false,
        "resultCode": 1100,
        "resultMessage": "error message"
    }
}
```
#### Header

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | true or false |
| resultCode |  Integer |  성공 및 실패의 상세코드 |
| resultMessage |  String |  상세 메시지 |

#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| channel      | String | 사용자 채널 |
| userId      | String | 사용자 키 |
| paymentSeq      | String | 결제번호 |
| appId      | String | packageName |
| productId         | String   | 스토어에 등록된 상품 식별자 |
| productType      | String | 상품 타입 |
| productSeq      | long | 상품 번호(iap console 내부 식별자)|
| currency      | String | 통화 |
| price      | Float | 가격 |
| paymentId      | String | 최근 갱신된 스토어 결제 번호 |
| originalPaymentId      | String | 최초 스토어 결제 번호 |
| purchaseTimeMillis      | long | 최근 갱신된 시간 |
| expiryTimeMillis      | long | 만료 시간 |



### Error Code

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|