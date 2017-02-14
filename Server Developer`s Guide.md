## Common > IAP > Server Developer's Guide

## Payment Consume API

사용자 애플리케이션 서버는 아이템을 지급하기 전에 IAP 서버에게 결제를 소비 할 것을 알려야 합니다. 
결제 1건당 1번만 결제소비 가능하며, 결제의 상태가 정상이 아니면 소비되지 않습니다. 
소비 (Consume) 하지 않은 결제내역은 SDK의 미소비 결제 내역조회 API를 통해 조회가능 합니다.

> [참고]  
> 결제 1건당 1번 소비 가능하며, 결제소비 하지 않은 결제는 IAP에서 아이템을 지급하지 않은 것으로 간주합니다.    
> 클라이언트는 소비 되지 않은 결제건을 일괄 조회할 수 있습니다.

### Request

[URL]

```http
POST https://api-iap.cloud.toast.com/inapp/v3/consume/{paymentSeq}/items/{itemSeq}
```

[Request Header]

| Property name | Value            |
| ------------- | ---------------- |
| Http Method   | POST             |
| Content-Type  | application/json |

[Path Parameter]

| 이름         | 자료형    | 설명                     |
| ---------- | ------ | ---------------------- |
| paymentSeq | String | 결제 번호                  |
| itemSeq    | Long   | Web Console에 등록된 아이템번호 |

[RequestBody]

| 이름            | 자료형    | 설명              |
| ------------- | ------ | --------------- |
| purchaseToken | String | 결제 검증을 위한 토큰 정보 |

[Example]

```http
POST https://api-iap.cloud.toast.com/inapp/v3/consume/2014090210002254/items/1032032

RequestBody
{
	"purchaseToken":"5PYSHgisiCU8BditHnDbPhmlS/0DSt4JDs2UMyg1/EY8oC6Q8qkuw5VBo7GNrBYLNUy656GCAh7h9e1BtXeoBA=="
}
```

### Response

Response body에 JSON형태로 전달

[Example Response]

```json
{
    "header": {
        "resultCode": 0,
        "resultMessage": "request is successful",
        "isSuccessful": true
    },
    "result": {
        "price":1000.0,
        "currency":"KRW"
    }
}
```

[Header]

| Property name | Value   | Description             |
| ------------- | ------- | ----------------------- |
| isSuccessful  | Boolean | 결제소비가 정상적으로 됐는지 여부. <br/> API 가 성공적으로 요청 되었을 때 true <br/> 실패 했을 때 false |
| resultCode |  Integer |  결제소비 실패시 상세코드 |
| resultMessage |  String |  상세 메시지 |

[Result]

| Property name | Value  | Description       |
| ------------- | ------ | ----------------- |
| price         | long   | 결제소비가 완료된 결제건의 가격 |
| currency      | String | 결제소비가 완료된 결제건의 통화 |

[ResultCode]

| 값 | 설명             |
| - | -------------- |
| 0 | 성공적으로 완료한 결제 건 |

> [참고]  
> [Error Code](/Common/IAP/Error%20Code/) 참조  

> [참고]  
> 기존의 consume API v2는 호출은 가능하나 더 이상 사용되지 않을 예정입니다.
