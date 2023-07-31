## Mobile Service > IAP > コンソール共通使用ガイド

ストアでアプリとアイテムを登録した後、IAPコンソールでアプリとアイテムを登録します。

<br>


## プロジェクト生成
```
Console (https://console.toast.com) > Click [+ プロジェクト作り]
```
![[プロジェクト生成]](http://static.toastoven.net/prod_iap/iap-console-new-project.png)


## IAP商品の有効化
```
Console (https://console.toast.com)  > [Mobile Service] > Click [IAP]
```
![[IAP商品の有効化]](http://static.toastoven.net/prod_iap/iap-console-iap-on.png)


## AppKey確認
```
"URL & Appkey"をクリックしてAppKeyを確認し、SDKの設定に使用します。
```
![[AppKey 확인]](http://static.toastoven.net/prod_iap/iap-console-appkey.png)


## アプリ登録
ストアー別の設定はストアーガイドを参考にしてください。
```
1. [App] Tab Click > [追加]ボタン·クリック
2. [Store ID]からストアー選択
3. 共通情報
   - Store ID : Google, Apple, ONE Store
   - App Name : アプリ名
   - Store APP ID : ストア package name or bundle id
4. [追加]ボタン·クリック
```
![[アプリ登録]](http://static.toastoven.net/prod_iap/iap-console-new-app.png)

## アイテム登録
```
1. [Item] Tab Click > [追加]ボタン·クリック
3. [Item 名前] : アイテム名を入力
4. [Store Item ID] : ストアに登録したアイテムIDを入力 
5. [Product Type] : CONSUMABLE , AUTO_RENEWABLE
5. [状態] 選択  
6. [追加] ボタンをクリック
```

![[アイテム登録]](http://static.toastoven.net/prod_iap/iap-console-new-item.png)

## ストア商品タイプ
```
各ストア開発者センターで登録したIn App Productsの商品タイプを参考にアイテムを登録します。
```

| Store | Store Product Type| IAP Supported |    
|---|---|---|
| Google Play Store| One-time, Subscriptions | CONSUMABLE, AUTO_SUBSCRIPTION |
| App Store| Consumable, Auto-Renewable | CONSUMABLE, AUTO_SUBSCRIPTION |
| ONE Store|	Managed product | CONSUMABLE|


<br>
<br>



> [注意]  
> 正確でない商品タイプで決済を進行した場合のシステムエラーおよび金銭的損失被害は責任を負いません。

## 決済照会
```
1. Click [Transaction] Tab  
2. [Search Condition] > 必要項目選択
   - Store ID / Date : ストア+日付複合検索
   - Store Reference Key : ストアー決済番号の単一検索
3. [Date] : 最大1ヶ月照会可能。
4. [整列手順]で整列条件を選択します。
5. [検索] ボタンをクリックします。
```
![[결제 조회]](http://static.toastoven.net/prod_iap/iap_new_01.png)


<br>
<br>

> [参考] 決済状態  
> - Reserved : 決済準備完了(IAPサーバーに決済予約リクエストは完了したが検証リクエストがなかった場合)   
> - Failure : 決済検証失敗 (ストアーで決済を進めたが決済検証でエラーが生じた場合)
> - Success : 決済完了 
> - Refund : 払い戻し完了 (管理者が手動で返金したと変更した場合)



## 決済状態の変更
```
以下のような状況の場合、決済状態を変更することができます。

1. 決済課金は実際に行われているのに、IAPの内部イシューで決済状態が正確に反映されなかった場合 ('Success'状態に変更)
   1.1 'Success'の状態に変更するためには、図7のように領収書情報と決済が行われた価格、通話を記入しなければなりません。

2. 決済が終わってから消費処理をせず、ユーザーがアイテムを貰えなくて払い戻し処理をした場合 (Refunded状態に変更)
   2.1 "Refunded"状態に変更された場合、クライアントの未消費決済内訳の照会APIで照会されません。

変更が可能な決済状態は、下記のように状態コラム右側に [変更] ボタンが露出されます。
```
![[決済状態変更]](http://static.toastoven.net/prod_iap/iap_new_03.png)
![[決済状態追加加入]](http://static.toastoven.net/prod_iap/iap_46.PNG)


## 決済統計照会
```
1. Click [Statistics] Tab  
2. Click [Currency]  
3. [<][>] ボタンでストアー別"今月総収入"、"日別詳細内訳"を月別に照会することができます。  
```
![[図 6 決済統計紹介]](http://static.toastoven.net/prod_iap/iap_n_35.png)


