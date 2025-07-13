# 투두 리스트 앱 - 프로젝트 구조

## 전체 디렉토리 구조

```
todo-app/
├── package.json                 # 루트 패키지 설정 (전체 프로젝트 관리)
├── README.md                    # 프로젝트 설명서
├── PRD.md                       # 제품 요구사항 문서
├── TECH_STACK.md               # 기술 스택 문서
├── ARCHITECTURE.md             # 아키텍처 설계 문서
├── PROJECT_STRUCTURE.md        # 프로젝트 구조 문서 (이 파일)
├── .gitignore                  # Git 무시 파일 목록
├── backend/                    # 백엔드 서버
│   ├── package.json           # 백엔드 의존성 관리
│   ├── server.js              # 메인 서버 진입점
│   ├── config/
│   │   └── database.js        # SQLite 데이터베이스 설정
│   ├── routes/
│   │   └── todos.js           # 투두 API 라우트
│   ├── models/
│   │   └── Todo.js            # 투두 데이터 모델
│   ├── middleware/
│   │   └── errorHandler.js    # 에러 처리 미들웨어
│   └── database.sqlite        # SQLite 데이터베이스 파일
└── frontend/                  # React 프론트엔드
    ├── package.json          # 프론트엔드 의존성 관리
    ├── public/
    │   ├── index.html        # HTML 템플릿
    │   ├── favicon.ico       # 파비콘
    │   └── manifest.json     # PWA 매니페스트
    └── src/
        ├── index.js          # React 앱 진입점
        ├── App.js            # 메인 앱 컴포넌트
        ├── components/       # React 컴포넌트
        │   ├── Header.js     # 헤더 컴포넌트
        │   ├── AddTodo.js    # 투두 추가 폼
        │   ├── TodoList.js   # 투두 목록 컨테이너
        │   └── TodoItem.js   # 개별 투두 아이템
        ├── services/         # API 서비스
        │   └── api.js        # API 호출 함수들
        └── styles/           # CSS 스타일
            ├── App.module.css
            ├── Header.module.css
            ├── AddTodo.module.css
            ├── TodoList.module.css
            └── TodoItem.module.css
```

## 파일별 상세 설명

### 루트 레벨

#### `package.json`
```json
{
  "name": "todo-app",
  "version": "1.0.0",
  "description": "React + Node.js 투두 리스트 앱",
  "scripts": {
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "server": "cd backend && npm run dev",
    "client": "cd frontend && npm start",
    "build": "cd frontend && npm run build",
    "install-deps": "cd backend && npm install && cd ../frontend && npm install"
  },
  "devDependencies": {
    "concurrently": "^8.2.2"
  }
}
```

#### `.gitignore`
```
# Dependencies
node_modules/
npm-debug.log*

# Database
backend/database.sqlite

# Production builds
frontend/build/

# Environment variables
.env
.env.local

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db
```

### 백엔드 (`/backend`)

#### `package.json`
```json
{
  "name": "todo-backend",
  "version": "1.0.0",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "express": "^4.18.2",
    "sqlite3": "^5.1.6",
    "cors": "^2.8.5"
  },
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}
```

#### `server.js` - 메인 서버 파일
```javascript
// Express 서버 설정
// 미들웨어 등록 (CORS, JSON 파싱)
// 라우트 등록
// 에러 처리
// 서버 시작 (포트 5000)
```

#### `config/database.js` - 데이터베이스 설정
```javascript
// SQLite 연결 설정
// 데이터베이스 초기화
// 테이블 생성 쿼리
// 연결 풀 관리
```

#### `routes/todos.js` - API 라우트
```javascript
// GET /api/todos - 모든 투두 조회
// POST /api/todos - 새 투두 생성
// PUT /api/todos/:id - 투두 수정
// DELETE /api/todos/:id - 투두 삭제
```

#### `models/Todo.js` - 데이터 모델
```javascript
// 투두 CRUD 함수들
// findAll() - 모든 투두 조회
// create(title) - 새 투두 생성
// findById(id) - ID로 투두 조회
// update(id, data) - 투두 업데이트
// delete(id) - 투두 삭제
```

#### `middleware/errorHandler.js` - 에러 처리
```javascript
// 글로벌 에러 핸들러
// 로깅 기능
// 클라이언트 에러 응답 포맷팅
```

### 프론트엔드 (`/frontend`)

#### `package.json`
```json
{
  "name": "todo-frontend",
  "version": "1.0.0",
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1",
    "axios": "^1.6.0"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject"
  }
}
```

#### `src/index.js` - React 앱 진입점
```javascript
// React DOM 렌더링
// App 컴포넌트 마운트
// 기본 CSS 임포트
```

#### `src/App.js` - 메인 앱 컴포넌트
```javascript
// 전역 상태 관리 (todos, loading, error)
// API 호출 함수들
// 컴포넌트 구성 및 props 전달
// 초기 데이터 로딩
```

#### `src/components/Header.js`
```javascript
// 앱 제목 표시
// 단순한 정적 컴포넌트
```

#### `src/components/AddTodo.js`
```javascript
// 새 투두 입력 폼
// 입력 상태 관리
// 폼 제출 처리
// 입력 검증
```

#### `src/components/TodoList.js`
```javascript
// 투두 목록 컨테이너
// TodoItem 컴포넌트들 렌더링
// 빈 목록 상태 처리
```

#### `src/components/TodoItem.js`
```javascript
// 개별 투두 아이템
// 체크박스 (완료 토글)
// 제목 편집 기능
// 삭제 버튼
```

#### `src/services/api.js` - API 서비스
```javascript
// Axios 인스턴스 설정
// API 엔드포인트 함수들:
//   - fetchTodos()
//   - createTodo(title)
//   - updateTodo(id, data)
//   - deleteTodo(id)
// 에러 처리
```

## 개발 워크플로우

### 1. 개발 환경 설정
```bash
# 프로젝트 클론 후
npm run install-deps    # 모든 의존성 설치
npm run dev             # 개발 서버 시작
```

### 2. 개발 서버 실행
- **프론트엔드**: `http://localhost:3000`
- **백엔드**: `http://localhost:5000`
- **데이터베이스**: `backend/database.sqlite` 파일

### 3. 빌드 및 배포
```bash
npm run build           # 프로덕션 빌드
```

## 데이터 흐름

### 1. 컴포넌트 계층 구조
```
App.js (상태 관리)
├── Header.js
├── AddTodo.js
└── TodoList.js
    └── TodoItem.js (반복)
```

### 2. 상태 전달 방식
- **하향식**: App → 자식 컴포넌트 (props)
- **상향식**: 자식 컴포넌트 → App (콜백 함수)

### 3. API 호출 흐름
```
컴포넌트 이벤트 → App.js 핸들러 → api.js 함수 → 백엔드 API → 데이터베이스
```

## 확장 가능성

### 추가 예정 기능
1. **필터링**: 완료/미완료 필터
2. **검색**: 제목으로 투두 검색
3. **카테고리**: 투두 분류 기능
4. **우선순위**: 중요도 설정

### 확장 시 추가될 디렉토리
```
frontend/src/
├── hooks/              # 커스텀 훅
├── utils/              # 유틸리티 함수
├── constants/          # 상수 정의
└── context/            # React Context

backend/
├── controllers/        # 비즈니스 로직 분리
├── utils/              # 헬퍼 함수
└── validators/         # 입력 검증
```

## 개발 가이드라인

### 파일 명명 규칙
- **컴포넌트**: PascalCase (`TodoList.js`)
- **유틸리티**: camelCase (`api.js`)
- **상수**: UPPER_SNAKE_CASE
- **CSS 모듈**: `.module.css` 접미사

### 코드 스타일
- **들여쓰기**: 2 스페이스
- **세미콜론**: 사용
- **따옴표**: 작은따옴표 우선
- **함수**: 화살표 함수 우선