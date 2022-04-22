## Mobile Service > IAP > Amazon Appstoreコンソールガイド

> [告知]
> 購読決済をサポートする新規IAP SDKが[NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)としてリリースされました。
> 従来のIAP SDKは、新規機能を開発しない予定です。
> この文書は[NHN Cloud SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)ガイドです。

## Amazon Developer Console

1. [Amazon開発者コンソール](https://developer.amazon.com/)にアカウントを登録し、Amazon AppStore管理メニューでアプリを作成します。
   ![Amazon開発者コンソール](http://static.toastoven.net/prod_iap/amazon_developer_console_eng.png)
2. NHN Cloud IAPは、AndroidプラットフォームのAmazon AppStoreアプリのみを公式サポートします。Androidプラットフォームを選択し、アプリ名を入力たら`Create app`ボタンをクリックしてアプリを作成します。
   ![アプリプラットフォーム選択](http://static.toastoven.net/prod_iap/amazon_appmenu_0_eng.png)
3. アプリを作成すると、次のように作成されたアプリのリストを確認できます。
   ![AppStore開発者コンソールのアプリリスト](http://static.toastoven.net/prod_iap/amazon_appmenu_1_eng.png)
4. アプリ作成後に追加情報を入力し、開発者コンソールで提供する情報をNHN Cloud IAPコンソールのアプリ設定に入力する必要があります。
5. このガイドの内容はAmazon AppStoreに登録されたアプリの情報とNHN Cloud IAP間のアプリ情報を接続するためのガイドだけを扱っており、より詳細なAmazon AppStoreのアプリ登録手順については[Amazonのガイド文書](https://developer.amazon.com/apps-and-games/documentation)を参照してください。

## 接続に必要な設定値

![NHN Cloud IAPアプリ設定ポップアップ](http://static.toastoven.net/prod_iap/amazon_iap_console_kor.png)

### Store App ID

'- Amazonコンソールから提出済み、または提出予定のアプリのビルド情報に入力したAndroidパッケージ名を入力します。
'- すでにアプリを提出している場合は、次の手順でAmazonコンソール画面で確認できます。
    - [アプリリスト](https://developer.amazon.com/apps-and-games/console/apps/list.html)画面で作成されたアプリの名前をクリックして詳細設定メニューに移動
    - アプリ詳細設定画面で**APK Files** > **Manifest**をクリック
      ![Amazon開発者コンソールのAPK Files](http://static.toastoven.net/prod_iap/amazon_app_store_id_01.png)
      ![Amazon開発者コンソールのAPK Files](http://static.toastoven.net/prod_iap/amazon_app_store_id_02.png)

### Amazon Shared Key

- Amazon開発者コンソールの[Settings -> Identityメニュー](https://developer.amazon.com/settings/console/sdk/shared-key)に移動すると、以下のような画面で共有キーを確認できます。
  ![Amazon開発者コンソールのIdentity画面](http://static.toastoven.net/prod_iap/amazon_appmenu_3_eng.png)
- この値をNHN Cloud IAPコンソールアプリ設定の`Amazon Shared Key`項目に入力する必要があります。
