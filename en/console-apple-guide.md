## Mobile Service > IAP > Apple Console Guide

> This document describes how to register and integrate the information of an app released on the App Store with [NHN Cloud IAP](https://docs.nhncloud.com/ko/Mobile%20Service/IAP/ko/Overview/) Console.
There are two methods of integration: **(New) Receipt Verification + Notification V2** and **(Old) Receipt Verification + Notification V1**.

## NHN Cloud SDK Integration for iOS Versions
| Version        | Integration Method                                                                         |
|-----------|--------------------------------------------------------------------------------------------|
| v1.8.0 or later | (New) Receipt Verification + Notification V2, (Old) Receipt Verification + Notification V1 |
| v1.7.*    | (New) Receipt Verification + Notification V2                                               |
| v1.6.2 and earlier | (Old) Receipt Verification + Notification V1                                               |


## (New) Receipt Verification + Notification V2
### Generate keys for in-app purchases
> **Note**
[https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-keys-for-in-app-purchases](https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-keys-for-in-app-purchases)

1. Go to **App Store Connect** > **Users & Access** > **Keys** 
2. Click **Key Type** > **In-app purchases** 
3. Click **Generate keys for in-app purchases** 
4. Enter a name for the key and click **Generate** 
5. Click **Download in-app purchase key** 
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-in-app-purchase-key.png)

### Enter the in-app purchase key in the IAP app information
1. [In the console,](https://console.nhncloud.com) select the organization and project, **Mobile Service** > **IAP** > **App** > **Add** or select an app, and click **Edit**
2. Store APP ID: Enter your **App Bundle ID** 
3. Receipt Verification and Notification method: Choose **(New) Receipt Verification + Notification V2** 
4. Enter the purchase key, Key ID, and Issuer ID for the downloaded app.
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-edit-v2.png)

### Register Notification V2 URL
1. **App Store Connect** > **My Apps** > **Select an App** > **General Information** > **App information > App** **App Store Server Notifications**
2. Click **Edit Production Server URL** or **Sandbox Server URL** 
3. Notification version: Select **Version 2 Notifications**.
4. Enter the server URL: `https://api-iap.cloud.toast.com/callback/subscription/{APP_BUNDLE_ID}/AS/v2` 
    - If you are using Gamebase Sandbox, enter `https://sandbox-api-iap.cloud.toast.com/callback/subscription/{APP_BUNDLE_ID}/AS/v2` for the **Server URL**.


## (Old) Receipt Verification + Notification V1 (soon to be deprecated)
- Apple subscription billing requires you to create a **shared secret** and set up a **Notification V1 URL** in App Store Connect.
- Register the shared secret in the IAP app information.
- Do not need any setup for payments for Apple general merchandise.

### Generate a shared secret
> **Note**
You can generate a **primary shared secret**, which is a single secret for all apps, or **app-specific shared secret** for individual apps.
[For more information, see https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-a-shared-secret-to-verify-receipts](https://developer.apple.com/help/app-store-connect/configure-in-app-purchase-settings/generate-a-shared-secret-to-verify-receipts)

#### Primary Shared Secret
1. Go to **App Store Connect** > **Users & Access** > **Shared Secret**
2. Click **Generate** 
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-primary-shared-secret.png)

#### App-Specific Shared Secret
1. Click **App Store Connect** > **My Apps** > **Select an app** > **General** > **App Information** > **App-Specific Shared Secret** > **Manage** 
2. Click **Generate** 
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-app-specific-shared-secret.png)

### Enter the Shared Secret in the IAP app information
1. [In the console,](https://console.nhncloud.com)select the organization and project, **Mobile Service** > **IAP** > **App** > **Add** or select an app, and click **Edit**
2. Store APP ID: Enter your **App Bundle ID** 
3. Receipt Verification and Notification method: Select **(Old) Receipt Verification + Notification V1**
4. Enter the Shared Secret
![[]](http://static.toastoven.net/prod_iap/iap-console-apple-edit-v1.png)

### Register a Notification V1 URL
1. **App Store Connect** > **My Apps** > **Select an App** > **General Information** > **App information > App** **App Store Server Notifications**
2. Click **Edit Production Server URL** or **Sandbox Server URL** 
3. Notification version: Select **Version 1 Notifications**
4. Enter the server URL: `https://api-iap.cloud.toast.com/callback/subscription/{APP_BUNDLE_ID}/AS`
    - If you are using Gamebase Sandbox, enter `https://sandbox-api-iap.cloud.toast.com/callback/subscription/{APP_BUNDLE_ID}/AS` for the **Server URL**.


## Precautions for changing from (Old) Receipt Verification + Notification V1 → (New) Receipt Verification + Notification V2
- If you make changes while the app is running, it may fail, so be sure to make changes during inspections.
- Refer to the **(New) Receipt Verification + Notification V2** guide to proceed during the app check.
    - Test thoroughly in Sandbox app before making changes to your product app.
- After completing the checks, a force update is required to ensure that users are using the latest version of the app.
    - If it's not the latest version, users may experience errors when using your app.
