## Mobile Service > IAP > Overview

> [お知らせ]
> 定期購入決済をサポートする新規のIAP SDKが[TOAST SDK](http://docs.toast.com/ja/TOAST/ja/toast-sdk/overview/)として発売されました。
> 既存のIAP SDKはこれ以上新規機能を開発しない予定です。
> 本文書は[TOAST SDK](http://docs.toast.com/ja/TOAST/ja/toast-sdk/overview/)ガイドです


In-App Purchase (以下IAP)サービスはアプリ内決済の統合ソリューションです。


## 主要機能

TOAST IAPは次のような機能を提供します。

* Google Play、Apple AppStore のアプリ決済に対し、ひとつのインターフェイスで連動します。
それぞれのストアー別の決済連動の仕様を学びなおす必要はありません。
* IAPで提供する決済検証サーバーを通じて決済することで、セキュリティおよび安定性を高めます。
* GoogleとAppleの定期購入決済およびプロモーション機能をサポートしています。
* 顧客サポートのためにウェブコンソールで決済内訳照会機能を提供します。

## サポートするストア

| プラットフォーム | ストアー |
| --- | --- |
| Android | Google |
| Android | ONEstore (Korea only)|
| iOS | Apple |

## サポートする商品タイプ

| ストア | ストア商品タイプ| IAP商品タイプ|    
|---|---|---|
| Google Play Store| One-time, Subscriptions | CONSUMABLE, AUTO_SUBSCRIPTION |
| App Store| Consumable, Auto-Renewable | CONSUMABLE, AUTO_SUBSCRIPTION |
| ONEStore|	Managed product | CONSUMABLE|

## サービス用語

| 用語 | 説明 |
| --- | --- |
| AppKey | TOAST Cloud ユーザープロジェクトと商品間の1:1 マッチングキー. 1プロジェクト当たり1つのIAP向けAppKeyを発給する。 |
| ストア(Store) | App Store、 Google Playのようなアプリを販売・配信する窓口となるオンラインアプリストア |
| 決済内訳(Payment) | 使用者が決済した内訳 |
| 決済要請(Purchase) | アプリ内、あるいはストアでアイテムを購入する。 |
| 決済消費(Consume) | 使用者にアイテムを生成する前に決済を消費すること。 |
| Payment Access Token | ユーザーアプリケーションサーバが決済を消費する際に使用する認証トークン |

## サービス構造

IAPサービスでは次の図のように、IAP SDK、ユーザーアプリケーションサーバー、 IAPサーバー、プラットフォーム別ストアの4つで構成されます。

![[図1 IAPサービス構造 - Server To Server Model]](http://static.toastoven.net/prod_iap/iap_n_1.png)


![[図2 IAP サービス構造 - Build-in Model]](http://static.toastoven.net/prod_iap/iap_n_23.png)


| コンポーネント名 | 説明 |
| ----- | --- |
| IAP SDK | アプリ内決済のためにユーザーID登録、決済リクエストを実行します。 <br> 決済を行う際、ストア(Androidの場合、Google Store)のアプリ内決済画面に移動します。 |
| User Application Server | ユーザーアプリケーションのサーバーです。 <br> IAP サーバーを通じてクライアントが要請した決済内訳を確認した後、決済消費を進め、アイテムの伝達を行います。 |
| User Application Client | ユーザーアプリケーションにサーバーが存在しない場合は、アプリケーションのクライアントで決済消費を行い、アイテムに対する権限を与えることになります。 |
| IAP Server | TOAST Cloudで提供するアプリ内決済サーバーです。|
| Store | Google Store、Apple App Storeなどのさまざまなストアです。 プラットフォーム別ストアはIAPサーバーと連動しています。 |


## IAP 決済フローチャート


![[図3 Server To Server Model 決済フローチャート]](http://static.toastoven.net/prod_iap/iap_n_28.png)


![[図4 Build-in model決済フローチャート]](http://static.toastoven.net/prod_iap/iap_n_29.png)


| Step | Description |
| ---------- | ----------- |
| [1] | 決済ユーザー ID を登録します。 <br>決済者は開発会社で使用者を識別し、アイテムを支給する対象であり、Google playやApp Storeアカウントではありません。<br>**[参照]**<br>API Step<br>Android:InternalInAppPurchase。InAppPurchase。 |
| [2] | クライアントから決済を要請します。<br>**[参照]** <br>API Step<br>Android : InternalInAppPurchase..InAppPurchases.requestPurchase<br>iOS : TIAPurchase startPurchaseWithViewController: itemId: completionHandler |
| [3]<br>[3-1] | ストアで決済を進めます。 |
| [4] | ストアで決済が完了したら、決済結果を受領します。<br> 受け取った結果を利用してユーザーアプリケーションサーバーでアイテム消費を行います。<br>**[注意]** <br>アプリケーションサーバーが存在しないモデルは決済消費をクライアントで直接検証できますが、 <br/> セキュリティー上のイシューにより、サーバー間で決済消費後、アイテムに対する権限を与えることを強く推奨します。 |
| [4-1]<br>[4-2] | ストアから受け取った結果により、IAP サーバーに消費リクエストを行います。 |
| [5] | Consumeを成功させると、ユーザーにitemをお届けします。 |
| [6] | 決済を完了します。 |
