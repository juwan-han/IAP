## Mobile Service > IAP > MyCard 가이드

## MyCard 앱 등

- 마이카드에서는 고객사가 로그인 가능한 웹콘솔을 제공하지 않습니다. (2023년 7월 기준)
- 마이카드는 NHN Cloud IAP 콘솔에 설정하는 사항만으로 결제 서비스를 이용하게 됩니다.
- 대금 정산은 IAP 콘솔에 설정된 내용을 바탕으로 마이카드에서 직접 정산합니다. 정산에 대한 가이드는 마이카드로 문의해 주시기 바랍니다.

```
1. 마이카드 결제에 사용하는 정보는 Store App ID 와 App Name 입니다. 각각은 마이카드의 facGameId 와 facGameName 항목에 이용되며, 마이카드 문의 시 참고하시기 바랍니다.
2. 현재 운영중인 서비스라면 두 값의 수정은 결제 및 정산 오류 발생의 원인이 될 수 있습니다.  
```
![[앱 등록]](http://static.toastoven.net/prod_iap/iap-console-new-app.png)