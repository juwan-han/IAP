## Mobile Service > IAP > Overview


> [Notice]
> A new IAP SDK that supports subscription has been released as [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).
> No new features will be developed for the existing IAP SDK.
> This document is the guide for [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).

In-App Purchase (IAP) service is an integrated in-app purchase service.

## Features

IAP offers the following features.

* Various in-app purchases, such as Google Play and Apple App Store, are integrated in a single interface. 
There is no need to study over detailed payment sync process for each store. 
* Security will become more powerful with purchase verification server provided by IAP. 
* IAP supports subscription , promoting of Google and App Store.
* Web console provides purchase history inquiry function for customer support.


## Available Store

| OS Type | Store |
| --- | --- |
| Android | Google Play |
| Android | One Store (Korea Only) |
| iOS | Apple App Store |



## Terms

| Term | Description |
| --- | --- |
| AppKey | These are terms for IAP service. |
| Store | App Store, Google Play |
| Payment | User purchase history |
| Purchase | Item purchased in-app |
| Consume | Consuming purchase before creating item for user. |
| Payment Purchase Token | Verification token used when user application server consumes purchase. |

## Service Diagram

IAP service is comprised of 4 components as in following figure: IAP SDK, User Application Server, IAP Server, and Market.

![[Figure 1 IAP Service Diagram - Server To Server Model]](http://static.toastoven.net/prod_iap/iap_n_1.png)
<center>[Figure 1 IAP Service Diagram - Server To Server Model]</center>

![[Figure 2 IAP Service Diagram - Build-in Model]](http://static.toastoven.net/prod_iap/iap_n_23.png)
<center>[Figure 2 IAP Service Diagram - Build-in Model]</center>

| Component | Description |
| ----- | --- |
| IAP SDK | Register User ID and request payment for in-app purchase. If payment is performed, you’ll move to in-app purchase screen of the store (Google Store for Android). |
| User Application Server | Verify purchase history requested by client via IAP server, consume purchase and transfer item. |
| User Application Client | If there is no server existent to user application, perform payment consume in application’s client and grant authority for item.  |
| IAP Server | This is in-app purchase server provided by NHN Cloud|
| Store | It includes various stores such as Google Store and Apple App Store. Store server for each platform is synchronized with IAP server. |
<center>[Table. 3 IAP Component]</center>

## IAP Payment Flow

In-app purchase provides IAP SDK and IAP server API. The following figure is payment flow.

![[Figure. 3 Server To Server Model Payment Flow]](http://static.toastoven.net/prod_iap/iap_n_28.png)
<center>[Figure. 3 Server To Server Model Payment Flow]</center>

![[Figure. 4 Build-in model Payment Flow]](http://static.toastoven.net/prod_iap/iap_n_29.png)
<center>[Figure. 4 Build-in model Payment Flow]</center>

[Table.4 IAP Payment Flow]

| Step | Description |
| ---------- | ----------- |
| [1] | Register payment user ID. Developer identifies the payment user and provides item accordingly. This is not Google Play or App Store account.<br>**[Reference]** <br>API Step<br>Android : InternalInAppPurchase.InAppPurchase.registerUserId<br>iOS : TIAPurchase registerUserId: error: |
| [2] | Request payment in client<br>**[Reference]** <br>API Step<br>Android : InternalInAppPurchase..InAppPurchases.requestPurchase<br>iOS : TIAPurchase startPurchaseWithViewController: itemId: completionHandler |
| [3]<br>[3-1] | Perform payment in store. |
| [4] | Once payment is done in store, payment result will be delivered. <br>Consume item in user application server using the result.<br>**[Warning]** <br>For Build in model, if user application server is not existent, payment consume is done directly from client. However, for security reason, we strongly recommend you to consume payment in server to server method before granting authority to item.  |
| [4-1]<br>[4-2] | Request consume to IAP Server via transferred result from the store |
| [5] | Deliver item to the user if consume is successful |
| [6] | Complete payment. |

