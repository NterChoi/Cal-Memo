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
