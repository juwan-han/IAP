Common &gt; IAP &gt; Store interlocking information
---------------------------------------------------

若想实现Store的In App结算，应将Store上发行的应用Key输入至IAP
Web控制台上。按Market发行的应用Key值请参照下表。

Google Play
-----------

### Google Play Store关联信息

  领域                                 说明
  ------------------------------------ --------------------------------------------------
  Market ID                            在Store清单上选择GG
  Market App ID                        注册于Google Play上的应用PackageName
  Google In App Purchase License Key   注册于Google Play上的应用Public KEY(RSA)
  Google API Client ID                 Google API Project的OAuth Client ID
  Google API Client Secret             Google API Project的OAuth Client Secret
  Refresh Token For Google OAuth       通过Google Play Developer账户获得的Refresh Token

\[表 1\] 关联Google Play Store的App注册领域

  领域             说明
  ---------------- ----------------------------------------------
  Item Name        有关项目的题目或说明
  Market Item ID   注册于Google Play开发者控制台上的InApp商品ID

\[表 2\] 关联Google Play Store的项目注册领域

### 确认Google Play开发者控制台的应用Public Key 

    选择Google Play开发者控制台菜单的[应用 – 服务及API] 

![](media/image1.jpg){width="5.833333333333333in"
height="1.3637849956255468in"}

> \[参考\] \[Android Developers – In App结算
> 管理\](http://developer.android.com/google/play/billing/billing\_admin.html)

### 在Google API开发者控制台上确认 OAuth 客户端信息

    用和Google Play开发者控制台一样的账户在Google API控制台上生成项目。参考下面的链接，生成OAuth认证所需的下列信息。 
    1) Client ID  
    2) Client Secret  
    3) Refresh Token  

> \[参考\] \[Android Developers -
> Authorization\](https://developers.google.com/identity/protocols/OAuth2WebServer)

    1. 生成Client ID及Client Secret 
      
      1) 用https://console.developers.google.com进行访问。
      
      2) 进入"用户认证信息> 制作用户认证信息> OAuth客户端ID" 菜单。
      
      3) 进行如下选择及输入。 
          - 应用类型: Web应用
          - 名称 : {任意指定}
          - 批准的Javascript原件: http://localhost
          - 批准的Redirection URI : http://localhost
      
      4) 若按生成按钮的话，Client ID和Client Secret会被生成并显示于页面。

![\[그림 1\] Client ID 및 Client Secret 생성
1](media/image2.png){width="5.833333333333333in"
height="3.3545570866141734in"}

\[图 1\] Client ID 及Client Secret的生成 1

![\[그림 2\] Client ID 및 Client Secret 생성
2](media/image3.png){width="5.833333333333333in"
height="4.5942858705161855in"}

\[图 2\] Client ID 及Client Secret的生成 2

    2. Refresh Token的生成
      
      1) 在浏览器URL输入栏中输入如下内容，将最后的{client_id}部分用上面发放的Client ID进行置换并实施。
          https://accounts.google.com/o/oauth2/v2/auth?scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fandroidpublisher&access_type=offline&include_granted_scopes=true&state=state_parameter_passthrough_value&redirect_uri=http://localhost&response_type=code&client_id={client_id}
      
      2) 在浏览器执行页面上邀请权限的话，点击“允许”按钮。 
      
      3) 将浏览器URL输入栏的URL进行如下更改的话，除了最后的#，{code}部分要另外保存。
          localhost/?code={code}
      
      4) 进行如下HTTPS请求的话，用应答结果可获得Refresh Token(refresh_token)。
          - URL : https://www.googleapis.com/oauth2/v4/token
          - Method : POST     
          - Headers : Content-Type = application/x-www-form-urlencoded
          - Body :
              grant_type = authorization_code
              code = {code}
              client_id = {client_id}
              client_secret = {client_secret}
              redirect_uri = http://localhost

![\[그림 3\] Refresh Token 생성
1](media/image4.jpg){width="5.833333333333333in"
height="1.160774278215223in"}

\[图 3\] Refresh Token的生成1

![\[그림 4\] Refresh Token 생성
2](media/image5.jpg){width="5.833333333333333in"
height="1.4439884076990377in"}

\[图 4\] Refresh Token的生成2

### AndroidManifest.xml 设置示例

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

    * Android : 参照样品App的/AndroidManifest-google-example.xml 
    * Unity : 参照Unity插件的/Plugins/Android/AndroidManifest-iap-template.xml 

### 关联Google Play 的注意事项

为了关联Google，需要注意一些事项。\
若不是以下情况的话，通过Web控制台有可能不能正常注册App、Item。

    1. 确认一下，‘Google Developers Console’上注册的项目是否激活了Google Play Developer API。.
      - 连接https://console.developers.google.com   
      - 访问[API及认证] > [API]菜单  
      - 访问[Mobile API] > [Google Play Developer API]   
      - API使用终止状态确认

![\[그림 5\] Google Developers Console 내부의 Google Play Developer API
메뉴](media/image6.png){width="5.833333333333333in"
height="2.3357042869641296in"}

\[图 5\] Google Developers Console内部的 Google Play Developer API 菜单

![\[그림 6\] Google Play Developer API 활성화
확인](media/image7.png){width="4.293333333333333in"
height="2.0733333333333333in"}

\[图 6\] Google Play Developer API 活性化确认

    2. 在‘Google Play Developer Console’上通过[API存取]菜单确认其是否与项目ID相连。
      - 连接https://play.google.com/apps/publish 
      - 访问左侧菜单的[设置] > [API存取]菜单
      - 确认项目是否连接

![\[그림 7\] Google Play Developer API 활성화
확인](media/image8.png){width="5.833333333333333in"
height="2.774284776902887in"}

\[图 7\] Google Play Developer API 活性化确认

    3. ‘Google Play Developer Console’的账户所有者必须是在Google Developers Console的项目上拥有权限的所有者。 
      - 连接https://console.developers.google.com 
      - 访问左侧[权限]菜单
      - 确认账户

![\[그림 8\] 인앱상품 ID
확인](media/image9.jpg){width="5.833333333333333in"
height="1.7389337270341207in"}

\[图 8\] 确认In App商品 ID

    4. 应该在‘Google Play Developer Console’In App商品上注册与Market Item ID一致的商品。.  
      - 连接https://play.google.com/apps/publish 
      - 访问左侧[In App]菜单
      - 确认In App 商品的ID 

ONE Store综合开发者中心 (旧 T Store)
------------------------------------

### 有关通信3公司的综合开发者中心的介绍

ONE Store综合开发者中心是Olleh Market / U+Store / T Store / Naver
Store的综合中心。 结算In
App的关联方法因为与现存提供的一致，所以可通过ONE Store关联信息进行出版。

> \[参考\] 2016年 6月1日后，Naver ONE Store就转为了ONE Store。 [Naver
> App Store开发者中心官方网站](http://cafe.naver.com/naverappdev/10658)

### ONE Store关联信息 

\[表 3\] 关联ONE Store的App注册领域

  领域            说明
  --------------- -------------------------------------
  Market ID       在Store清单上选择TS
  Market App ID   注册于Store上的AID (Application ID)

\[表 4\] 关联ONE Store 的项目注册领域

  领域             说明
  ---------------- ---------------------------------
  Item Name        有关项目的题目或说明
  Market Item ID   注册于ONE Store上的In-App商品ID
                   

### 在ONE Store 开发者中心上发行AID和 In-App ID 

    在ONE Store开发者中心上确认以下信息。  
    1) AID : 在ONE Store开发者中心上生成的应用ID  
    2) In-App ID : 注册于生成的应用上的In-App商品ID

### 添加Android ONE Store 库

为了IAP Android SDK的下载和关联ONE Store，需额外在如下项目上添加库。

- 在Download的SDK
Package上，将/libs/tstore文件夹的文件复制于应用项目的/libs上。

![\[그림 9 원스토어 라이브러리의
추가\]](media/image10.png){width="2.0in" height="0.6in"}

\[图 9 添加ONE Store库\]

> \[参考\]\
> 在Unity 项目上添加 Library\
> 在Download的SDK Package上，将 /libs/tstore
> 文件夹的文件复制于/Plugins/Android/iap/libs上。

### AndroidManifest.xml设置示例 

为了关联ONE Store，需添加如下AndroidManifest.xml设置信息。

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

    - Android: 参照样品App的/AndroidManifest-tstore-example.xml 
    - Unity: 参照Unity插件的/Plugins/Android/AndroidManifest-iap-tstore-template.xml  
    - ONE Store在结算时，支持如下开发环境。可通过AndroidManifest.xml进行设置。

      * iap:plugin_mode: 开发(development), 运营(release)

> \[参考\]
> \[`ONE Store``开发者中心开发工``具`\](http://dev.onestore.co.kr/devpoc/reference/view/Tools)

&gt; \[参考\]\
&gt; 更新ONE Store In App SDK\
&gt; 根据Android 6.0的公开，强烈建议在ONE Store上适用最新的In App SDK
(v.15.01.00)。 &gt;
为了通过OneStore开发者中心来注册App，只有适用最新的In App
SDK才能注册App。\
&gt; [ONE Store
Reference](http://dev.onestore.co.kr/devpoc/support/news/noticeView.omp?noticeId=26472)

&gt; \[参考\]\
&gt; [Naver App
Store营业转让相关服务主要更改事项](http://cafe.naver.com/naverappdev/10658)

Apple App Store
---------------

### App Store 关联信息

  领域                       说明
  -------------------------- ----------------------------------
  Market ID                  在Store清单上选择AS
  Market App ID              注册于App Store上的应用Bundle Id
  Web Console 项目注册领域   说明
  Item Name                  有关项目的题目或说明
  Market Item ID             App Store注册的产品ID

### 在App Store开发者中心 上确认Bundle Id 及 In-App 的产品ID 

    通过iTunes Connect确认以下信息。  
    1) Bundle Id : 通过iTunes Connect注册的应用Bundle Id  
    2) 产品ID : 通过iTunes Connect注册的In-App商品的产品ID

> \[参考\]\
> 为了测试In App Purchase，假设在iTunes Connect上完成App及商品注册。.\
> iTunes Connect
