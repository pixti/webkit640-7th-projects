# computer-app — PC 부품 견적 & 커뮤니티 웹

**Webkit640 7기** *(2025년 대학·기업 협력형 SW아카데미 사업, 풀스택 개발자 양성과정)* 개인 프로젝트로 개발한 **React + Node.js 기반 컴퓨터 견적 사이트**입니다.

네이버 검색 API를 활용해 부품 제품 정보를 수집·정규화하여 MySQL DB에 저장하고, 사용자가 카테고리별 부품을 조합해 PC 견적을 생성·공유하며 커뮤니티에서 소통할 수 있도록 구현했습니다.

> **참고**: 초기에는 웹앱(Web App)으로 기획했으나, 유라클 Morpheus 집체 교육 일정으로 인해 시간 관계상 웹(Web) 버전으로 완성해 제출했습니다.  
> 관련 기사: [경북형 SW아카데미 7기 (전자신문)](https://www.etnews.com/20251209000053)

---

## 주요 기능

- **PC 견적 빌더 (`QuoteBuilderPage`, `PartSelectionModal`)**
  - CPU, 메인보드, RAM, GPU, SSD, 케이스 등 카테고리별 부품 선택 및 총액 계산
  - 내 견적 저장/조회(`MyPage`) 및 공유 견적 페이지(`SharedQuotePage`) 지원
- **부품 조회 & 네이버 API 수집 (`scraper.js`)**
  - 네이버 검색 API로 부품·가격 데이터를 수집하고 `string-similarity`로 모델 매칭 후 Sequelize ORM을 통해 DB 저장
  - 부품 목록 필터링, 상세 정보 조회(`PartDetailPage`), 통합 검색(`SearchResultsPage`)
- **커뮤니티 & 인증**
  - JWT 기반 회원가입·로그인(`AuthContext`, `authMiddleware`)
  - 게시판 유형별 게시글·댓글 CRUD(`CommunityPage`, `PostDetailPage`, `CreatePostPage`)
  - 다크/라이트 테마 전환(`useTheme`)
- **관리자 기능 (`AdminPage`, `EditPartPage`)**
  - 관리자 전용 라우트(`AdminRoute`)를 통한 부품 정보 수정 및 데이터 관리

---

## 기술 스택

| 영역 | 기술 |
|---|---|
| **Frontend** | React 19, Vite 7, React Router 7, Axios, Bootstrap 5, Bootstrap Icons |
| **Backend** | Node.js, Express 5, Sequelize 6, MySQL2, JWT, bcrypt |
| **Data Collection** | Naver Search API, Puppeteer, `string-similarity` |

---

## 폴더 구조 및 산출물

```text
computer-app/
├── frontend/                                # React + Vite 클라이언트
│   └── src/
│       ├── components/                      # layout, home, parts, quote, common
│       ├── context/                         # AuthContext
│       ├── hooks/                           # useParts, useMyEstimates, usePosts, useTheme 등
│       └── pages/                           # Home, QuoteBuilder, SharedQuote, Community, Admin 등
├── backend/                                 # Express + Sequelize REST API 서버
│   ├── config/config.json                   # MySQL DB 연결 설정
│   ├── controllers/                         # auth, part, estimate, quotation, post, comment 등
│   ├── models/                              # Sequelize 모델 (part, price, estimate, post, user 등)
│   ├── routes/                              # /api/* 라우터
│   ├── app.js                               # 서버 진입점 (sequelize.sync + seedDatabase)
│   ├── seed.js                              # 초기 카테고리/시드 데이터 생성
│   └── scraper.js                           # 네이버 API 부품 데이터 수집 스크립트
├── 박재형_개인프로젝트_요구사항명세서.pdf
├── 박재형_개인프로젝트_설계명세서.pdf
├── 박재형_개인프로젝트_완료보고서.pdf
├── 박재형_체크리스트.xlsx
└── 1.jpg
```

---

## 로컬 실행 방법

### 1. 사전 준비
- Node.js (v18 이상 권장) 및 MySQL 서버
- `backend/config/config.json`의 MySQL 계정(`username`, `password`, `database`)을 로컬 환경에 맞게 수정하고, `computer_app_db` 데이터베이스를 생성합니다.

### 2. 백엔드 실행
```bash
cd computer-app/backend
npm install
npm start
```
- 서버 시작 시 `sequelize.sync({ alter: true })` 및 `seedDatabase()`가 실행되어 테이블과 초기 데이터가 구성됩니다.
- *(선택)* 네이버 API로 부품 데이터를 수집하려면 `backend/scraper.js` 상단에 `NAVER_CLIENT_ID`, `NAVER_CLIENT_SECRET`을 입력한 뒤 `node scraper.js`를 실행합니다.

### 3. 프론트엔드 실행
```bash
cd computer-app/frontend
npm install
npm run dev
```
