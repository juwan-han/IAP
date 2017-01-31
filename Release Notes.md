## Common > IAP > Release Notes

### 2017.01.19

#### 기능 개선/변경

* [Console] 결제상태 변경 기능 추가
* [Console] 앱 / 아이템 수정시 필수 입력값 검증처리 추가 
* [SDK][Unity] 1.5.0 업데이트
* [SDK][Android] 1.3.1 업데이트
    * 불필요한 권한 제거(WRITE_EXTERNAL_STORAGE, READ_EXTERNAL_STORAGE)
    * <a href="/ko/Common/IAP/Error%20Code/" target="_blank">Error Code Guide</a> 와 상이한 오류 코드 수정
    * [Error Code Guide](/ko/Common/IAP/Error%20Code/)
* [SDK][iOS] 1.4.3 업데이트
    * <a href="/ko/Common/IAP/Error%20Code/" target="_blank">Error Code Guide</a> 와 상이한 오류 코드 수정

### 2016.12.22

#### 기능 개선/변경

* [SDK][Android] 1.3.0 업데이트
* [SDK][Unity] 1.4.9 업데이트
    * ONE Store SDK 버전 업데이트(16.02.00 -> 16.03.00)


### 2016.11.29

#### 기능 개선/변경

* [SDK][Android] 1.2.9 업데이트
* [SDK][Unity] 1.4.8 업데이트
    * ONE Store SDK 버전 업데이트(15.01.00 -> 16.02.00)

### 2016.11.24

#### 버그 수정

* [SDK][iOS] 1.4.1 업데이트
* [SDK][Unity] 1.4.7 업데이트
    * 일부 iOS(10.0.1 이상)버전에서 결제 검증 로직 실패하던 문제 수정


### 2016.11.02

#### 기능 추가

* [SDK][Android] 1.2.8 업데이트 
* [SDK][iOS] 1.4.0 업데이트 
* [SDK][Unity] 1.4.6 업데이트 
    * 미처리된 결제에 대한 재처리 Client API 추가
        * 미처리된 결제건(IAP 서버 검증 실패)들에 대해 일괄로 재처리 작업을 진행합니다.
        * 참고 : Android Developer's Guide > IAP 결제 흐름도 > 미처리 결제건 일괄 재처리 & iOS Developer's Guide > API Reference > 7. 미처리 결제건 일괄 재처리

#### 기능 삭제

* [SDK][Android] 네이버 라이브러리 삭제

### 2016.10.12

#### 버그 수정

* [SDK][Android] 1.2.7 업데이트
* [SDK][Unity] 1.4.5 업데이트
    * AndroidManifest.xml 필수 permission 거부 시 앱 크래쉬 현상 수정

### 2016.09.29

#### 기능 개선/변경

* [SDK][iOS] 1.3.3 업데이트 
* [SDK][Unity] 1.4.4 업데이트
    * iOS에서 구매가능 상품 조회 API 호출 시 유저등록 API 호출 없이 가능하도록 수정

### 2016.09.22

#### 버그 수정

* [SDK][Unity] 1.4.3.1 업데이트
    * 구 서버 API 조회 수정 및 유니티 커스텀 패키지내의 안드로이드 모듈 수정

### 2016.08.24

#### 기능 추가

* [SDK][Android] 1.2.6 업데이트 
* [SDK][iOS] 1.3.2 업데이트 
* [SDK][Unity] 1.4.3 업데이트 
    * 구매가능한 상품 조회 Client API 추가
        * Web Console에서 상태값이 USE 인 아이템을 가격 및 통화값을 포함하여 조회할 수 있습니다.
        * 참고 : Android Developer's Guide > IAP 결제 흐름도 > 구매 가능한 아이템 내역 조회 & iOS Developer's Guide > API Reference > 6.구매 가능한 아이템 내역 조회


### 2016.08.04

#### 기능 개선/변경

* [SDK][Android] 1.2.5 업데이트 
    * AndroidManifest.xml 필수 permission 거부시 callback 에러코드 리턴 수정
