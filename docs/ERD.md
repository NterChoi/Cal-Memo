erDiagram
    USER ||--o{ NOTE : "writes"
    USER ||--o{ TAG : "owns"
    NOTE ||--o{ NOTE_TAG : "has"
    TAG ||--o{ NOTE_TAG : "assigned to"

    USER {
        uuid id PK
        string email UK
        string password
        string nickname
        datetime created_at
    }

    NOTE {
        uuid id PK
        uuid user_id FK
        string title
        text content
        date target_date
        datetime created_at
        datetime updated_at
    }

    TAG {
        uuid id PK
        uuid user_id FK
        string name
        string color_code
    }

    NOTE_TAG {
        uuid note_id PK, FK
        uuid tag_id PK, FK
    }

### 🧠 Design Decisions & Strategy

1. **N:M Relationship for Tags**
   - 메모와 태그 간의 유연한 매핑을 위해 중간 테이블(`note_tags`)을 도입했습니다. 이는 데이터 중복을 최소화하고 검색 효율성을 높이기 위한 설계입니다.

2. **UUID as Primary Key**
   - 오토 인크리먼트(Auto-increment) 대신 UUID를 선택했습니다. 이는 향후 오프라인 우선(Offline-first) 동기화 환경에서 기기 간 ID 충돌을 방지하고 보안성을 강화하기 위함입니다.

3. **Indexing Strategy**
   - `notes` 테이블의 `user_id`와 `target_date` 컬럼에 복합 인덱스를 생성할 예정입니다. 캘린더 뷰의 핵심인 '날짜별 메모 조회' 성능을 최적화하기 위한 결정입니다.
