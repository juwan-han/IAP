## Mobile Service > IAP > Google 設定ガイド

> [お知らせ]
> 定期購入決済を支援する新規のIAP SDKが[TOAST SDK](http://docs.toast.com/ja/TOAST/ja/toast-sdk/overview/)として発売されました。
> 既存のIAP SDKはこれ以上新規機能を開発しない予定です。
> 本文書は[TOAST SDK](http://docs.toast.com/ja/TOAST/ja/toast-sdk/overview/)ガイドです


Google一般商品および定期購入商品のアプリ内決済のためにGoogle Play Billingと連動しなければなりません。<br>
Google Play Billingは、Google Play ConsoleとGoogle API Consoleで生成された値を使用します。<br>
さらに、Google定期購入商品の決済のため、Notificationを設定する必要があります。<br>
Notificationの設定が正しくなければ定期購入決済が進行しません。




## Google Application Key
下記情報をIAPアプリ情報に登録します。

| Key | Description                                             |
| ---------------------------------- | ---------------------------------------------- |
| Google In App Purchase License Key | Google Play Public KEY(RSA)       |
| Google API Client ID               | Google API Project OAuth Client ID            |
| Google API Client Secret           | Google API Project OAuth Client Secret        |
| Refresh Token For Google OAuth     | Google Play Developer アカウントを通じて取得したRefresh Token |


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
![[]](http://static.toastoven.net/prod_iap/iap_google_license_ja.png)


## Google API Console

> [参考]<br>
> [Android Developers - アプリ内決済管理](http://developer.android.com/google/play/billing/billing_admin.html) <br>
> [Android Developers - Authorization](https://developers.google.com/identity/protocols/OAuth2WebServer)

### OAuth クライアント生成
```
Google Play Consleと同一のアカウントでGoogle API Consoleにプロジェクトを生成します。
下記の図を参照して、OAuth 認証に必要な情報3つを生成します。
1) Client ID  
2) Client Secret  
3) Refresh Token  
```
<br>

##### 1. https://console.droパス google.com/apis/credentialsでオイスクライアントを生成(ウェブアプリケーション)
![[図 1] OAuth クライアント生成 1](http://static.toastoven.net/prod_iap/iap_google_credentials_ja.png)


##### 2. 承認された redirection urlに https://developers.google.com/oauthplayground 入力
![[図 2] OAuth クライアント生成 2](http://static.toastoven.net/prod_iap/iap_google_Oauth_ja.png)

##### 3. 作成後にポップアップウィンドウからクライアントID /クライアントシークレットをコピーする
![[]](http://static.toastoven.net/prod_iap/iap_google_Oauth_clientSecret_ja.png)

##### 4. [OAuth Playground](https://developers.google.com/oauthplayground/) > oauthplayground 設定 > Use your own OAuth credentials 使用
![[図 4] OAuth クライアント生成 3](http://static.toastoven.net/prod_iap/iap_g_03.png)


##### 5. Step 1で https://www.googleapis.com/auth/androidpublisher 入力して Authorization code コード発給
![[図 5] OAuth クライアント生成 4](http://static.toastoven.net/prod_iap/iap_g_04.png)


##### 6. Step 2で Exchange authorization code for tokens ボタンを押してトークン発給
![[図 6] OAuth クライアント生成 5](http://static.toastoven.net/prod_iap/iap_g_05.png)


## Google Playとの連動における注意事項

OAuth 認証情報を生成したら、以下のガイドを参考にプロジェクト設定を進めます。

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

### Google Play開発者コンソールのリンクされたプロジェクトがGoogleAPIのOAuthクライアントを作成プロジェクトと同じであることを確認します。
![[]](http://static.toastoven.net/prod_iap/iap_google_linked_ja.png)

## Google real-time developer notification 設定

> [参考]<br>
> Google Cloud (https://cloud.google.com) Platformを使用しなければなりません。<br>
> Google Cloud Platform に決済プロフィールを登録し、使用状態に変更しなければなりません。


### Google Cloud > ビッグデータ > 掲示/購読

Pub/Subコンソール(https://console.cloud.google.com/cloudpubsub)で下記の作業を行います。

#### トピックの作成 (プロダクト > Pub/Sub)

```
1. トピックが生成されると、オプションの権限をクリックするか、もしくはトピック名をクリックし、トピック詳細情報ページに移動します。
2. トピックの詳細情報ページで、役割の選択をクリックし、Pub/Sub パブリッシャーを選択します。
3. メンバーの追加に google-play-developer-notifications@system.gserviceaccount.com を入力します。
4. 追加ボタンをクリックします。
```
![[] トピックの再生](http://static.toastoven.net/prod_iap/iap_google_createTopic_ja.png)
![[] トピックの修正](http://static.toastoven.net/prod_iap/iap_google_addMember_ja.png)

<br>

#### サブスクリプションの作成
```
1. トピック右クリック > 新しいサブスクリプション
2. 転送タイプ
- [エンドポイントURLでプッシュ] 選択
- URL :  https://api-iap.cloud.toast.com/callback/subscription/{YOUR_PACKAGE_NAME}/GG
- {YOUR_PACKAGE_NAME} : google package name
```
![[] サブスクリプションの作成](http://static.toastoven.net/prod_iap/iap_google_new_subscirption_ja.png)
![[] サブスクリプションの作成](http://static.toastoven.net/prod_iap/iap_google_create_subscription_ja.png)

<br>

#### IAP ドメイン検証
```

1. https://console.cloud.google.com/apis/credentials/domainverification
2. [ドメイン確認]タブで、[ドメイン追加] をクリックします。
3. https://api-iap.cloud.toast.comを入力します。
4. [今移動]ボタンを押してウェブマスターセンターに移動します。
5. ウェブマスターセンターでプロパティを合わせることをクリックします。
6. [プロパティ追加]に https://api-iap.cloud.toast.com を入力します。
7. ドメイン認証URLのhtmlファイル名をTOAST CONSOLEアプリの登録時に入力します。
    -> 例) https://api-iap.cloud.toast.com/googleabc.htmlの場合、googleabc.html入力
8. [推奨方法] 下段の [ロボットではない] クリック後、[OK] をクリックします。
9. 認証に成功すると、最後のイメージと同じ画面が表示されます。 この画面が表示されないと、定期購入決済を正常に使用できません。
```
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification_ja_1.png) <br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap_google_add_domain_ja.png) <br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification_ja_3.png) <br>
![[] domain verification](http://static.toastoven.net/prod_iap/google_domain_auth.png) <br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification_ja_4.png) <br>
![[] domain verification](http://static.toastoven.net/prod_iap/iap-console-domain-verification_ja_5.png) <br>



### Realtime developer notifications
````
https://play.google.com/console/developers > [Select App] > Monetize > Monetization setup > Real-time developer notificqations
````
![[]realtime notification](http://static.toastoven.net/prod_iap/2020/google_realtime_notification_en.png)