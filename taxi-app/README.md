# taxi-app — React Native 택시 호출 앱 서비스

**Webkit640 7기** *(2025년 대학·기업 협력형 SW아카데미 사업, 풀스택 개발자 양성과정)* 공통 과제로 개발한 **React Native(TypeScript) + Node.js 기반 택시 호출 앱 서비스**입니다.

승객용 앱(`taxi`), 기사용 앱(`driver`), 백엔드 API 및 푸시 서버(`taxi-server`)의 3-tier 구조로 구성했으며, Google Maps Platform API와 Firebase Cloud Messaging(FCM)을 연동해 호출 생성부터 배차 알림까지 실제 동작하는 수준으로 구현했습니다.

> **테스트 참고**: Google Maps Platform API 특성상 국내 지역 경로·주소 탐색에 제약이 있어, 미국 지역 좌표를 기준으로 테스트를 진행했습니다.  
> 관련 기사: [경북형 SW아카데미 7기 (전자신문)](https://www.etnews.com/20251209000053)

---

## 주요 기능

- **승객용 앱 (`taxi/`)**
  - 회원가입·로그인 및 자동 로그인(`Intro`, `Login`, `Register`)
  - Google Maps 지도 표시, 현재 위치 조회(`Geolocation`), 장소 자동완성(`Google Places Autocomplete`)을 통한 출발지/목적지 지정 및 호출 요청(`Main_Map`)
  - 내 호출 목록 조회(`Main_List`) 및 설정(`Main_Setting`)
  - 배차 상태 변경 시 FCM 푸시 알림 수신
- **기사용 앱 (`driver/`)**
  - 기사 로그인·회원가입(`Intro`, `Login`, `Register`)
  - 대기 중인 택시 호출 목록 조회 및 수락/처리(`Main_List`, `Main_Setting`)
  - 신규 호출 접수 시 FCM 푸시 알림 수신
- **백엔드 서버 (`taxi-server/`)**
  - 승객(`/taxi`), 기사(`/driver`), 사용자(`/users`) REST API 라우팅
  - MySQL 데이터베이스 연동(`database/db_connect.js`)
  - `firebase-admin`을 활용한 FCM 푸시 발송 서비스(`services/pushService.js`)

---

## 기술 스택

| 영역 | 기술 |
|---|---|
| **Mobile Apps (`taxi`, `driver`)** | React Native 0.81, React 19, TypeScript 5.8, React Navigation, Axios, AsyncStorage |
| **Maps & Location** | Google Maps Platform (`react-native-maps`, `react-native-google-places-autocomplete`, `geolocation`) |
| **Push Notification** | Firebase Cloud Messaging (`@react-native-firebase/messaging`, `firebase-admin`) |
| **Backend Server (`taxi-server`)** | Node.js, Express, MySQL |

---

## 폴더 구조

```text
taxi-app/
├── taxi/               # 승객용 React Native 앱 (TypeScript)
│   └── src/            # TaxiApp, Intro, Login, Register, Main, Main_Map, Main_List, Main_Setting, API
├── driver/             # 기사용 React Native 앱 (TypeScript)
│   └── src/            # DriverApp, Intro, Login, Register, Main, Main_List, Main_Setting, API
├── taxi-server/        # Express 백엔드 & FCM 푸시 서버
│   ├── bin/www         # 서버 실행 진입점 (기본 포트 3000)
│   ├── database/       # MySQL 연결 설정 (db_connect.js)
│   ├── routes/         # index, users, taxi, driver 라우터
│   └── services/       # FCM 푸시 알림 서비스 (pushService.js)
└── README.md
```

---

## 로컬 실행 방법

> React Native 실행을 위해 Node.js >= 20, Android Studio(Android SDK) 또는 Xcode 환경과 Google Maps API Key / Firebase 설정 파일(`google-services.json`, Firebase Admin 서비스 계정 키)이 필요합니다.

### 1. 백엔드 서버 실행 (`taxi-server`)
```bash
cd taxi-app/taxi-server
npm install
npm start
```

### 2. 승객용 / 기사용 앱 실행
```bash
# 승객용 앱
cd taxi-app/taxi
npm install
npm run android   # 또는 npm run ios

# 기사용 앱
cd taxi-app/driver
npm install
npm run android   # 또는 npm run ios
```
