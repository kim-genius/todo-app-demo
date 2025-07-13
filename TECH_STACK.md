# 투두 리스트 앱 - 기술 스택

## 프론트엔드

### 핵심 기술
- **React 18.2.0** - UI 라이브러리
- **JavaScript (ES6+)** - 개발 언어 (TypeScript 없이 빠른 개발)
- **Create React App** - 프로젝트 부트스트래핑

### HTTP 통신
- **Axios 1.6.0** - HTTP 클라이언트
- **기본 URL**: `http://localhost:5000/api`

### 스타일링
- **CSS Modules** - 컴포넌트별 스타일 격리
- **기본 CSS** - 반응형 디자인

### 상태 관리
- **React useState** - 로컬 상태 관리
- **React useEffect** - 사이드 이펙트 처리

## 백엔드

### 핵심 기술
- **Node.js 18+** - 런타임 환경
- **Express.js 4.18+** - 웹 프레임워크
- **JavaScript (ES6+)** - 개발 언어

### 데이터베이스
- **SQLite3** - 경량 파일 기반 데이터베이스
- **sqlite3 5.1.6** - Node.js SQLite 드라이버

### 미들웨어
- **cors 2.8.5** - Cross-Origin Resource Sharing
- **express.json()** - JSON 파싱 (내장)
- **express.urlencoded()** - URL 인코딩 파싱 (내장)

## 개발 도구

### 패키지 관리
- **npm** - Node Package Manager
- **package.json** - 의존성 관리

### 개발 서버
- **nodemon 3.0.1** - 백엔드 자동 재시작
- **concurrently 8.2.2** - 프론트엔드/백엔드 동시 실행

### 포트 설정
- **프론트엔드**: `http://localhost:3000`
- **백엔드**: `http://localhost:5000`

## 의존성 목록

### 루트 package.json
```json
{
  "scripts": {
    "dev": "concurrently \"npm run server\" \"npm run client\"",
    "server": "cd backend && npm run dev",
    "client": "cd frontend && npm start",
    "install-deps": "cd backend && npm install && cd ../frontend && npm install"
  },
  "devDependencies": {
    "concurrently": "^8.2.2"
  }
}
```

### 백엔드 의존성
```json
{
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

### 프론트엔드 의존성
```json
{
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "axios": "^1.6.0"
  }
}
```

## 개발 환경 요구사항

### 시스템 요구사항
- **Node.js**: 18.0.0 이상
- **npm**: 8.0.0 이상
- **운영체제**: Windows 10+, macOS 10.15+, Ubuntu 20.04+

### 브라우저 지원
- **Chrome**: 90+
- **Firefox**: 88+
- **Safari**: 14+
- **Edge**: 90+

## 선택 이유

### React
- 컴포넌트 기반 아키텍처로 재사용성 높음
- 풍부한 생태계와 커뮤니티 지원
- 학습용 프로젝트에 적합한 난이도

### Express.js
- 경량 웹 프레임워크
- 빠른 프로토타이핑 가능
- REST API 구현에 최적화

### SQLite
- 파일 기반으로 설정 간단
- 별도 데이터베이스 서버 불필요
- 개발/데모용으로 충분한 성능

### JavaScript (TypeScript 제외)
- 빠른 개발 속도
- 타입 설정 없이 즉시 개발 가능
- MVP 개발에 적합