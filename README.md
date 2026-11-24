# webkit640-7th-projects

**Webkit640 7기** *(2025년 대학·기업 협력형 SW아카데미 사업, 풀스택 개발자 양성과정)*에서 수행한 3개의 프로젝트를 커밋 히스토리와 산출물 문서를 유지한 채 하나로 통합한 아카이브 저장소입니다.

> 관련 기사: [경북형 SW아카데미 7기 (전자신문)](https://www.etnews.com/20251209000053)

---

## 프로젝트 한눈에 보기

| 프로젝트 | 구분 | 핵심 내용 | 주요 기술 스택 | 산출물 |
|---|---|---|---|---|
| **[computer-app](./computer-app/)** | 개인 프로젝트 | 네이버 검색 API 기반 PC 부품 수집·견적 빌더 및 커뮤니티 웹 | React 19 (Vite), Node.js (Express 5, Sequelize), MySQL, Naver API | 요구사항·설계명세서, 완료보고서, 체크리스트 |
| **[semi-project](./semi-project/)** | 이론교육 세미 프로젝트 | Google Gemini API 기반 웹소설 AI 번역기(텍스트/URL) + 커뮤니티 CRUD | React 19, Node.js (Express 5), MySQL, Gemini API, Cheerio | 프로젝트 발표/보고서 PDF, 반응형웹 과제 |
| **[taxi-app](./taxi-app/)** | 공통 과제 | 승객·기사·서버 3-tier 구조의 택시 호출 앱 서비스 | React Native 0.81 (TypeScript), Node.js (Express), MySQL, Google Maps, FCM | 승객앱 · 기사앱 · API/푸시 서버 |

---

## 저장소 구조

```text
webkit640-7th-projects/
├── computer-app/          # PC 부품 견적 사이트 + 커뮤니티 (개인 프로젝트)
│   ├── frontend/          # React 19 + Vite + Bootstrap 5
│   ├── backend/           # Express 5 + Sequelize + MySQL + Naver API 수집기
│   └── README.md
├── semi-project/          # Gemini AI 웹소설 번역기 + 커뮤니티 (세미 프로젝트)
│   ├── frontend/          # React 19 + React Bootstrap
│   ├── backend/           # Express 5 + MySQL2 + Gemini API + Cheerio
│   └── README.md
├── taxi-app/              # 택시 호출 앱 서비스 (공통 과제)
│   ├── taxi/              # 승객용 React Native 앱 (TypeScript)
│   ├── driver/            # 기사용 React Native 앱 (TypeScript)
│   ├── taxi-server/       # Express API & Firebase Cloud Messaging 서버
│   └── README.md
└── README.md
```

---

## 프로젝트별 핵심 구현 포인트

### 1. [computer-app — PC 부품 견적 & 커뮤니티 웹](./computer-app/README.md)
- **부품 데이터 자동 수집**: `scraper.js`로 네이버 검색 API에서 CPU·메인보드·RAM·GPU·SSD 등 부품 정보를 수집하고 문자열 유사도(`string-similarity`) 기반으로 DB에 정규화·저장
- **견적 빌더 & 공유**: 카테고리별 부품 선택 모달로 나만의 PC 견적을 구성·저장하고 공유 링크(`SharedQuotePage`) 제공
- **커뮤니티 & 관리자 기능**: 게시판/댓글 CRUD, 통합 검색, JWT 인증, 다크/라이트 테마, 관리자 부품 관리 페이지(`AdminPage`)

### 2. [semi-project — Gemini AI 웹소설 번역기 & 커뮤니티](./semi-project/README.md)
- **AI 번역 기능**: Google Gemini API를 연동해 일반 텍스트뿐만 아니라 URL 크롤링(`cheerio` + 프록시 라우트) 기반 번역 지원
- **사용자 커스터마이징**: 사용자가 직접 API 키, 모델, 시스템 프롬프트, 테마를 설정하고 번역 결과를 복사하거나 커뮤니티 게시글로 즉시 공유
- **커뮤니티 CRUD**: 회원가입/로그인(JWT), 게시글·댓글 작성/수정/삭제, 제목·내용·댓글 통합 검색

### 3. [taxi-app — React Native 택시 호출 앱](./taxi-app/README.md)
- **3-tier 모바일 서비스**: 승객용 앱(`taxi`), 기사용 앱(`driver`), 백엔드 서버(`taxi-server`)를 분리 설계
- **지도 & 위치 기반 호출**: Google Maps Platform(`react-native-maps`, Places Autocomplete, Geolocation)을 연동해 출발지/목적지 설정 및 호출 요청
- **실시간 알림**: `firebase-admin`과 `@react-native-firebase/messaging` 기반 FCM 푸시 알림 연동

