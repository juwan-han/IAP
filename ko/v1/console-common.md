## Mobile Service > IAP > 콘솔 공통 사용 가이드
스토어에서 앱과 아이템을 등록한 후 IAP Console에서 앱과 아이템을 등록합니다.

> 본 문서는 [신규 IAP SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/) 가이드입니다.
<br>



<br>


## 프로젝트 생성
```
Console (https://console.toast.com)에서  [+ 프로젝트 만들기] 를 클릭하여 프로젝트를 생성합니다.
```
![[프로젝트 생성]](http://static.toastoven.net/prod_iap/iap-console-new-project.png)


## IAP 상품 활성화
```
Console (https://console.toast.com)에서 [Mobile Service] > [IAP] 을  클릭하여 활성화합니다.
```
![[IAP 상품 활성화]](http://static.toastoven.net/prod_iap/iap-console-iap-on.png)


## AppKey 확인
```
'URL & Appkey'를 클릭하여 AppKey를 확인하여 SDK 설정에 사용합니다.
```
![[AppKey 확인]](http://static.toastoven.net/prod_iap/iap-console-appkey.png)


## 앱 등록
스토어별 설정은 스토어 가이드를 참고하세요. 
```
1. [App] 탭 선택 > [추가] 버튼 클릭
2. [Store ID]에서 스토어 선택  
3. 공통 정보
   - Store ID : Google, Apple, ONEStore
   - App Name : 앱이름
   - Store APP ID : 스토어 package name or bundle id
4. [추가] 버튼 클릭 
```
![[앱 등록]](http://static.toastoven.net/prod_iap/iap-console-new-app.png)

## 아이템 등록
```
1. [Item] 탭 선택 > [+ 추가] 버튼을 클릭 
3. [Item 이름] : 아이템 이름을 입력
4. [Store Item ID] : 스토어에 등록한 아이템 ID를 입력  
5. [Product Type] : CONSUMABLE , AUTO_RENEWABLE
5. [상태] 선택  
6. [추가] 버튼을 클릭  
```

![[아이템 등록]](http://static.toastoven.net/prod_iap/iap-console-new-item.png)

## 스토어 상품 유형
```
각 스토어 개발자 센터에서 등록한 In App Products의 상품유형을 참고하여 아이템을 등록합니다.
```

| Store | 스토어 상품유형| IAP 상품유형|    
|---|---|---|
| Google Play Store| One-time, Subscriptions | CONSUMABLE, AUTO_SUBSCRIPTION |
| App Store| Consumable, Auto-Renewable | CONSUMABLE, AUTO_SUBSCRIPTION |
| ONEStore|	Managed product | CONSUMABLE|
<center>[표]상품 유형</center>

<br>
<br>



> [주의]  
> 명시되지 않은 상품 유형으로 결제 진행 시의 시스템 에러 및 재산상의 피해는 책임지지 않습니다.

## 결제 조회
```
1. [Transaction] 탭을 클릭합니다.  
2. [Search Condition] 중, 필요항목 선택
   - Store ID / Date : 스토어 + 날짜 복합 검색
   - Store Reference Key : 스토어 결제번호 단일 검색 
3. [Date] : 최대 한달 조회 가능
4. [정렬순서]에서 정렬 조건을 선택합니다.
5. [검색] 버튼을 클릭합니다.  
```
![[결제 조회]](http://static.toastoven.net/prod_iap/iap_new_01.png)


<br>
<br>

> [참고] 결제 상태   
> - Reserved : 결제 준비 완료(IAP 서버에 결제 예약 요청은 완료되었으나 검증 요청이 오지 않은 경우)   
> - Failure : 결제 검증 실패  (스토어에서 결제를 진행했으나 결제검증에서 오류가 난 경우)
> - Success : 결제 완료 (스토어 검증 성공 및 미소비결제내역에 포함됨) 
> - Refund : 환불 완료 (관리자가 수동으로 환불됬다고 변경한 경우)



## 결제 상태 변경
```
아래와 같은 상황일 경우 결제상태를 변경할 수 있습니다.

1. 결제과금은 실제로 이루어졌으나 IAP 내부 이슈로 결제상태가 정확히 반영되지 않았을 경우 ('Success' 상태로 변경)
   1.1 'Success' 상태로 변경하기 위해선 그림 7과 같이 영수증 정보와 결제가 이뤄진 가격, 통화를 기입해야 합니다.

2. 결제과금 완료 후 consume처리를 하지 않아 유저가 아이템을 받지못하여 환불처리를 했을경우 ('Refunded' 상태로 변경)
   2.1 'Refunded' 상태로 변경되었을 경우 client의 미소비 결제내역 조회 API에서 조회되지 않습니다.

변경이 가능한 결제상태는 아래와 같이 상태 컬럼 우측에 [수정] 버튼이 노출됩니다.
```
![[결제 상태 변경]](http://static.toastoven.net/prod_iap/iap_new_03.png)
![[결제 상태 변경시 추가 기입]](http://static.toastoven.net/prod_iap/iap_46.png)


## 결제 통계 조회
```
1. [Statistics] 탭을 클릭합니다.  
2. [통화]를 선택합니다.  
3. [<][>] 버튼으로 스토어별 '이달의 총 수입', '일별 상세내역'을 월별로 조회할 수 있습니다.  
```
![[그림 6 결제 통계 조회]](http://static.toastoven.net/prod_iap/iap_n_35.png)


