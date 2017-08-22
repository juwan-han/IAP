Common &gt; IAP &gt; Error Code Guide
-------------------------------------

Client API 错误类型
-------------------

  错误 代码   类型                              说明
  ----------- --------------------------------- ----------------------------------------------------
  100         NETWORK\_TIMEOUT                  网络错误
  101         AUTHORIZATION\_ERROR              平台认证错误
  102         UNSUPPORTED\_DEVICE               不支持的设备
  103         UNSUPPORTED\_MARKET               不支持的Store
  104         USER\_CANCEL                      用户在结算途中取消的情况
  105         IAP\_INITIALIZED\_ERROR           IAP初始化错误的情况，确认初始化信息。
  106         IAP\_SERVER\_UNKNOWN\_ERROR       IAP 服务器不是HTTP Response 20x而是HTTP Status时
  107         IAP\_RESPONSE\_ON\_FAILED         IAP API的response失败
  108         INAPP\_INITIALIZED\_ERROR         Store结算库初始化错误
  109         INAPP\_PURCHASE\_ERROR            Store结算错误 – 请求购买时
  110         INAPP\_VERIFY\_SIGNATURE\_ERROR   Store结算错误 – 检验签名时
  111         INAPP\_CONSUME\_ERROR             Store结算错误 – 消耗结算明细时
  112         INAPP\_VERIFY\_CONSUME\_ERROR     Store结算检验错误 – 检验收据时
  113         SERVER\_NETWORK\_FAIL             IAP 服务器 NETWORK 错误
  116         APP\_STORE\_REMAINS\_PAYMENT      以前的结算未进行处理（需向用户显示再次购买诱导信息

Server API 错误类型
-------------------

  错误代码   类型                                  说明
  ---------- ------------------------------------- -----------------------------------------------------------------------------
  1100       INVALID\_PARAMETERS                   参数信息错误
  2111       HTTP\_CONTENT\_TYPE\_NOT\_SUPPORT     Content-Type 错误 – 请求Request 时，Content-Type不是 application/json的情况
  2112       HTTP\_REQUEST\_METHOD\_NOT\_SUPPORT   HTTP Method 错误 – 请求Request 时，用错误的HTTP Method进行请求时
  5000       CONSUME\_FAILED                       Consume 失败

Web Console 错误类型
--------------------

  错误代码   类型                               说明
  ---------- ---------------------------------- ---------------------
  1100       INVALID\_PARAMETERS                参数信息错误
  5003       INVALID\_AUTHENTICATED             Store验证信息错误
  5013       MARKET\_GOOGLE\_INVALID\_REQUEST   Google 关联信息错误

Ttouble Shooting
----------------

  错误代码     说明
  ------------ -------------------------------------------------------------------------------------------------------------------------------------------------------
  1100         参数信息错误
  2111, 2112   在IAP Server上请求Request时，确认Content-type, HTTP Method。链接
  5003, 5013   确认一下，用以下步骤是否能获得Store关联信息。 [链接](file:///C:\Users\user\Downloads\기술%20문서%20(3)\IAP_(document)\Server%20Developer%60s%20Guide)
  5000         - 确认PurchaseToken的正确与否。- 确认一下，先前通过客户端进行的结算是否进行的不错。
