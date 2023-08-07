## Mobile Service > IAP > MyCard Guide

## App MyCard, etc.

- MyCard does not provide a web console where customers can log in. (As of July 2023)
- MyCard uses the payment service only with the settings set in the NHN Cloud IAP console.
- Payments are settled directly from MyCard based on the settings in the IAP console. For a guide on settlement, please contact MyCard.

```
1. The information used for MyCard payment is Store App ID and App Name. Each is used in the facGameId and facGameName fields of the MyCard, which you can refer to when inquiring about MyCard.
2. If the service is currently in operation, modification of the two values may cause errors in payment and settlement.  
```
![[App Registration]](http://static.toastoven.net/prod_iap/iap-console-new-app.png)