## Mobile Service > IAP > Amazon Appstore Console Guide

> [Notice]
> A new IAP SDK that supports subscription has been released as [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).
> No new features will be developed for the existing IAP SDK.
> This document is the guide for [NHN Cloud SDK](http://docs.toast.com/en/TOAST/en/toast-sdk/overview/).

## Amazon Developer Console

1. After registering an account in [Amazon Developer Console](https://developer.amazon.com/), create an app in the Amazon Appstore Management menu.
![Amazon Developer Console](http://static.toastoven.net/prod_iap/amazon_developer_console_eng.png)
2. NHN Cloud IAP officially supports only the Amazon Appstore app for the Android platform. Select the Android platform, enter the app name, and click the `Create app` button to create an app.
![Select app platform](http://static.toastoven.net/prod_iap/amazon_appmenu_0_eng.png)
3. After creating an app, you can check the list of created apps as shown below.
![App list in Appstore Developer Console](http://static.toastoven.net/prod_iap/amazon_appmenu_1_eng.png)
4. After creating the app, enter additional information and enter the information provided by the Developer Console in the app settings of the NHN Cloud IAP console.
5. This guide covers only how to link the app information registered in the Amazon Appstore and the app information of the NHN Cloud IAP. For more detailed steps for Amazon Appstore app registration, refer to the [Amazon documentation](https://developer.amazon.com/apps-and-games/documentation).

## Setting Values ​​Required for Linking

![NHN Cloud IAP app settings popup](http://static.toastoven.net/prod_iap/amazon_iap_console_en.png)

### Store App ID

- Enter the Android package name that you entered as build information for the app that you submitted or plan to submit through the Amazon console.
- If you have already submitted your app, you can check the information on the Amazon console screen in the following steps.
    - Click the name of the created app on the [app list](https://developer.amazon.com/apps-and-games/console/apps/list.html) screen to enter the detailed settings menu.
    - In the app detailed settings screen, click **APK Files** > **Manifest**.
![APK Files in the Amazon Developer Console](http://static.toastoven.net/prod_iap/amazon_app_store_id_01.png)
![APK Files in the Amazon Developer Console](http://static.toastoven.net/prod_iap/amazon_app_store_id_02.png)

### Amazon Shared Key

- Go to [Settings -> Identity menu](https://developer.amazon.com/settings/console/sdk/shared-key) in the Amazon Developer Console, and you can check the shared key on the following screen.
![Identity screen in Amazon Developer Console](http://static.toastoven.net/prod_iap/amazon_appmenu_3_eng.png)
- You must enter this value in the `Amazon Shared Key` item in the NHN Cloud IAP console app settings.
