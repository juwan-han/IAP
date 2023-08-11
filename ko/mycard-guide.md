## Mobile Service > IAP > MyCard 가이드

## MyCard 앱 등록

- 마이카드에서는 고객사가 로그인 가능한 웹콘솔을 제공하지 않습니다. (2023년 7월 기준)
- 마이카드 연동은 NHN Cloud IAP 콘솔에 입력한 정보를 기준으로 처리됩니다.
- 따라서 마이카드와 입력할 정보에 대해서 사전에 협의하십시오.
```
1. 아래 화면에서 입력된 App Name과 Store App ID는 결제 처리 시 마이카드의 facGameName과 facGameId 항목으로 연동됩니다.
 - 마이카드에 문의 시에는 facGameName과 facGameId를 이용해 문의하십시오.
 - 반드시 정확하게 입력하십시오.
2. Live 중인 게임일 경우 아래 화면에서 App Name과 Store App ID를 수정하면 결제 오류 및 장애 발생의 원인이 될 수 있습니다.
 - 반드시 서비스 Live 전에 정상 입력 여부를 확인하십시오.  
```
![[앱 등록]](http://static.toastoven.net/prod_iap/iap-console-new-app.png)