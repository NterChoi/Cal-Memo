# [Cal-Memo] Software Requirements Specification (SRS) v1.0

이 문서는 캘린더 기반의 심플 메모 애플리케이션 **'Cal-Memo'**의 요구사항을 정의합니다. 본 프로젝트는 윈도우 PC와 모바일 기기 간의 자유로운 동기화와 날짜 중심의 직관적인 기록 관리를 목표로 합니다.

---

## 1. 개요 (Introduction)

### 1.1 목적 (Purpose)
기존 메모 앱(Notion, Obsidian 등)의 무거운 사용성과 날짜별 기록 확인의 어려움을 해결하기 위해, 가장 가볍고 직관적인 **'날짜 중심 메모 시스템'**을 구축합니다.

### 1.2 대상 독자 (Intended Audience)
- 오사카 소재 기술 중심 기업의 채용 담당자 및 엔지니어
- 본 프로젝트의 백엔드 및 프론트엔드 개발자 (본인)

### 1.3 범위 (Scope)
- NestJS 기반의 백엔드 API 서버
- Next.js 기반의 PWA 프론트엔드 (윈도우/모바일 공용)
- Redis를 활용한 실시간 동기화 엔진

---

## 2. 전체 설명 (Overall Description)

### 2.1 사용자 클래스 및 특징 (User Classes and Characteristics)
- **개인 기록가**: 매일의 일과나 아이디어를 날짜별로 남기고 싶어 하는 사용자.
- **멀티 디바이스 사용자**: 윈도우 PC로 작업하며 아이폰/안드로이드로 이동 중에 메모를 확인하는 사용자.

### 2.2 운영 환경 (Operating Environment)
- **Client**: Web Browser (Chrome, Safari, Edge) 및 PWA 지원 환경.
- **Server**: Node.js v22+, PostgreSQL, Redis, AWS EC2/RDS.

### 2.3 제약 사항 (Constraints)
- 6월 졸업 전까지 MVP(최소 기능 제품) 개발 완료.
- 1인 개발 프로젝트로서 유지보수성이 높은 클린 아키텍처 준수.

---

## 3. 기능적 요구사항 (Functional Requirements)

| ID | 기능 명칭 | 설명 | 우선순위 |
| :--- | :--- | :--- | :--- |
| **REQ-01** | **캘린더 뷰 조회** | 월별 달력을 표시하고, 메모가 작성된 날짜를 시각적으로 표시함. | High |
| **REQ-02** | **날짜별 메모 CRUD** | 특정 날짜를 선택하여 메모를 작성, 조회, 수정, 삭제함. | High |
| **REQ-03** | **실시간 동기화** | 동일 계정으로 접속된 여러 기기 간에 메모 내용을 실시간으로 동기화함. | High |
| **REQ-04** | **사용자 인증** | 이메일/비밀번호 기반의 회원가입 및 로그인 (JWT 방식). | Medium |
| **REQ-05** | **통합 검색** | 날짜에 상관없이 키워드를 통해 과거 메모를 검색함. | Medium |

---

## 4. 비기능적 요구사항 (Non-functional Requirements)

### 4.1 성능 (Performance)
- **응답 시간**: 모든 데이터 조회 API의 응답 시간은 200ms 이내여야 함.
- **동기화 지연**: 기기 간 동기화 지연 시간(Latency)은 500ms 이내여야 함.

### 4.2 보안 (Security)
- 모든 API 통신은 HTTPS를 통해 암호화되어야 함.
- 비밀번호는 Argon2 또는 Bcrypt를 사용하여 단방향 해싱 저장함.

### 4.3 가용성 및 확장성 (Availability & Scalability)
- **PWA 지원**: 오프라인 상태에서도 메모를 작성할 수 있으며, 온라인 연결 시 자동 동기화됨.
- **무상태 설계**: 서버는 Stateless하게 설계하여 수평적 확장이 가능해야 함.

---

## 5. 외부 인터페이스 요구사항 (External Interface Requirements)

### 5.1 사용자 인터페이스 (UI)
- 캘린더 라이브러리(FullCalendar 등)를 활용한 직관적인 달력 UI.
- 모바일 우선(Mobile-first) 반응형 디자인 적용.

### 5.2 소프트웨어 인터페이스
- **Database**: PostgreSQL (주 저장소), Redis (캐시 및 실시간 동기화).
- **API**: RESTful API 설계 원칙 준수.

---

## 6. 부록 (Appendix)

### 6.1 용어 정의
- **PWA (Progressive Web App)**: 웹과 앱의 장점을 결합한 기술로, 설치 및 오프라인 사용이 가능함.
- **CRDT (Conflict-free Replicated Data Type)**: 분산 시스템에서 데이터 충돌 없이 동기화하기 위한 데이터 구조.
