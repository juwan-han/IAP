## Mobile Service > IAP > 릴리스 노트

### 2019.8.27
#### 소비성 구독상품 기능 추가
* 주기적으로 자동결제 및 상품을 지급할 수 있는 상품 유형(CONSUMABLE_AUTO_RENEWABLE)
* Apple, Google 지원
#### 원스토어 샌드박스 결제 수정 사항 
* 콘솔>App 등록/편집 팝업에서 SandBox Y/N 항목 삭제 
* SandBox Y/N 설정없이 샌드박스, 실결제 가능하도록 수정

### 2018.12.04
#### 신규 SDK 릴리즈
* iOS, Google, ONEStore 지원
* 구독 결제 지원
* 다양한 에러 처리
* [TOAST SDK](http://docs.toast.com/ko/TOAST/ko/toast-sdk/overview/)
* [console] 구독결제 기능 추가


### 2018.10.23
#### 버그수정

* [SDK][[AOS-1.5.2](/Download/#mobile-service-iap)]
    * 구글 빌링 서비스가 초기화 되지 않았을 때 메소드 호출 시 크래시 오류 수정
    * Database 접근 시 크래시 오류 수정
	
* [SDK][[Unity-1.7.1](/Download/#mobile-service-iap)]
	* [AOS-1.5.2](/Download/#mobile-service-iap) 적용
		
### 2018.09.04
#### 기능추가
* [SDK][[iOS-1.6.0](/Download/#mobile-service-iap)]
	* AppStore 프로모션 결제 지원
* [SDK][[Unity-1.7.0](/Download/#mobile-service-iap)]
	* [AOS-1.5.1](/Download/#mobile-service-iap), [iOS-1.6.0](/Download/#mobile-service-iap) 적용
	* iOS 프로모션 결제 콜백 등록 API 추가 

#### 기능개선

* [SDK][[AOS-1.5.1](/Download/#mobile-service-iap)]
	* 스토어 모듈이 프로젝트에 포함되지 않았을 경우 에러코드(UNSUPPORTED_MARKET:103)가 반환되도록 수정

#### 버그수정

* [SDK][[AOS-1.5.1](/Download/#mobile-service-iap)]
	* 구글 서비스 연결 차단 시 크래시 이슈 수정
	* API 중복 호출 방지 코드 추가

### 2018.08.28
#### 기능개선/변경
* [CONSOLE] 결제상태 변경 팝업 미번역 문구 언어팩 적용
* [CONSOLE] Transaction 탭 Item 조회 조건 개선
    * 아이템명 선택 창 추가
* [CONSOLE] IAP 콘솔과 GameBase 결제내역 조회 화면 문구 통일
* [CONSOLE] App 화면, Google 앱 정보 수정 시 마켓 검증 추가
    * Google 앱 정보 수정 시, 기 등록되어 있는 아이템 마켓에 정상 등록 되어 있는 지 검증 진행
    * 검증 실패인 경우 확인 경고 팝업 (앱 정보는 수정됨)
* [API] GameBase 결제내역 조회 API 이슈 개선
    * 삭제된 아이템의 결제내역이 조회 안 되던 문제 해결

### 2018.07.31
#### 기능추가/개선/변경
* [SDK][[Unity-1.6.0](/Download/#mobile-service-iap)]
    * [AOS-1.5.0](/Download/#mobile-service-iap), [iOS-1.5.6](/Download/#mobile-service-iap) 적용
    
#### 기능추가
* [SDK][[AOS-1.5.0](/Download/#mobile-service-iap)]
    * OneStore V17 추가  
      
#### 기능개선/변경
* [SDK][[iOS-1.5.6](/Download/#mobile-service-iap)]
    * Release Build 시 발생하던 ModuleCache Warning 제거
    * 내부 네트워크 통신 모듈 개선

### 2018.07.24
#### 기능개선/변경
* [Console] 결제내역 조회 - 조회 화면 개선
* [Console] 아이템 삭제 기능 제거 및 아이템 조회 상태 조건 추가
* [Console] Store Item Id 중복 체크 
* [API] 구글 마켓 검증 프로세스 보완

### 2018.06.26
#### 기능 개선
* [Console] 결제내역 조회 - 결제상태 조건 추가

### 2018.06.05

#### 기능추가
* [SDK][[AOS-1.4.1](/Download/#mobile-service-iap)]
    * 구매가능한 상품 조회시 국가별 통화기호가 포함된 가격정보 추가 
        * localizedPrice


* [SDK][[iOS-1.5.5](/Download/#mobile-service-iap)]
    * Bitcode 지원 추가
    * sdkVersion Interface 추가
    * 구매가능한 상품 조회시 국가별 통화기호가 포함된 가격정보 추가  
        * localizedPrice
  
#### 기능개선/변경
* [SDK][[AOS-1.4.1](/Download/#mobile-service-iap)]
    * Eclipse 지원 중단
    * aar 형식으로 SDK 배포
    * 에러코드 추가 (119)
    * tstore bintray 지원 추가
        ```
        //IAP SDK Google Play Store 사용 시 추가 - Store ID : GG
        implementation 'com.toast.iap:iap:1.4.1'
        ```
        ```
        //IAP SDK OneStore(TStore) 사용 시 추가 - Store ID : TS
        implementation 'com.toast.iap:iap-tstore:1.4.1'
        ```
    * 공개용 Sample app 추가

* [SDK][[iOS-1.5.5](/Download/#mobile-service-iap)]
    * 결제 요청시 116 Error가 지속적으로 발생할 수 있었던 문제 개선


### 2018.05.29
#### 기능 개선
* [Console] 결제내역 조회 - 결제상태코드 변경 및 툴팁 노출 개선

### 2018.05.03
#### 버그 수정
* [SDK][[iOS-1.5.4](/Download/#mobile-service-iap)]
    * 비정상적으로 중단된 결제의 재처리시 PaymentSeq가 없는 결제건의 간헐적 크래시 수정

* [SDK][[Unity-1.5.10](/Download/#mobile-service-iap)]
    * [iOS-1.5.4](/Download/#mobile-service-iap) 적용

### 2018.05.02
#### 기능 개선
* [SDK][[AOS-1.4.0](/Download/#mobile-service-iap)]
    * 일부 기능 개선

* [SDK][[iOS-1.5.3](/Download/#mobile-service-iap)]
    * Setting 예외 처리 추가

* [SDK][[Unity-1.5.9](/Download/#mobile-service-iap)]
    * [AOS-1.4.0](/Download/#mobile-service-iap), [iOS-1.5.3](/Download/#mobile-service-iap) 적용

#### 버그 수정
* [SDK][[iOS-1.5.3](/Download/#mobile-service-iap)]
    * Refresh Receipt 버그 수정

### 2018.03.22
#### 기능개선
* [Console] Transaction 탭 검색기간 한 달로 변경

### 2018.02.22
#### 기능 개선
* [Console] Transaction 탭 Excel 다운로드 기능 추가
* [Console] Transaction 탭 조회/Excel 다운로드 검색기간 7일로 수정
* [Console] 스토어결제번호 검색기능추가

#### 버그 수정
* [SDK][[iOS-1.5.2](/Download/#mobile-service-iap)][[AOS-1.3.9](/Download/#mobile-service-iap)][[Unity-1.5.8](/Download/#mobile-service-iap)] 릴리스
    * Console에서 결제 상태 수정시 미지급 결제건 조회 API에서 항상 빈 값을 반환하던 버그 수정

### 2018.01.31

#### 기능 개선
* [SDK][[AOS-1.3.8](/Download/#mobile-service-iap)][[Unity-1.5.7](/Download/#mobile-service-iap)] 릴리스
    * 'android.permission.READ_PHONE_STATE' 권한 제거

### 2018.01.24

#### 버그 수정
* [SDK][[AOS-1.3.7](/Download/#mobile-service-iap)] 릴리스
    * 구글 결제 시  20개 이상의 아이템을 한번에 검색하는 경우, 검색에 실패하는 버그 수정

### 2017.12.21

#### 버그 수정

* [SDK][[AOS-1.3.5.2](/Download/#mobile-service-iap)][[iOS-1.5.1](/Download/#mobile-service-iap)][[Unity-1.5.6](/Download/#mobile-service-iap)] 릴리스
    * 간헐적으로 발생하는 앱 크래시 현상 수정
    * 결제내역이 존재하지 않은 경우 미소비내역 조회 API 리턴값을 기존과 통일되도록 수정
    * 사용자 등록시점에 미처리된 결제건을 조회하도록 로직 수정
    * 결제요청 API 호출 시 로컬 DB에서 조회하는 조건을 User key값만으로 조회하도록 수정

### 2017.09.21

#### 기능 개선/변경

* [SDK][[AOS-1.3.5](/Download/#mobile-service-iap)][[IOS-1.4.6](/Download/#mobile-service-iap)][[Unity-1.5.5](/Download/#mobile-service-iap)] 릴리스
    * 미소비 결제내역 조회 API 내부 로직 중 과거 결제가 있는 경우에만 서버를 통해 내역을 가져오고 그렇지 않을 경우 빈 리스트 반환하도록 개선


### 2017.08.24

#### 버그 수정

* [SDK][[AOS-1.3.4](/Download/#mobile-service-iap)][[Unity-1.5.4](/Download/#mobile-service-iap)] 릴리스
    * 미처리 결제건 일괄 재처리 API 호출 시 간헐적으로 발생하는 앱 크래시 현상 수정
* [SDK][[IOS-1.4.5](/Download/#mobile-service-iap)][[Unity-1.5.4](/Download/#mobile-service-iap)] 릴리스
    * 결제시도시 잔존하는 결제건들 처리중 발생하는 앱 크래시 현상 수정


#### 기능 개선/변경

* [SDK][[AOS-1.3.4](/Download/#mobile-service-iap)][[IOS-1.4.5](/Download/#mobile-service-iap)][[Unity-1.5.4](/Download/#mobile-service-iap)] 릴리스
    * 해외 네트워크 이슈로인한 가속 URL 적용

### 2017.07.20

#### 버그 수정

* [SDK][[iOS-1.4.4](/Download/#mobile-service-iap)][[Unity-1.5.3](/Download/#mobile-service-iap)] 릴리스
    * 간헐적 '해당 항목은 무료로 복구됩니다.' native alert 대신 client 에러코드 116을 반환함  (network 상태가 좋지 않을때 발생 할 수 있음)


#### 기능 개선/변경

* [SDK][[iOS-1.4.4](/Download/#mobile-service-iap)][[Unity-1.5.3](/Download/#mobile-service-iap)] 릴리스
    * 결제 종료시점 변경 (finishTransaction의 실행시점변경. 기존 : 영수증 검증이후, 변경 : 영수증 검증이전)

### 2017.06.29

#### 버그 수정

* [SDK][[Android-1.3.3.1](/Download/#mobile-service-iap)][[Unity-1.5.2](/Download/#mobile-service-iap)] 릴리스
    * 미처리 결제건 일괄 재처리 API가 connection timeout 과 관련된 항목만 처리하도록 수정
    * 원스토어 응답실패 시 발생하는 앱 크래시 현상 수정
    * 미처리 결제건 일괄 재처리 API 호출 시 간헐적으로 발생하는 앱 크래시 현상 수정
    * 소수점 금액을 포함할 경우 발생하는 앱 크래시 현상 수정
    * 간헐적 'IAB helper is not set up' 예외 발생으로 인한 앱 크래시 현상 수정

#### 기능 개선/변경

* [SDK][[Android-1.3.3.1](/Download/#mobile-service-iap)][[Unity-1.5.2](/Download/#mobile-service-iap)] 릴리스
    * mobill-core 모듈에 물리적으로 포함되던 okhttp.jar 및 gson.jar 파일을 제거하고, gradle 의존성 설정으로 변경

### 2017.04.20

#### 버그 수정
* TEST 마켓 사용시 영수증 검증 처리가 안되는 문제 수정

### 2017.04.04

#### 기능 개선/변경

* [API] 아이템 조회, 미소비내역 조회 API 추가


### 2017.02.23

#### 기능 개선/변경

* [Console] 명칭 변경(Market > Store)
* [Console] 결제내역 조회시 결제번호(ID 컬럼)  정렬 기능 추가

#### 버그 수정
* [SDK][[Android-1.3.2](/Download/#mobile-service-iap)][[Unity-1.5.1](/Download/#mobile-service-iap)] 릴리스
    * [미처리 결제건 일괄 재처리](/Mobile Service/IAP/ko/android-sdk-guide/#_9)시 앱 크래시 현상 수정
    * [구매 가능한 아이템 조회](/Mobile Service/IAP/ko/android-sdk-guide/#_5)시 잘못된 응답값이 반환되는 문제 수정
    ```
    변경 전: itmeSeq
    변경 후: itemSeq
    ```

### 2017.01.19

#### 기능 개선/변경

* [Console] 결제상태 변경 기능 추가
* [Console] 앱 / 아이템 수정시 필수 입력값 검증처리 추가
* [SDK][[Android-1.3.1](/Download/#mobile-service-iap)][[Unity-1.5.0](/Download/#mobile-service-iap)] 릴리스
    * 불필요한 권한 제거(WRITE_EXTERNAL_STORAGE, READ_EXTERNAL_STORAGE)
    * <a href="/ko/Mobile Service/IAP/ko/error-code/" target="_blank">Error Code Guide</a> 와 상이한 오류 코드 수정
* [SDK][[iOS-1.4.3](/Download/#mobile-service-iap)] 릴리스
    * <a href="/ko/Mobile Service/IAP/ko/error-code/" target="_blank">Error Code Guide</a> 와 상이한 오류 코드 수정

### 2016.12.22

#### 기능 개선/변경

* [SDK][[Android-1.3.0](/Download/#mobile-service-iap)][[Unity-1.4.9](/Download/#mobile-service-iap)] 릴리스
    * ONE Store SDK 버전 릴리스(16.02.00 -> 16.03.00)


### 2016.11.29

#### 기능 개선/변경

* [SDK][[Android-1.2.9](/Download/#mobile-service-iap)][[Unity-1.4.8](/Download/#mobile-service-iap)] 릴리스
    * ONE Store SDK 버전 릴리스(15.01.00 -> 16.02.00)

### 2016.11.24

#### 버그 수정

* [SDK][[iOS-1.4.1](/Download/#mobile-service-iap)][[Unity-1.4.7](/Download/#mobile-service-iap)] 릴리스
    * 일부 iOS(10.0.1 이상)버전에서 결제 검증 로직 실패하던 문제 수정


### 2016.11.02

#### 기능 추가

* [SDK][[Android-1.2.8](/Download/#mobile-service-iap)][[iOS-1.4.0](/Download/#mobile-service-iap)][[Unity-1.4.6](/Download/#mobile-service-iap)] 릴리스
    * 미처리된 결제에 대한 재처리 Client API 추가
        * 미처리된 결제건(IAP 서버 검증 실패)들에 대해 일괄로 재처리 작업을 진행합니다.
        * 참고 : Android Developer's Guide > IAP 결제 흐름도 > 미처리 결제건 일괄 재처리 & iOS Developer's Guide > API Reference > 7. 미처리 결제건 일괄 재처리

#### 기능 삭제

* [SDK][Android] 네이버 라이브러리 삭제

### 2016.10.12

#### 버그 수정

* [SDK][[Android-1.2.7](/Download/#mobile-service-iap)][[Unity-1.4.5](/Download/#mobile-service-iap)] 릴리스
    * AndroidManifest.xml 필수 permission 거부 시 앱 크래쉬 현상 수정

### 2016.09.29

#### 기능 개선/변경

* [SDK][[iOS-1.3.3](/Download/#mobile-service-iap)][[Unity-1.4.4](/Download/#mobile-service-iap)] 릴리스
    * iOS에서 구매가능 상품 조회 API 호출 시 유저등록 API 호출 없이 가능하도록 수정

### 2016.09.22

#### 버그 수정

* [SDK][[Unity-1.4.3.1](/Download/#mobile-service-iap)] 릴리스
    * 구 서버 API 조회 수정 및 유니티 커스텀 패키지내의 안드로이드 모듈 수정

### 2016.08.24

#### 기능 추가

* [SDK][[Android-1.2.6](/Download/#mobile-service-iap)][[iOS-1.3.2](/Download/#mobile-service-iap)][[Unity-1.4.3](/Download/#mobile-service-iap)] 릴리스
    * 구매가능한 상품 조회 Client API 추가
        * Web Console에서 상태값이 USE 인 아이템을 가격 및 통화값을 포함하여 조회할 수 있습니다.
        * 참고 : Android Developer's Guide > IAP 결제 흐름도 > 구매 가능한 아이템 내역 조회 & iOS Developer's Guide > API Reference > 6.구매 가능한 아이템 내역 조회


### 2016.08.04

#### 기능 개선/변경

* [SDK][[Android-1.2.5](/Download/#mobile-service-iap)] 릴리스
    * AndroidManifest.xml 필수 permission 거부시 callback 에러코드 리턴 수정
