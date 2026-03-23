# 📚 SMU WIKI — 상명대학교 위키

> 상명대학교 구성원을 위한 위키 & 커뮤니티 웹 서비스

학교 관련 정보를 누구나 작성·편집할 수 있는 위키 문서 시스템과,  
자유롭게 소통할 수 있는 커뮤니티 게시판을 제공합니다.

---

## ✨ 주요 기능

### 📝 위키 문서
- 문서 작성 / 조회 / 수정 / 삭제 (CKEditor 5 리치 텍스트 에디터)
- 문서 편집 이력(로그) 관리 및 버전 비교
- 문서 내 파일 첨부 (AWS S3 업로드)
- 랜덤 문서 보기 / 최근 편집 문서 / 내가 작성한 문서

### 💬 커뮤니티 게시판
- 게시글 CRUD + 좋아요(추천) 기능
- 댓글 및 대댓글 (계층형 구조)
- 인기 게시물 조회 (추천 순 + 최신 순)

### 👤 회원
- 이메일 인증 기반 회원가입 (학교 이메일 제한)
- 로그인 / 로그아웃
- 아이디 찾기 / 비밀번호 찾기 및 변경
- 마이페이지 (내 문서, 업로드 파일 관리)

### 📁 파일 관리
- AWS S3 기반 파일 업로드 / 다운로드
- 파일 라이선스 및 카테고리 분류

---

## 🛠 기술 스택

### Backend
| 구분 | 기술 |
|------|------|
| Framework | Spring Boot 3.1.9 |
| Language | Java 17 |
| ORM | Spring Data JPA |
| Security | Spring Security |
| Database | MySQL |
| Storage | AWS S3 |
| Template | Thymeleaf |
| Build | Gradle |

### Frontend
| 구분 | 기술 |
|------|------|
| Library | React 18 |
| Routing | React Router v6 |
| 상태 관리 | TanStack React Query |
| HTTP Client | Axios |
| 에디터 | CKEditor 5 (Custom Build) |
| 애니메이션 | Framer Motion |
| WebSocket | STOMP.js + SockJS |

### Infra
| 구분 | 기술 |
|------|------|
| 컨테이너 | Docker / Docker Compose |
| 스토리지 | AWS S3 |

---

## 📂 프로젝트 구조

```
SMU_WIKI/
├── src/main/java/smw/capstone/
│   ├── config/          # Security, CORS, S3, WebMvc 설정
│   ├── controller/      # REST API 컨트롤러
│   ├── service/         # 비즈니스 로직
│   ├── repository/      # JPA Repository
│   ├── entity/          # JPA 엔티티 (Documents, Board, Member, Comments 등)
│   ├── DTO/             # 요청/응답 DTO
│   └── common/          # 예외 처리, 유틸리티
├── frontend/
│   ├── src/
│   │   ├── pages/       # 페이지 컴포넌트
│   │   ├── component/   # 재사용 UI 컴포넌트
│   │   ├── layout/      # 레이아웃 (Root, Outlet)
│   │   └── util/        # API, 인증, 유효성 검사 유틸
│   └── public/
├── docker-compose.yml
├── Dockerfile
└── build.gradle
```

---

## 🚀 실행 방법

### 사전 요구사항
- Java 17+
- Node.js 18+
- MySQL 8.0+
- AWS S3 버킷 (파일 업로드용)

### Backend

```bash
# 1. 프로젝트 클론
git clone https://github.com/<username>/SMU_WIKI.git
cd SMU_WIKI

# 2. application.yml 설정 (DB, S3 자격 증명 등)

# 3. 빌드 및 실행
./gradlew bootRun
```

### Frontend

```bash
cd frontend

# 의존성 설치
yarn install

# 개발 서버 실행
yarn start
```

> 프론트엔드는 기본적으로 `http://localhost:3000` 에서 실행됩니다.

### Docker로 실행

```bash
docker-compose up --build
```

---

## ⚙️ 환경 변수 설정

`src/main/resources/application.yml` 에 아래 항목을 설정해야 합니다.

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/smuwiki
    username: {DB_USERNAME}
    password: {DB_PASSWORD}

cloud:
  aws:
    credentials:
      access-key: {AWS_ACCESS_KEY}
      secret-key: {AWS_SECRET_KEY}
    region:
      static: ap-northeast-2
    s3:
      bucket: {S3_BUCKET_NAME}
```

---

## 📊 ERD

주요 엔티티 관계:

```
Member ──< Documents ──< DocLog
   │            │
   │            └──< DocFile >── Files
   │
   ├──< Board ──< Comments (self-referencing: 대댓글)
   │      │
   │      └──< Like
   │
   └──< Files
```

---

## 👥 팀원

상명대학교 캡스톤 디자인 프로젝트

---

## 📄 License

This project is for educational purposes.
