# 투두 리스트 앱 - Product Requirements Document (PRD)

## 프로젝트 개요

**프로젝트명**: 투두 리스트 앱 MVP  
**목적**: React + Node.js 기반의 간단한 투두 리스트 애플리케이션  
**타겟**: 학습용/데모용 (빠른 개발 우선, 보안 최소화)

## 기술 스택

### 프론트엔드
- **프레임워크**: React 18+
- **언어**: JavaScript/TypeScript
- **스타일링**: CSS Modules 또는 Styled Components
- **HTTP 클라이언트**: Axios 또는 Fetch API

### 백엔드
- **런타임**: Node.js
- **프레임워크**: Express.js
- **데이터베이스**: SQLite (간단한 파일 기반 DB)
- **ORM**: 없음 (Raw SQL 사용)

## 핵심 기능

### 1. 투두 아이템 관리
- **생성**: 새로운 투두 아이템 추가
- **조회**: 모든 투두 아이템 목록 표시
- **수정**: 투두 아이템 내용 편집
- **삭제**: 투두 아이템 제거
- **완료 토글**: 완료/미완료 상태 변경

### 2. 데이터 구조
```javascript
Todo {
  id: number,           // 고유 식별자
  title: string,        // 투두 제목
  completed: boolean,   // 완료 상태
  createdAt: string,    // 생성 시간
  updatedAt: string     // 수정 시간
}
```

## API 설계

### 엔드포인트
- `GET /api/todos` - 모든 투두 조회
- `POST /api/todos` - 새 투두 생성
- `PUT /api/todos/:id` - 투두 수정
- `DELETE /api/todos/:id` - 투두 삭제

### 요청/응답 예시
```javascript
// POST /api/todos
Request: { "title": "React 공부하기" }
Response: { "id": 1, "title": "React 공부하기", "completed": false, "createdAt": "2024-01-01T00:00:00Z", "updatedAt": "2024-01-01T00:00:00Z" }

// GET /api/todos
Response: [
  { "id": 1, "title": "React 공부하기", "completed": false, "createdAt": "2024-01-01T00:00:00Z", "updatedAt": "2024-01-01T00:00:00Z" },
  { "id": 2, "title": "Node.js 실습", "completed": true, "createdAt": "2024-01-01T01:00:00Z", "updatedAt": "2024-01-01T01:30:00Z" }
]
```

## 사용자 인터페이스

### 화면 구성
1. **헤더**: 앱 제목 ("투두 리스트")
2. **입력 영역**: 새 투두 추가 폼
3. **리스트 영역**: 투두 아이템들의 목록
4. **필터**: 전체/완료/미완료 필터링 (선택사항)

### 투두 아이템 UI
- 체크박스 (완료 상태)
- 제목 텍스트
- 편집 버튼
- 삭제 버튼

## 개발 우선순위

### Phase 1 (핵심 MVP)
1. 백엔드 API 서버 구축
2. SQLite 데이터베이스 설정
3. CRUD API 구현
4. React 프론트엔드 기본 구조
5. API 연동

### Phase 2 (개선사항)
1. 입력 유효성 검사
2. 에러 처리
3. 로딩 상태 표시
4. 기본적인 스타일링

## 비기능적 요구사항

### 성능
- 100개 이하의 투두 아이템에서 1초 이내 응답
- 클라이언트 사이드 상태 관리 (React useState)

### 보안 (최소한)
- 기본적인 입력 검증만 구현
- CORS 설정
- SQL 인젝션 방지 (Prepared Statement 사용)

### 호환성
- 모던 브라우저 (Chrome, Firefox, Safari 최신 버전)
- 반응형 디자인 (모바일 기본 지원)

## 제외 사항 (MVP 범위 외)

- 사용자 인증/권한 관리
- 멀티 사용자 지원
- 실시간 동기화
- 복잡한 필터링/정렬
- 파일 첨부 기능
- 알림 기능
- 백업/복원 기능

## 프로젝트 구조

```
todo-app/
├── backend/
│   ├── server.js
│   ├── database.js
│   ├── routes/
│   │   └── todos.js
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── App.js
│   │   └── index.js
│   ├── public/
│   └── package.json
└── README.md
```

## 개발 일정 (예상)

- **Day 1**: 백엔드 API 구현
- **Day 2**: 프론트엔드 기본 구조 및 API 연동
- **Day 3**: UI/UX 개선 및 테스트

## 성공 지표

1. 투두 추가/삭제/수정이 정상 동작
2. 브라우저 새로고침 후에도 데이터 유지
3. 기본적인 사용자 경험 제공
4. 로컬 환경에서 안정적 실행