Common &gt; IAP &gt; Getting Started
------------------------------------

IAP在Web Console上注册了App和项目之后，可使用SDK。

IAP 商品活性化及发行Appkey 
---------------------------

    为了使用IAP服务，在Web Console (http://console.cloud.toast.com)上
    选择了[Common] > [IAP]之后，点击[使用商品]按钮，激活服务。

![\[그림 1 IAP 상품
활성화\]](media/image1.png){width="5.833333333333333in"
height="5.276344050743657in"}

\[图 1 IAP 商品活性化\]

    点击[图 2]上端的'URL & Appkey'，确认AppKey或在剪贴板上进行复制。

![\[그림 2 AppKey 확인\]](media/image2.png){width="5.833333333333333in"
height="2.8722495625546807in"}

\[图 2 确认AppKey \]

注册Store – 获得APP ID 
-----------------------

    1. 选择[App]标签 > 点击[添加]按钮
    2. 在[Store ID]上选择Store
       输入关联Store的信息示例(Google Play)  
        - Store APP ID : 注册于Google Play的App Package Name 
        - Google In App Purchase License Key : 注册于Google Play的App的Public Key  
        - Google API Client ID : 认证OAuth的Google API下面的Client ID  
        - Google API Client Secret : 认证OAuth的Google API项目的Client Secret  
        - Refresh Token For Google OAuth : 通过Google Play Developer账户获得Token  
    3. 点击[添加]按钮  
    4. 确认[APP ID]

> \[参考\]\
> 为获得APP ID 而关联Store信息

![\[그림 3 스토어 등록\]](media/image3.png){width="5.833333333333333in"
height="1.3296314523184602in"}

\[图 3 注册Store\]

注册项目
--------

    1. 选择[Item]标签。
    2. 选择[Store ID] > 点击[+ Add]按钮。 
    3. 在[Item Name]栏内输入项目名称。 
    4. 在[Store Item ID]栏内输入和Google Play一样的注册于Store上的项目ID。
    5. 选择[状态]。
    6. 点击[添加]按钮，确认注册的[ITEM ID]。

![\[그림 4 아이템 등록\]](media/image4.png){width="5.833333333333333in"
height="1.3534962817147858in"}

\[图 4 注册项目\]

Store商品类型
-------------

    参考在各Store开发者中心上注册的InAppProducts的商品类型([表 1])，注册项目。

  Store                 商品类型
  --------------------- ------------------------
  Google Play           管理的商品
  App Store             易耗品 (consumable)
  T-Store (One store)   消耗性(consumable)商品

\[表 1\] Store商品类型

> \[注意\]\
> 用未指明的商品类型进行结算时的系统错误及财产损失，概不负责。

查询结算信息
------------

    1. 点击[Transaction]标签。
    2. 选择[Store ID]。
    3. 在[Date]上选择起始日和终止日的条件。  
    4. 在[排序方式]上选择排序条件。
    5. 点击[搜索]按钮。

![\[그림 5 결제 정보
조회\]](media/image5.png){width="5.833333333333333in"
height="1.2451257655293089in"}

\[图 5 查询结算信息\]

> \[参考\] 结算情况\
> - In Progress : 结算进行中\
> - Success : 完成结算\
> - Failure : 结算检验失败\
> - Refund : 完成退款
>
> 结算状态引起的情况\
> - In Progress : 通过Store进行的结算将不再进行或不进行至结算验证时\
> - Failure : 在Store上进行结算，但在结算验证上出现错误时\
> - Success : Store结算成功 - Refund :
> 管理员在Market上手动更新退款处理时

查询结算状态
------------

    以下情况可更改结算状态。

    1. 结算收费实际已经实现，但用IAP内部问题并不能正确反映结算状态时 (更为'Success'状态)
       1.1 为了变更为'Success'状态，应该像图7一样，记入收据信息和实现结算的价格、通货。

    2. 完成结算收费后，不进行consume处理，用户就不能接收项目且进行退款处理的情况 (变更为‘Refunded’状态)
       2.1 变更为‘Refunded’状态时，client的未消费结算明细查询不能在API上进行。

    可进行变更的结算状态如下图所示，[修改]按钮在状态会显示在column右侧。

![\[그림 6 결제 상태 수정\]](media/image6.png){width="5.133333333333334in"
height="2.06in"}

\[图 6 修改结算状态\]

 
![\[그림 7 결제 상태 수정\]](media/image7.png){width="5.833333333333333in"
height="3.6653291776028in"}

\[图 7 用成功结算的状态来修改时，记入添加信息\]

查询统计结算
------------

    1. 点击[Statistics]标签。
    2. 选择[通货]。
    3. 用[<][>]按钮，各Store 可按月查询‘本月总收入’、‘每日详细明细’。

![\[그림 6 결제 통계
조회\]](media/image8.png){width="5.833333333333333in"
height="1.3084109798775152in"}

\[图 6 查询统计结算\]
