## Mobile Service > IAP > STEAM 콘솔 가이드

> 본 문서는 Steamworks로 출시된 앱의 정보를 [NHN Cloud IAP](https://docs.nhncloud.com/ko/Mobile%20Service/IAP/ko/Overview/) 콘솔에 등록 및 연동시키는 방법을 다룹니다.
> 스팀 앱을 출시하기 위한 보다 자세한 사항들은 [Steamworks 가이드 문서](https://partner.steamgames.com/doc/home)를 참고하시기 바랍니다.


## 기본 정보 입력

STEAM 연동을 위해서는 다음의 3가지 정보를 정확히 입력해 주시기 바랍니다. 

연동과 관련된 정보는 [Steamworks](https://partner.steamgames.com/)에서 생성합니다.

기타 본 페이지에서 설명하지 않는 항목은 ‘Mobile Service > IAP > [콘솔 공통 사용 가이드](https://docs.alpha-nhncloud.com/ko/Mobile%20Service/IAP/ko/console-guide/)’ 페이지를 참고 하시기 바랍니다. 


![NHN Cloud IAP 앱 설정](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_01_kor.png)


### STEAM App ID

* Steamworks 를 통해 제품을 등록한 후 발급 받는 앱의 고유 식별 정보입니다.
* Steamworks > App Admin > (프로젝트 명)에 표시된 App ID를 입력합니다.

![STEAM App ID](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_02_kor.png)


### STEAM Web API Key

* [ISteamMicroTxn Interface](https://partner.steamgames.com/doc/webapi/ISteamMicroTxn)(스팀 결제 API)에 접근하기 위해 필요한 정보입니다.
* Steamworks > Users & Permissions에서 신규 생성 또는 기존 발급 받은 Key 값을 입력합니다.
  * 보다 자세한 발급 방법은 [Steamworks Publisher Web API Key](https://partner.steamgames.com/doc/webapi_overview/auth)를 참고하세요.

![STEAM Web API Key](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_03_kor.png)


### STEAM 기본 통화

* 유저가 구매를 시도하여 스팀 결제 오버레이에 진입 시 아이템 가격에 적용된 통화코드의 기본 값을 설정할 수 있습니다. 
* 유저 스팀 지갑의 통화와 일치하는 아이템 정보 내 통화코드가 존재하지 않을 경우, 본 항목에서 설정된 기본통화로 상품의 가격이 출력 됩니다. 
  * ‘판매 아이템 설정’ 섹션 내 ‘국가 별 판매 아이템 정보 입력’ 항목 참고


![STEAM 기본 통화](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_04_kor.png)



## 판매 아이템 설정

NHN Cloud IAP는 [Steam Microtransaction API](https://partner.steamgames.com/doc/features/microtransactions)를 지원합니다.

![NHN Cloud IAP 아이템 설정](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_2acdfabf4efe4efc8a04c00b348110c9/cdn_origin/prod_iap/console_steam/steam_console_app_05_kor.png)



### 아이템 기본 정보 입력

- **Item 이름**: IAP Console을 통해 관리하는 아이템의 대표 이름을 입력합니다.
- **Store Item ID**: 앱에서 관리하는 아이템 ID를 입력합니다.

> 각 Item 의 Store Item ID는 고유한 값으로 입력되어야 하며 `uint32` type 만 입력 가능합니다. 
> \* 0 ~ 4,294,967,295 사이의 숫자

- **Product Type**: 현재 소비성 아이템(`CONSUMABLE`) 만을 지원합니다.


### 국가 별 판매 아이템 정보 입력
입력된 아이템의 이름 및 가격 등의 정보는 구매를 시도한 유저에게 실제 청구되는 정보이니 입력 및 수정에 유의하시기 바랍니다.

- **언어 코드**: 결제창에 표시될 아이템 명에 대응하는 언어 코드를 선택합니다.
- **국가별 아이템 명**: 선택한 통화 코드로 판매하려는 아이템의 이름을 입력합니다.
- **통화 코드**: 판매 가격에 대응하는 통화 코드를 선택합니다.
- **통화별 판매 가격**: 선택한 통화 코드에 대응하는 가격을 입력합니다.


> 앱 설정 내 기본 통화 코드에 대응하는 가격 정보는 필수 입력값 입니다. 
> 2가지 이상의 가격 정보 입력 시 유저의 스팀 지갑에 충전된 재화의 통화 코드에 대응하는 가격으로 결제 정보를 생성합니다.
> (입력된 아이템 정보 중 유저 지갑의 통화 코드에 대응하는 정보가 존재하지 않을 경우 기본 통화 코드로 결제 정보를 생성합니다.) 