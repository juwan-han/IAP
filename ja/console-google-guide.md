## Mobile Service > IAP > Google 設定ガイド


Google一般商品および購読商品のインアップ決済のためにGoogle Play Billingを連動しなければなりません。<br>
Google Play Billingは,Google Play ConsoleとGoogle API Consoleで生成された値を使用します。<br>
さらに,グーグル購読商品の決済のため,Notificationを設定する必要があります。<br>
Notificationの設定が正しくなければ購読決済が進みません。

> 本文書は[新規のIAP SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)ガイドです。
<br>


## Google Application Key
下記情報をIAPアプリ情報に登録します。

| Key | Description                                             |
| ---------------------------------- | ---------------------------------------------- |
| Google In App Purchase License Key | Google Play Public KEY(RSA)       |
| Google API Client ID               | Google API Project의 OAuth Client ID            |
| Google API Client Secret           | Google API Project의 OAuth Client Secret        |
| Refresh Token For Google OAuth     | Google Play Developer 勘定を通じて獲得したRefresh Token |


## Google Console
| Console        | Location                              |
| -------------- | ------------------------------- |
| Google Play Console | https://developer.android.com/distribute/console |
| Google API Console | https://console.developers.google.com/apis/dashboard |


## Google Play Console

### Google In App Purchase License Key 確認
```
Google Play Console > App > (左側) 開発ツール > サービス及びAPI > ライセンス及びインアップ決済
```
![](http://static.toastoven.net/prod_iap/iap_8.jpg)


## Google API Console

> [参考]<br>
> [Android Developers - インアプリ決済管理](http://developer.android.com/google/play/billing/billing_admin.html) <br>
> [Android Developers - Authorization](https://developers.google.com/identity/protocols/OAuth2WebServer)

### OAuth クライアント生成
```
Google Play Consleと同一のアカウントでGoogle API Consoleにプロジェクトを生成します。
下記の図を参照して,OAuth 認証に必要な情報3 つを生成します。
1) Client ID  
2) Client Secret  
3) Refresh Token  
```
<br>

##### 1. https://console.droパス google.com/apis/credentialsでオイスクライアントを生成(ウェブアプリケーション)
![[그림 1] Client ID 및 Client Secret 생성 1](http://static.toastoven.net/prod_iap/iap_g_01.png)


##### 2. 承認された redirection urlに https://developers.google.com/oauthplayground 入力
![[그림 2] Client ID 및 Client Secret 생성 2](http://static.toastoven.net/prod_iap/iap_g_02.png)


##### 3. oauthplayground 設定 > Use your own OAuth credentials 使用
![[그림 3] Client ID 및 Client Secret 생성 3](http://static.toastoven.net/prod_iap/iap_g_03.png)


##### 4. Step 1で https://www.googleapis.com/auth/androidpublisher 入力して Authorization code コード発給
![[그림 4] Client ID 및 Client Secret 생성 4](http://static.toastoven.net/prod_iap/iap_g_04.png)


##### 5. Step 2で Exchange authorization code for tokens ボタンを押してトークン発給
![[그림 5] Client ID 및 Client Secret 생성 5](http://static.toastoven.net/prod_iap/iap_g_05.png)


## Google Play連動注意事項

OAuth 認証情報生成後,以下のガイドを参考にプロジェクト設定を進めます。

> [参考]
> Google Guide : https://developers.google.com/android-publisher/getting_started

### Google Play Android Developer APIのenable状態を確認します。

```
  - https://console.developers.google.com > APIs & Services > Dashboard
```
![[]](http://static.toastoven.net/prod_iap/iap-console-google-console-1.png)

<br>

### Google Play Developer ConsoleでLinked Projectを確認します。
 
```
  - https://play.google.com/apps/publish > Settings > Developer account > API access
```
![[]](http://static.toastoven.net/prod_iap/iap-console-google-console-2.png)




## Google real-time developer notification 設定

> [参考]<br>
> Google Cloud (https://cloud.google.com) Platformを使用しなければなりません。<br>
> Google Cloud Platform に決済プロフィールを登録し,使用状態に変更しなければなりません。


### Google Cloud > ビッグデータ > 掲示/購読

掲示/購読コンソール(https://console.cloud.google.com/cloudpubsub)で下記の作業を行います。

#### Topic 作り

```
1. Topicが生成されると,オプションの権限をクリックするか,Topic名をクリックしてTopic細部情報ページに移動します。
2. 主題の詳細情報ページで,役割の選択をクリックし,掲示/購読の掲示者を選択します。
3. 構成員の追加に google-play-developer-notifications@system.gserviceaccount.com を入力します。
4. 追加ボタンをクリックします。
```
![[] Topic 만들기](http://static.toastoven.net/prod_iap/iap-console-new-topic.png)
![[] Topic 수정하기](http://static.toastoven.net/prod_iap/iap-console-topic-option.png)

<br>

#### Subscription 作り
```
1. Topic右クリック > 新購読 
2. 転送タイプ
- [エンドポイントURLでプッシュ] 選択
- URL :  https://api-iap.cloud.toast.com/callback/subscription/{YOUR_PACKAGE_NAME}/GG
- {YOUR_PACKAGE_NAME} : google package name
```
![[] Subscription 만들기](http://static.toastoven.net/prod_iap/iap-console-new-subscription.png)

<br>

#### IAP ドメイン検証
```

1. https://console.cloud.google.com/apis/credentials/domainverification
2. [ドメイン確認]タブで,[ドメイン追加] をクリックします。
3. https://api-iap.cloud.toast.comを入力します。
4. [今移動]ボタンを押してウェブマスターセンターに移動します。
5. ウェブマスターセンターでプロパティを合わせることをクリックします。
6. [プロパティ追加]に https://api-iap.cloud.toast.com を入力します。
7. [推奨方法] 下段の [ロボットではない] クリック後,[OK] をクリックします。
8. 認証に成功すると,最後のイメージと同じ画面が表示されます。 この画面が露出しないと,購読決済を正常に使用できません。
```
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification-1.png)<br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification-2.png)<br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification-3.png)<br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification-4.png)<br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification-5.png)<br>



