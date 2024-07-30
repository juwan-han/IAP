## Mobile Service > IAP > STEAMコンソールガイド

> 本文書は、Steamworksでリリースされたアプリの情報を[NHN Cloud IAP](https://docs.nhncloud.com/ko/Mobile%20Service/IAP/ko/Overview/)コンソールに登録して連動する方法を説明します。
> Steamアプリをリリースするための詳細は、[Steamworksガイド文書](https://partner.steamgames.com/doc/home)を参照してください。


## 基本情報の入力

Steam連動のために以下の3つの情報を正確に入力してください。

連動に関する情報は[Steamworks](https://partner.steamgames.com/)で作成します。

その他、本ページで説明しない項目は、 **Mobile Service > IAP > [コンソール共通使用ガイド](https://docs.alpha-nhncloud.com/ko/Mobile%20Service/IAP/ko/console-guide/)**を参照してください。


![NHN Cloud IAPアプリ設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_01_kor.png)


### Steam App ID

* Steamworksで製品を登録した後に発行されるアプリの固有識別情報です。
* **Steamworks > App Admin >** (プロジェクト名)に表示されたApp IDを入力します。

![STEAM App ID](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_02_kor.png)


### Steam Web API Key

* [ISteamMicroTxn Interface](https://partner.steamgames.com/doc/webapi/ISteamMicroTxn)(Steam決済API)にアクセスするために必要な情報です。
* **Steamworks > Users & Permissions**で新規作成または発行済みのキー値を入力します。
  * より詳細な発行方法は[Steamworks Publisher Web API Key](https://partner.steamgames.com/doc/webapi_overview/auth)を参照してください。

![STEAM Web API Key](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_03_kor.png)


### Steamの基本通貨

* ユーザーが購入を試行し、Steam決済オーバーレイに入る際、アイテム価格に適用される通貨コードのデフォルト値を設定できます。
* ユーザーのSteamウォレットの通貨と一致する通貨コードがアイテム情報に存在しない場合、本項目で設定された基本通貨で商品の価格が出力されます。
  * **販売アイテム設定**セクション内の **国別販売アイテム情報の入力**項目をご参照ください。


STEAMのデフォルト通貨](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_04_kor.png)



## 販売アイテム設定

NHN Cloud IAPは[Steam Microtransaction API](https://partner.steamgames.com/doc/features/microtransactions)をサポートします。

![NHN Cloud IAPアイテム設定](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_05_kor.png)



### アイテム基本情報の入力

- **Item名前**: IAPコンソールで管理するアイテムの代表的な名前を入力します。
- **Store Item ID**:アプリで管理するアイテムIDを入力します。

> 各アイテムのStore Item IDは固有の値で入力する必要があり、`uint32`タイプのみ入力可能です。
> \* 0～4,294,967,295の間の数字

- **Product Type**:現在、消費性アイテム(`CONSUMABLE`)のみをサポートしています。


### 国別販売アイテム情報の入力
入力されたアイテムの名前や価格などは、購入しようとしたユーザーに実際に請求される情報なので、入力および修正する際は注意してください。

- **言語コード**:決済画面に表示されるアイテム名に対応する言語コードを選択します。
- **国別アイテム名**:選択した通貨コードで販売するアイテムの名前を入力します。
- **通貨コード**:販売価格に対応する通貨コードを選択します。
- **通貨別販売価格**:選択した通貨コードに対応する価格を入力します。


> アプリ設定内の基本通貨コードに対応する価格情報は必須入力値です。
> 2種類以上の価格情報を入力すると、ユーザーのSteamウォレットにチャージされた財貨の通貨コードに対応する価格で決済情報を作成します。
> (入力されたアイテム情報のうち、ユーザーのウォレットの通貨コードに対応する情報が存在しない場合、基本通貨コードで決済情報を作成します)
