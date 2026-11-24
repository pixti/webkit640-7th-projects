# semi-project — Gemini AI 웹소설 번역기 & 커뮤니티

**Webkit640 7기** *(2025년 대학·기업 협력형 SW아카데미 사업, 풀스택 개발자 양성과정)* 이론교육 세미 프로젝트로 개발한 **Google Gemini API 기반 웹소설 AI 번역기 + 커뮤니티 CRUD 웹 서비스**입니다.

> 관련 기사: [경북형 SW아카데미 7기 (전자신문)](https://www.etnews.com/20251209000053)

---

## 주요 기능

- **AI 번역 기능 (`components/translate/`)**
  - **텍스트 & URL 번역**: 직접 텍스트를 입력하거나 웹사이트 URL을 입력해 본문을 추출(`cheerio` + `/api/proxy`)한 뒤 Gemini API로 번역
  - **사용자 맞춤 설정**: API 키·모델 선택(`ApiAndModelSettings`), 번역 프롬프트 커스터마이징(`PromptSettings`), 화면 테마 설정(`ThemeSettings`)
  - **결과 활용**: 번역 결과 클립보드 복사 및 커뮤니티 게시글로 바로 공유
- **커뮤니티 게시판 (`components/posts/`, `components/comments/`)**
  - 게시글 작성·조회·수정·삭제 및 댓글 CRUD
  - 게시글 제목·내용·댓글을 아우르는 통합 검색(`SearchResults`)
  - 회원가입 및 로그인 등 JWT 기반 사용자 인증(`Login`, `Register`, `useAuth`)

---

## 기술 스택

| 영역 | 기술 |
|---|---|
| **Frontend** | React 19 (Create React App), React Router 7, React Bootstrap, Axios, `jwt-decode` |
| **Backend** | Node.js, Express 5, MySQL2, `@google/generative-ai`, Cheerio, JWT, bcryptjs |
| **Database** | MySQL (`backend/schema.sql`) |

---

## 시스템 아키텍처 & 폴더 구조

- **Frontend (React)**: 사용자 입력·번역 설정·게시판 UI를 처리하고 백엔드 REST API 호출
- **Backend (Node.js / Express)**: 인증·게시판·검색 요청을 MySQL과 연동하고, 번역 및 웹 본문 수집 요청을 Google Gemini API / 프록시 라우터로 처리

```text
semi-project/
├── frontend/                                               # React 클라이언트
│   └── src/
│       ├── components/                                     # auth, translate, posts, comments, common
│       └── hooks/                                          # useAuth, useTranslation, usePosts, useSettings 등
├── backend/                                                # Express REST API 서버
│   ├── routes/                                             # auth, posts, comments, search, users, translate, proxy
│   ├── schema.sql                                          # MySQL 테이블 스키마
│   └── server.js                                           # 서버 진입점 (기본 포트 5000)
├── Semi-Project_Solo_국립금오공과대학교_20210474_박재형.pdf  # 프로젝트 보고서
└── 반응형웹_과제4_국립금오공과대학교_박재형.html             # 반응형 웹 과제물
```

---

## 로컬 실행 방법

### 1. 데이터베이스 구성
MySQL에서 데이터베이스를 생성한 뒤 `backend/schema.sql`을 실행해 테이블을 생성합니다.

### 2. 백엔드 환경 변수 및 실행
`semi-project/backend/.env` 파일을 생성해 아래 환경 변수를 설정합니다.
```env
PORT=5000
JWT_SECRET=your_jwt_secret
DB_HOST=127.0.0.1
DB_USER=root
DB_PASSWORD=your_db_password
DB_NAME=your_db_name
```
```bash
cd semi-project/backend
npm install
node server.js
```

### 3. 프론트엔드 실행
```bash
cd semi-project/frontend
npm install
npm start
```
