## Mobile Service > IAP > Apple 設定ガイド

Apple定期購入商品の決済を使用するには、App Store Connectでsecret key生成およびNotification url設定が必要です。<br>
Secret KeyはIAPアプリ情報に登録します。<br>
Apple一般商品決済は特別な設定が必要でありません。




> 参考<br>
> https://help.apple.com/app-store-connect/#/devf341c0f01

## shared secret key 生成下期
```
shared secret keyはすべてのアプリに共通したマスターキーで生成でき、アプリ別に生成することもできます。
secret keyをIAPアプリ情報に登録します。
```

### master shared secret key 生成下期
```
1. App Store Connect
2. Click [My Apps] 
3. Click [Master Shared Secret]
```
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-shared-key-1.png)

<br>

### App-specific shared secret key
```
1. App Store Connect
2. Click [My Apps]  > Click App>  Click [Features] in toolbar
3. Click [App-Specific Shared Secret]
```
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-shared-key-2.png)


### IAPアプリ情報にshared secret key入力する。
```
1. IAP Console > App > choose ios APP
2. Apple Shared Secret 入力
```
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-edit.png)



## Notification url 登録する
**Notification V2** はサポートされていません。**V1** を使用してください。
```
1. App Store Connect > My Apps > App information> General
2. 定期購入（サブスクリプション）状態URL にIAP urlを登録します。
- URL : https://api-iap.cloud.toast.com/callback/subscription/{YOUR_PACKAGE_NAME}/AS
- {YOUR_PACKAGE_NAME} : app bundle id
```

