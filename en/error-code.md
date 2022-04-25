## Mobile Service > IAP > Error Codes

> [Notice]<br>
> A new IAP SDK that supports subscription has been released as [NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/). <br>
> No new features will be developed for the existing IAP SDK.

## Client API Errors

| Error Code | Type | Description |
| ---------- | ----- | ----- |
| 100 |  NETWORK_TIMEOUT |  Network error |
| 101 |  AUTHORIZATION_ERROR |  Platform authorization error |
| 102 |  UNSUPPORTED_DEVICE |  Unsupported device |
| 103 |  UNSUPPORTED_MARKET |  Unsupported market |
| 104 |  USER_CANCEL |  Cancelled by the user during the payment process |
| 105 |  IAP_INITIALIZED_ERROR |  Invalid IAP initialization. Check the initialization information. |
| 106 |  IAP_SERVER_UNKNOWN_ERROR |  HTTP status is not IAP Server HTTP Response 20x |
| 107 |  IAP_RESPONSE_ON_FAILED |  IAP API response failure |
| 108 |  INAPP_INITIALIZED_ERROR |  Store payments library initialization error |
| 109 |  INAPP_PURCHASE_ERROR |  Store payment error - when requesting a purchase |
| 110 |  INAPP_VERIFY_SIGNATURE_ERROR |  Store payment error - when verifying signature |
| 111 |  INAPP_CONSUME_ERROR |  Store payment error - when payment history is consumed |
| 112 |  INAPP_VERIFY_CONSUME_ERROR |  Store payment verification error - when verifying receipt |
| 115 |	 INAPP_ONGATE_CASH_INSUFFICIENT_ERROR |  ONGATE cash is insufficient |
| 117 |  IAP_IN_PROGRESS_ERROR | This error may occur when a new request comes in while the IAP API is still in progress. The client can ignore the error or make a request again as needed. |
| 118 |  FORCED_TERMINATION_ERROR | The activity has been forcibly terminated |
| 119 |  INAPP_PURCHASE_ERROR_ALREADY_PURCHASED_AT_OTHER_ACCOUNT | The same item has already been purchased with another account and issued |
| 120 |  INAPP_DEVELOPER_ERROR | An error that might occur during the development process, where required information is missing or incorrect arguments are used during the payment flow |
| 201 |  INAPP_ONESTORE_NEED_UPDATE | OneStore app needs to be updated |
| 202 |  INAPP_ONESTORE_NEED_LOGIN | OneStore app login required |

## Server API Errors

|Error Code|	Type|	Description|
|---|---|---|
|1100|	INVALID_PARAMETERS|	Invalid parameters|
|2111|	HTTP_CONTENT_TYPE_NOT_SUPPORT|	Content-Type error – The Content-Type is not application/json for HTTP request|
|2112|	HTTP_REQUEST_METHOD_NOT_SUPPORT|	HTTP Method error – A request was made with an unsupported HTTP method|
|5000|	CONSUME_FAILED|	Failed to consume|
|5018|	ALREADY_CONSUMED|	A payments has already been consumed|



## Web Console Errors

|Error Code|	Type|	Description|
|---|---|---|
|1100|	INVALID_PARAMETERS|	Invalid parameters|
|5003|	INVALID_AUTHENTICATED|	Store authentication error|
|5013|	MARKET_GOOGLE_INVALID_REQUEST|	Google integration information error|

## Troubleshooting

|Error Code|	Description|
|---|---|
|1100|	Invalid parameters|
|2111, 2112|	When making a request to the IAP Server, check the Content-type and HTTP Method.<br/> [Link](./api-guide-for-toast-sdk) |
|5003, 5013|	Check that the store integration information has been issued in the following steps. <br/> [Link](./console-guide) |
|5000| - Check if PurchaseToken is invalid. <br/> - Check whether the payment through the client was processed properly in advance.|
