# 투두 리스트 앱 - 시스템 아키텍처

## 전체 아키텍처 개요

```
┌─────────────────┐    HTTP/REST API    ┌─────────────────┐    SQLite Queries    ┌─────────────────┐
│                 │◄──────────────────►│                 │◄────────────────────►│                 │
│   React Client  │                    │  Express Server │                      │  SQLite Database│
│   (Port 3000)   │                    │   (Port 5000)   │                      │   (File based)  │
│                 │                    │                 │                      │                 │
└─────────────────┘                    └─────────────────┘                      └─────────────────┘
        │                                       │                                        │
        ▼                                       ▼                                        ▼
┌─────────────────┐                    ┌─────────────────┐                      ┌─────────────────┐
│ UI Components   │                    │ API Routes      │                      │ todos Table     │
│ • TodoList      │                    │ • GET /todos    │                      │ • id (INTEGER)  │
│ • TodoItem      │                    │ • POST /todos   │                      │ • title (TEXT)  │
│ • AddTodo       │                    │ • PUT /todos/:id│                      │ • completed     │
│ • App           │                    │ • DELETE /todos │                      │   (BOOLEAN)     │
└─────────────────┘                    └─────────────────┘                      │ • createdAt     │
                                                                                 │   (DATETIME)    │
                                                                                 │ • updatedAt     │
                                                                                 │   (DATETIME)    │
                                                                                 └─────────────────┘
```

## 계층별 상세 설계

### 1. 프레젠테이션 계층 (React Frontend)

#### 컴포넌트 구조
```
App.js
├── Header.js (제목 표시)
├── AddTodo.js (새 투두 입력 폼)
└── TodoList.js
    └── TodoItem.js (개별 투두 아이템)
```

#### 상태 관리 흐름
```
App.js (최상위 상태)
├── todos: Todo[] - 전체 투두 목록
├── loading: boolean - 로딩 상태
└── error: string - 에러 메시지

Data Flow:
1. useEffect → API 호출 → 초기 데이터 로드
2. 사용자 액션 → API 호출 → 상태 업데이트 → 리렌더링
```

### 2. API 계층 (Express Backend)

#### 라우트 구조
```
/api/todos
├── GET    /          - 모든 투두 조회
├── POST   /          - 새 투두 생성
├── PUT    /:id       - 투두 수정
└── DELETE /:id       - 투두 삭제
```

#### 미들웨어 스택
```
Express App
├── cors() - CORS 처리
├── express.json() - JSON 파싱
├── express.urlencoded() - URL 인코딩 파싱
└── /api/todos 라우터
```

### 3. 데이터 계층 (SQLite Database)

#### 데이터베이스 스키마
```sql
CREATE TABLE todos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    title TEXT NOT NULL,
    completed BOOLEAN DEFAULT FALSE,
    createdAt DATETIME DEFAULT CURRENT_TIMESTAMP,
    updatedAt DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

#### 데이터 모델
```javascript
Todo {
    id: number,           // 자동 증가 기본키
    title: string,        // 투두 제목 (필수)
    completed: boolean,   // 완료 상태 (기본: false)
    createdAt: string,    // 생성 시간 (ISO 8601)
    updatedAt: string     // 수정 시간 (ISO 8601)
}
```

## API 명세

### 요청/응답 형식

#### 1. 투두 목록 조회
```http
GET /api/todos
Response: 200 OK
[
    {
        "id": 1,
        "title": "React 공부하기",
        "completed": false,
        "createdAt": "2024-01-01T00:00:00.000Z",
        "updatedAt": "2024-01-01T00:00:00.000Z"
    }
]
```

#### 2. 투두 생성
```http
POST /api/todos
Content-Type: application/json

Request Body:
{
    "title": "새로운 투두"
}

Response: 201 Created
{
    "id": 2,
    "title": "새로운 투두",
    "completed": false,
    "createdAt": "2024-01-01T01:00:00.000Z",
    "updatedAt": "2024-01-01T01:00:00.000Z"
}
```

#### 3. 투두 수정
```http
PUT /api/todos/1
Content-Type: application/json

Request Body:
{
    "title": "수정된 투두",
    "completed": true
}

Response: 200 OK
{
    "id": 1,
    "title": "수정된 투두",
    "completed": true,
    "createdAt": "2024-01-01T00:00:00.000Z",
    "updatedAt": "2024-01-01T01:30:00.000Z"
}
```

#### 4. 투두 삭제
```http
DELETE /api/todos/1

Response: 204 No Content
```

## 데이터 플로우

### 1. 앱 초기화 흐름
```
1. React App 시작
2. App.js useEffect 실행
3. GET /api/todos 호출
4. 서버에서 SQLite 쿼리 실행
5. 투두 목록 반환
6. React 상태 업데이트
7. UI 렌더링
```

### 2. 투두 추가 흐름
```
1. 사용자가 입력 폼에 제목 입력
2. 폼 제출 이벤트 발생
3. POST /api/todos 호출
4. 서버에서 INSERT 쿼리 실행
5. 새 투두 반환
6. React 상태에 새 투두 추가
7. UI 업데이트
```

### 3. 투두 수정/삭제 흐름
```
1. 사용자가 체크박스 클릭 또는 삭제 버튼 클릭
2. PUT 또는 DELETE API 호출
3. 서버에서 UPDATE 또는 DELETE 쿼리 실행
4. 성공 응답 반환
5. React 상태 업데이트
6. UI 업데이트
```

## 에러 처리

### HTTP 상태 코드
- `200 OK` - 성공적인 조회/수정
- `201 Created` - 성공적인 생성
- `204 No Content` - 성공적인 삭제
- `400 Bad Request` - 잘못된 요청 데이터
- `404 Not Found` - 존재하지 않는 투두
- `500 Internal Server Error` - 서버 오류

### 에러 응답 형식
```json
{
    "error": {
        "message": "에러 메시지",
        "code": "ERROR_CODE",
        "timestamp": "2024-01-01T00:00:00.000Z"
    }
}
```

## 보안 고려사항

### 입력 검증
- 제목 길이 제한 (최대 255자)
- HTML/Script 태그 이스케이프
- SQL 인젝션 방지 (Prepared Statement 사용)

### CORS 설정
```javascript
app.use(cors({
    origin: 'http://localhost:3000',
    credentials: true
}));
```

## 성능 최적화

### 프론트엔드
- React.memo로 불필요한 리렌더링 방지
- 디바운스로 API 호출 최적화

### 백엔드
- SQLite 인덱스 활용
- 적절한 HTTP 캐시 헤더 설정

### 데이터베이스
- id 컬럼에 기본 인덱스 활용
- 필요시 title 컬럼에 인덱스 추가