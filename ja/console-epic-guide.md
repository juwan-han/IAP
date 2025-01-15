## Mobile Service > IAP > EPICコンソールガイド

本書はEpic Games Store(以下Epic)と連動する方法について取り扱います。
Epicに製品をリリースするためのより詳しい文書は、[Epic開発者リソース文書](https://dev.epicgames.com/docs/ko)を参照してください。

>[参考]
> 現在該当ストアの連動はGamebase SDKを通じて実施できます。
> 従って連動が必要な場合は、[Gamebaseガイド](https://docs.nhncloud.com/ko/Game/Gamebase/ko/Overview)を参照して作業してください。

## Epicプロジェクト接続
連動と関連する情報は[Epic Devポータル](https://dev.epicgames.com/)で作成します。
Epicが製品配布のために提供する環境は次のとおりです。

![Epicサンドボックス環境](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_sandbox_01_kor.png)

* EpicはDev、Stage、Liveの3つのサンドボックスを基本提供し、各サンドボックスの下位に開発者がデプロイを作成できます。
* IAPアプリは、Epicのサンドボックス内に作成されたデプロイとマッピングされ、アプリ情報で使用する**Store APP ID**は**デプロイID**です。

### デプロイ作成
* **製品設定 > サンドボックス**メニューでデプロイを作成します。

![Epicデプロイ作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_sandbox_02_kor.png)

### クライアント作成
* IAPがEpicと通信するためにはEpicのOAuthクライアントが必要です。
* **製品設定 > クライアント**メニューでIAPに使用するクライアントを作成できます。
> クライアントを作成する前にクライアントポリシーを先に作成してください。

* クライアントを作成するためには、クライアントに適用するポリシーを先に追加する必要があります。
  * クライアントポリシー名は任意の名前を設定します。
  * クライアントポリシータイプは**TrustedServer**を選択します。
  * **Ecom**機能を有効にします

![Epicクライアントポリシー作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_app_05_kor.png)

* クライアントポリシーの追加後にクライアントを作成します。

![Epicクライアント作成](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_app_02_kor.png)

### デプロイおよびクライアント情報確認
* 作成されたデプロイとクライアント情報は、**製品設定 > SDKダウンロードおよびクレデンシャル**メニューで確認できます。

![Epicアプリ情報](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_app_03_kor.png)

* **デプロイID**、**クライアントID**、**クライアント秘密鍵**、**サンドボックスID**をIAPアプリ情報に登録します。

![Epicアプリ登録](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_app_04_kor.png)


## アイテム(オファー)接続
* Epicのアイテムはストアのオファーで管理します。
* オファーはエディション、デモなどの所有するオファーと購入後に消費する消耗型オファーに分けられます。
* IAPではこの内、消耗型オファーのみをアイテムとして管理します。

### オファー登録
* **Epic Game Store > オファー**メニューでオファーを登録します。
* オファータイプで消耗型を選択します。

![Epicオファー登録](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_item_01_kor.png)
![Epicオファー登録](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_item_02_kor.png)

### アイテムIDの確認およびIAP登録
* アイテムIDの確認は登録後、オファーの詳細情報から確認できます。
* ID項目で**対象アイテムID**をIAPの**Store Item ID**に登録します。

![Epicアイテム登録](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_item_03_kor.png)
![Epicアイテム登録](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_epic/epic_console_item_04_kor.png)
