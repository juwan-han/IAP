## Mobile Service > IAP > Googleコンソールガイド

> 本文書は、Google Playでリリースしたアプリの情報を[NHN Cloud IAP](http://docs.toast.com/ko/Mobile%20Service/IAP/ko/Overview/)コンソールに登録及び連動させる方法を説明します。
> Google Playでアプリをリリースするためのより詳しい内容は、Googleが提供するGoogle Play Consoleガイドを参照してください。

## Googleサイト
連動に必要な情報を得るために下記のGoogleサイトを利用します。
*[Google Play Console](https://play.google.com/console/developers)
* [Google Cloud Console](https://console.cloud.google.com)
* [Google Developers - OAuth 2.0 Playground](https://developers.google.com/oauthplayground/)

## 基本情報入力

![NHN Cloud IAPアプリ設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_iap_console_app_01.png)

### 1. **Store App ID**

* Google Play登録のためにビルドしたアプリのPackage Nameで、Google Play内でアプリを識別できる固有の値です。
* アプリを登録したら、Google Play Consoleのアプリ一覧やダッシュボードなどで確認できます。

![Google Playアプリパッケージ名](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_play_console_05.png)

### 2. **Google InApp Purchase License Key**

* ライセンス確認のためGoogle Play Consoleに接続します。
* **ホーム**画面で設定するアプリを選択し、**収益化設定**に移動します。
* 項目のうち**ライセンス**にあるBase64でエンコードされた内容をコピーして貼り付けます。

![Google Playアプリライセンスキー](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_play_console_06.png)

### 3. **マーケット連動検証省略**

* Googleの障害状況に備えたオプションで、通常はデフォルトの**NO**に設定してください。
* **YES**に設定すると、送信された決済情報の改ざん有無のみを確認し、Googleの検証を省略します。
* すべての決済に有効なわけではなく購読や再検証などには適用されません。

### 4. **Domain authentication File Names**

* 廃止予定の項目なので、空白のままにしておきます。

## 連動のための2つの認証方式を提供

* Google連携のためにはGoogle Cloud APIを使用する必要があり、Google Cloud APIはGoogleが提供するOAuth2.0認証が必要です。
* NHN Cloud IAPはGoogleのOAuth2.0認証のうち、**クライアントID**方式と**サービスアカウント**方式をサポートします。
* NHN Cloud IAP連動方式でクライアントIDは**SUPERVISOR**に、サービスアカウントは**SERVICE_ACCOUNT**にマッピングされます。
* 二つの方式の違いは以下の通りで、詳細は[GoogleのOAuth 2.0ガイド](https://developers.google.com/identity/protocols/oauth2?hl=ko)を参照してください。

**[クライアントID方式]** 
* ユーザーに代わって認証に使うクライアントIDと認証情報を生成します。
* 認証情報を生成する過程で、実際のGoogleユーザー(開発者)の承認が必要です。
* 承認はWeb上で1回だけ行われ,生成された認証情報と承認結果をWebサイトにリターンします。
* 承認されたクライアントIDでGoogle Cloud APIを使用すると,承認したユーザーと同じ権限を持ちます。
* Google Play Consoleを作成(所有)したユーザーが認証情報を作成した場合、そのクライアントIDはGoogle Play Console内のすべてのアプリにアクセスできます。

**[サービスアカウント方式]**
* Google Cloud Consoleではプロジェクトのためのサービスアカウントを作成できます。サービスアカウントはGoogleメールを持つ一般ユーザーアカウントではありません。
* Google Play ConsoleではGoogle Cloud Consoleで作成したサービスアカウントを追加して使用します。
* サービスアカウントがアプリにアクセスするためには、適切な権限を付与する必要があります。

![NHN Cloud IAPアプリ設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_iap_console_1.1.png)


## Google Cloudプロジェクト設定
* Google Playに登録されたアプリと連動するためにGoogle Cloudプロジェクトが必要です。
* 既に作られたプロジェクトがある場合は,既存のプロジェクトを使うことも可能ですが、ここではGoogle Cloudプロジェクトの作成からガイドします。

### 1. プロジェクト作成

* プロジェクトを作成するため[Google Cloud Console](https://console.cloud.google.com/)にアクセスします。
* Google Play Console開発者アカウントを所有するユーザーでログインします。
* **IAMおよび管理者 > プロジェクト作成**を選択します。
* **プロジェクト名**と**位置**を入力し、プロジェクトを作成します。

![Google Cloudプロジェクト作成メニュー](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_01.png)
![Google Cloudプロジェクト作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_02.png)

### 2. プロジェクトで使うAPIを追加

* 生成したプロジェクトを選択して、**API及びサービス > ライブラリ**メニューに移動します。
* **APIライブラリ**で使用するAPIを選択します。Google Playに登録したアプリと連動するために次のAPIが必要です。
    * **Play Android Developer API**
    * **Play Games Services Publishing API**
* 該当APIを選択後、**製品詳細**で使用に設定します。

![Google Cloud API選択](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_03.png)

### 3. Google Cloud Consoleメニュー表示

* 設定過程でGoogle Cloud Pub/Subのように見えないメニューがある場合、**製品及びソリューション > すべての製品**に入るとメニュー(固定された製品)に追加できます。

![Google Cloud固定された製品設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_13.png)

## SUPERVISOR連動方式設定
NHN Cloud IAPでGoogle CloudクライアントID認証を使用するためには、クライアントIDで作成したRefresh tokenが必要です。Refresh tokenの生成中はユーザーの承認プロセスがあり、そのためにGoogle Cloudプロジェクトで**OAuth同意画面**を設定する必要があります。Google Play Consoleに登録したアプリのアクセス権限はRefresh tokenの生成を承認したユーザーの権限に従います。

### 1. OAuth同意画面構成

* クライアントIDを作成する前に**OAuth同意画面**を設定したことがない場合は、まず**OAuth同意画面**を設定する必要があります。
* **APIおよびサービス > OAuth同意画面**で、ユーザーが認証情報の生成を承認する際に表示される画面を設定します。
* Google Workspaceを使用しなかった場合、**User Type**は**外部**のみ選択が可能です。
* 残りの構成関連設定は、画面内の**詳細**に沿って進めます。

![Google Cloud Oauth同意画面構成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_04.png)

### 2. Google CloudクライアントIDの作成

* **APIおよびサービス > ユーザー認証情報**で上部の**ユーザー認証情報の作成 > OAuthクライアントID**を選択して**OAuthクライアントIDの作成**ページに入ります。

![Google Cloudユーザー認証情報の作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_05.png)

* **アプリケーションタイプ**は**Webアプリケーション**を選択します。
* クライアントIDを識別する**名前**を入力します。
* **承認されたリダイレクトURI**は、先に設定した**OAuth同意画面**でユーザー承認後、結果を返すアドレスです。**アプリケーションタイプ**を**Webアプリケーション**に設定すると、承認された認証情報(Authorization code)をWebで受け取ります。
* 別のユーザーWebアプリケーションで認証結果を受け取りたい場合は,ユーザーのWebアドレスの設定も可能です。ここではGoogle Developersサイトを利用して認証情報を確認します。
* **承認されたリダイレクトURI**に `https://developers.google.com/oauthplayground` を入力します。

![Google Cloud Oauthクライアント作成情報入力](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_06.png)

* **作成**ボタンでOAuthクライアントを作成すると、**クライアントID**と**クライアントセキュリティパスワード**を確認できます。

![Google Cloud Oauthクライアントの作成結果](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_07.png)

### 3. OAuthクライアントでRefresh token作成

* Refresh tokenを作成するために[Google Developers - OAuth 2.0 Playground](https://developers.google.com/oauthplayground)に接続します。
* **Step 1**で認証に使用するAPIである**Google Play Android Developer API v3**の`https://www.googleapis.com/auth/androidpublisher`を選択します。
* 右上の歯車ボタンを押して**OAuth 2.0 configuration**を開き、**Use your own OAuth credentials**をチェックして追加入力欄が出るようにします。
* 先に作成した**クライアントID**と**クライアントセキュリティパスワード**を**OAuth Client ID**と**OAuth Client secret**に入力します。

![Google Developers OAuth2.0 Playground - Step1](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_playground_02.png)

* **Authorize APIs**ボタンを押してログインを進めると**OAuth同意画面**メニューで設定したページに来ます。
* 進行中のログインはGoogle Play Console開発者アカウントを所有したユーザーで行います。
* **続行**を押すと**Google Developers - OAuth 2.0 Playground**の**Step 2**にリダイレクトします。

![Google Developers OAuth2.0 Playground - 認証同意](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_playground_04.png)

* **OAuth同意画面**で**公開状態**がテスト状態なら**Googleで確認してないアプリ**画面が表示されることもあります。

![Google Developers OAuth2.0 Playground - 確認していないアプリ](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_playground_03.png)

* クライアントIDを生成する時、**承認されたリダイレクトURI**に `https://developers.google.com/oauthplayground` を入力しなかった場合、結果を受信できません。
* 正常にリダイレクトされると**Step 2**で**Authorization code**を確認できます。
* ここで**Exchange authorization code for tokens**を押して**Refresh token**と**Access token**を発行します。

![Google Developers OAuth2.0 Playground - Refresh token](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_playground_05.png)

* **Step 3**は進行しなくても構いません。

### 4. NHN Cloud IAPアプリでクライアント情報設定

* **IAP > App**の登録または修正でGoogle Cloud ConsoleとGoogle Developsersで確認した情報を入力します。
* **Google API Client ID** : **クライアントID**を入力
* **Google API Client Secret** : **クライアントセキュリティパスワード**を入力
* **Refresh Token For Google Oauth** : Google Developsers OAuth Playgroundで受信した**Refresh token**を入力

![NHN Cloud IAPアプリ設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_iap_console_app_03.png)

> [注意]<br>
> 発行されたRefresh tokenは、認証したユーザーアカウントのパスワードを変更するとすぐに失効します。もしアプリが稼働中であれば、障害が発生する可能性があります。
> 他にも有効期限が切れる場合がありますので、[GoogleのOAuth 2.0ガイド - 更新トークンの有効期限](https://developers.google.com/identity/protocols/oauth2?hl=ko#expiration)を必ずご確認ください。


## SERVICE_ACCOUNT連動方式設定
人以外のユーザーがGoogle CloudリソースにアクセスできるようにGoogle Cloud IAMでサービスアカウントを発行できます。ユーザーアカウントとの違いや運営戦略は、[Google Cloud IAMドキュメント](https://cloud.google.com/iam/docs/service-account-overview?hl=ko)または[Google Cloud認証ドキュメント](https://cloud.google.com/docs/authentication?hl=ko#credentials)を参照してください。

### 1. Google Cloudサービスアカウントの作成

* **IAMおよび管理者 > サービスアカウント**で**サービスアカウントの作成**をクリックするか、**APIとサービス > ユーザー認証情報**で**ユーザー認証情報の作成 > サービスアカウント**を選択します。

![Google Cloud IAMでサービスアカウントの作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_08.png)

![Google Cloud APIでサービスアカウントの作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_09.png)
 
* **サービスアカウント名**と**サービスアカウントID**に適切な情報を入力し、**作成して続行**を押して次に進みます。

![Google Cloudサービスアカウント入力](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_10.png)

* アクセス権限の付与は**所有者**を選択します。

![Google Cloudサービスアカウントのアクセス権限](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_11.png)

* その後,完了をするか、追加でサービスアカウントの管理者メールアドレスを登録できます。管理者メールアドレスを登録すると、作成中のサービスアカウントの管理権限を取得します。もし現在プロジェクトに参加していないユーザーメールであれば、招待メールが送信されます。

### 2. Google Cloudサービスアカウントのキー作成

* 作成されたサービスアカウントをクリックして詳細を確認します。
* **キー**タブに移動して**キーの追加 > 新しいキーの作成**を選択します。
* **キータイプ**は**JSON**を選択し、作成を押してキーファイルをダウンロードします。
* ダウンロードしたファイルの内容はNHN Cloud IAPアプリを設定する際に使用します。

![Google Cloudサービスアカウントのキー作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_12.png)

> [注意]<br>
> ダウンロードしたサービスアカウントのキーファイルは再度ダウンロードできません。紛失した場合は、キーを廃棄し、新たに作成する必要があります。
> また、キーはサービスアカウントに付与したすべての権限を使用することができますので、キーのセキュリティに十分ご注意ください。

### 3. Google Play Consoleにサービスアカウント登録

* Google Play Consoleに接続します。
* **ユーザーおよび権限**で**新規ユーザー招待**ボタンをクリックします。

![Google Cloudサービスアカウント招待](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_play_console_02.png)

* ユーザー招待画面で作成したサービスアカウントのメールアドレスを入力します。**アクセス権限の有効期限設定**はチェックしません。
* 権限はサービスアカウントの下にアプリケーションを追加してアプリごとに付与することもできますし、登録するサービスアカウントに権限を付与することもできます。ここでは**アカウント権限**で登録します。
* 範囲は顧客の意図に合わせて設定しますが、**アプリ情報の表示とレポート一括ダウンロード(読み取り専用)**、**財務データ、注文、キャンセルアンケート回答の表示**、**注文と購読の管理**は必ず選択する必要があります。
* 権限は設定後、反映されるまである程度の時間がかかる場合があります。場合によっては7日程度の時間がかかることもあります。
* サービスアカウントは招待後、ユーザーのメール承認プロセスなしで有効になります。

![Google Cloudサービスアカウント権限付与](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_play_console_03.png)

> Googleの一般ユーザーアカウントもGoogle Cloudのプロジェクトに主メンバーとして登録されており、Google Play Consoleでユーザー招待と権限を付与すれば、SUPERVISOR方式のようにクライアントIDでGoogle Cloud APIアクセスが可能です。

### 4. NHN Cloud IAPアプリでサービスアカウント設定

* **IAP > App**の登録または修正で**サービスアカウント連動情報**項目にダウンロードしたサービスアカウントのキーファイルの内容を入力します。
* コピーする際は、メモ帳などのテキストエディタを使用して内容全体をコピーしてください。

![Google Cloudサービスアカウント情報の入力](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_iap_console_app_02.png)


## リアルタイム購読状態を受信するためのGoogle通知設定
Google Playで購読商品を販売する場合、NHN Cloud IAPではGoogleから通知を受け取り、購読の最新状態を管理できます。購読商品の更新は、更新時にGoogle内で自動的に行われます。このようなGoogle内で発生する購読イベントを追跡するため、Google Cloudの**トピック(Topic)**を使用します。トピックに関する追加内容は[Android Developers - トピックの作成](https://developer.android.com/google/play/billing/getting-ready#create-topic)で確認できます。

### 1. Google Cloud通知トピックの作成

* [Google Cloud Console](https://console.cloud.google.com/)に接続します。
* **Pub/Sub**で**トピックの作成**をクリックします。
* **トピックID**を入力し、**基本購読の追加**と**Google管理暗号化キー**を選択してトピックを作成します。
* **Pub/Sub** メニューが表示されない場合は、**製品およびソリューション > すべての製品**からアクセスできます。

![Google Cloud Pub/Subトピック](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_14.png)

![Google Cloud Pub/Sub トピックの作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_15.png)

* トピックが作成されたら、購読イベントが発生した際にトピックに掲示する掲示者を追加する必要があります。作成されたトピックを選択した後、**権限**タブで**主メンバーの追加**をクリックします。
* **新しい主メンバー**には`google-play-developer-notifications@system.gserviceaccount.com`を、**ロール選択**には掲示/購読 > **掲示/購読掲示者**を選択して保存します。

![Google Cloud Pub/Sub トピックに掲示者を追加](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_16.png)

### 2. トピックに掲示する購読設定

* トピックを作成すると、**購読**メニューで該当トピックの購読が一緒に作成されたことが確認できます。
* 購読修正に移動し、**送信タイプ**は**プッシュ**を選択し、**エンドポイントURL**はNHN Cloud IAPの通知受信アドレスである`https://api-iap.cloud.toast.com/callback/subscription/{YOUR_PACKAGE_NAME}/GG` を入力します。入力時に`{YOUR_PACKAGE_NAME}`は、上記のNHN Cloud IAPアプリ基本情報入力中の**Store App ID**と同じ値に置き換えてください。
* Gamebaseサンドボックスを使用している場合、**エンドポイントURL**は`https://sandbox-api-iap.cloud.toast.com/callback/subscription/{YOUR_PACKAGE_NAME}/GG`と入力します。
* すでに作成されたトピックに購読を追加したい場合は、**購読の作成**で購読を追加することもできます。

![Google Cloud Pub/Sub購読情報の入力](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_cloud_console_17.png)

### 3. Google Play Consoleに購読 トピック 登録

* **ホーム**画面で通知を受けるアプリを選択し、**収益化設定**に入ります。
* **Google Play決済**項目のうち**トピック 名**に先に作成したトピックの**トピック 名**を入力します。

![Google Play通知 トピック 登録](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_google/google_play_console_04.png)
