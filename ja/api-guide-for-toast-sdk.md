## Mobile Service > IAP > Server API ガイド


> [お知らせ]
> 購読決済を支援する新規のIAP SDKが[TOAST SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)として発売されました。
> 既存IAP SDKはこれ以上新規機能を開発しない予定です。
> 本文書は[TOAST SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)ガイドです


IAPを連動するときに開発会社のサーバーで使用できるAPIです。<br>


## Consume API

ユーザアプリケーション サーバーは,アイテムを支給する前に,IAP サーバーに決済を消費することをお知らせする必要があります。 <br>
決済1件当たり1回だけ決済消費が可能で,決済の状態が正常でないと消費されません。 <br>
消費(Consume)していない決済内訳は,SDKの未消費決済内訳照会APIにて照会されます。<br>
商品タイプがCONSUMABLEの決済のみconsume可能です。



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

| Property name | Value   | Description             |
| ------------- | ------ | --------------- |
| paymentSeq | String | 決済番号 |
| accessToken | String | API Accessのためのトークン情報 |


### Response

Response bodyにJSON形に配信

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
| resultCode |  Integer |  成功と失敗の詳細コード |
| resultMessage |  String |  詳細メッセージ |

#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| price         | Float   | price |
| currency      | String | currency |
| productSeq      | long | 決済のアイテム番号 (consoleに登録されたアイテム固有番号) |



### Error Code

| Value | Description             |
| ------------- | ----------------------- |
| 5000 | CONSUME FAILED (例:パラメータ誤りなど) |
| 5018 |  ALREADY CONSUMED|
| 9999 |  UNKNOWN ERROR|



## Consumable List API

決済が完了しましたが,消費(consume)されていない決済内訳をServer APIで照会することができます。 <br>


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

| Property name | Value  | Description       |
| ------------- | ------ | --------------- |
| marketId | String | ストアコード (GG : Google, AS : Apple) |
| userChannel | String | ユーザーチャンネル (GF) |
| userKey | String | ユーザ識別キー |




### Response
Response bodyにJSON形に配信



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
| resultCode |  Integer |  成功と失敗の詳細コード |
| resultMessage |  String |  詳細メッセージ |

#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| paymentSeq      | String | 決済番号 |
| productSeq      | long | 決済のアイテム番号 (consoleに登録されたアイテム固有番号) |
| price         | Float   | price |
| currency      | String | currency |
| accessToken      | String | API accessのためのトークン |



### Error Code

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|



## ActiveSubscription List API
アプリ別,ユーザ別に満了していない購読決済を照会する。


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

| Property name | Value   | Description             |
| ------------- | ------ | --------------- |
| marketId | String | ストアコード (GG : Google, AS : Apple) |
| packageName | String | APP packageName (예: com.nhnent.iap.google.sample) |
| userChannel | String | ユーザーチャンネル (GF) |
| userKey | String | ユーザ識別キー |



### Response
Response bodyにJSON形に配信



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
| resultCode |  Integer |  成功と失敗の詳細コード |
| resultMessage |  String |  詳細メッセージ |

#### Result

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| channel      | String | ユーザーチャンネル (GF) |
| userId      | String | ユーザ識別キー |
| paymentSeq      | String | 決済番号 |
| appId      | String | packageName |
| productId         | String   | ストアーに登録された商品識別子 |
| productType      | String | 商品タイプ |
| productSeq      | long | 決済のアイテム番号 (consoleに登録されたアイテム固有番号)|
| currency      | String | currency |
| price      | Float | price |
| paymentId      | String | 最近更新されたストアの決済番号 |
| originalPaymentId      | String | 最初のストア決済番号 |
| purchaseTimeMillis      | long | 最近更新された時間 |
| expiryTimeMillis      | long | 満了時間 |




### Error Code

| Value | Description             |
| ------------- | ----------------------- |
| 1100 | INVALID PARAMETER |
| 9999 |  UNKNOWN ERROR|