## Mobile Service > IAP > Apple設定ガイド

> この文書、はApp Storeにリリースされたアプリの情報を[NHN Cloud IAP](https://docs.nhncloud.com/ko/Mobile%20Service/IAP/ko/Overview/) コンソールに登録及び連動させる方法を説明します。
> 連動方法は**(新)領収書検証 + Notification V2**, **(旧)領収書検証 + Notification V1**の2つの方法に分かれています。

## (新)領収書検証 + Notification V2
> この方式を正常に使用するには、**NHN Cloud SDK iOS v1.7.0 バージョン以上**が必要です。

### アプリ内購入キーの生成
> **参考** 
> [https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-keys-for-in-app-purchases](https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-keys-for-in-app-purchases)
1. **App Store Connect** > **ユーザーおよびアクセス** > **キー**タブをクリック
2. **キータイプ** > **アプリ内購入**をクリック
3. **アプリ内購入キーの生成**ボタンをクリック
4.キー名を入力し、生成ボタンをクリック
5. アプリ内購入キーのダウンロードリンクをクリック
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-in-app-purchase-key.png)

### IAPアプリ情報にアプリ内購入キーを入力
1. [コンソール接続](https://console.nhncloud.com) > **組織及びプロジェクトの選択** > **Mobile Service** > **IAP** > **App** > **追加**及びAppを選択し、**編集**ボタンをクリック
2. Store APP ID: **App Bundle ID**を入力
3. 領収書検証およびノーティ方式: **(新)領収書検証 + Notification V2** 選択
4. ダウンロードしたアプリ内購入キー、Key ID、Issuer ID入力
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-edit-v2.png)

### Notification V2 URL登録
1. **App Store Connect** > **マイアプリ** > **アプリ選択** > **一般情報** > **アプリ情報** > **App Storeサーバー通知**
2. **プロダクションサーバーURL** または **SandboxサーバーURL**編集をクリック
3. 通知バージョン: **バージョン2通知**を選択
4. サーバーURL: `https://api-iap.cloud.toast.com/callback/subscription/{APP_BUNDLE_ID}/AS/v2`を入力


## (旧)領収書検証 + Notification V1 (Deprecated予定)
> この方式を正常に使用するには**NHN Cloud SDK iOS v1.7.0以前のバージョン**を使用する必要があります。

Appleサブスクリプション商品決済を使用するには、App Store Connectで共有パスワードの作成とNotification V1 URLの設定が必要です。
共有暗号はIAPアプリ情報に登録します。<br>
Apple一般商品決済は別途設定が必要ありません。

### 共有パスワードの作成
> **参考**
> すべてのアプリのための単一のパスワードである**基本共有パスワード**または個々のアプリのための**アプリ共有パスワード**を作成できます。
> [https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-a-shared-secret-to-verify-receipts](https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-a-shared-secret-to-verify-receipts)

#### 基本共有パスワード
1. **App Store Connect** > **ユーザーとアクセス** > **共有パスワード**タブをクリック
2. 作成をクリック
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-primary-shared-secret.png)

#### アプリ共有パスワード
1. **App Store Connect** > **マイアプリ** > **アプリを選択** > **一般情報** > **アプリ情報** > **アプリ共有パスワード** > **管理**をクリック
2. 作成をクリック
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-app-specific-shared-secret.png)

### IAPアプリ情報にshared secretを入力
1. [コンソール接続](https://console.nhncloud.com) > **組織およびプロジェクトを選択** > **Mobile Service** > **IAP** > **App** > **追加** およびAppを選択し、**編集**ボタンをクリック
2. Store APP ID: **App Bundle ID**を入力
3. 領収書検証およびノーティ方式: **(旧)領収書検証 + Notification V1** 選択
4. Shared Secretを入力
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-edit-v1.png)

### Notification V1 URL登録
1. **App Store Connect** > **マイアプリ** > **アプリを選択** > **一般情報** > **アプリ情報** > **App Storeサーバー通知**
2. **プロダクションサーバーURL** または **SandboxサーバーURL**編集をクリック
3. 通知バージョン: **バージョン1通知**を選択
4. サーバーURL: `https://api-iap.cloud.toast.com/callback/subscription/{APP_BUNDLE_ID}/AS`入力


## (旧)領収書検証 + Notification V1 -> (新)領収書検証 + Notification V2変更時の注意事項
- App運営中に変更する場合、**障害**が発生するため、必ず**点検中に変更**してください。
- Appの点検中に**(新)領収書検証 + Notification V2**ガイドを参照して進行してください。
  - Product App変更前Sandbox Appで十分なテストを行ってから作業してください。
- 点検を終えた後、ユーザーはAppの最新バージョンを使用するために**強制アップデート**が必要です。
  - 最新バージョンではない場合、ユーザーはApp実行中に**エラー**が発生する可能性があります。
