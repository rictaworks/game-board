# ER図

```mermaid
erDiagram
    users {
        uuid id PK
        string google_sub UK "NOT NULL"
        string display_name "NOT NULL"
        string avatar_url
        boolean tutorial_completed "DEFAULT false"
        timestamp created_at
        timestamp updated_at
    }
    boards {
        uuid id PK
        uuid owner_id FK
        string title "NOT NULL"
        integer template_type_id FK
        integer timer_minutes
        timestamp created_at
        timestamp updated_at
    }
    board_members {
        uuid id PK
        uuid board_id FK
        uuid user_id FK
        enum role "owner/editor/viewer"
        timestamp joined_at
    }
    canvas_objects {
        uuid id PK
        uuid board_id FK
        enum object_type "sticky/text/shape/arrow/image/frame/stamp/marker"
        float x "NOT NULL"
        float y "NOT NULL"
        float width
        float height
        float rotation "DEFAULT 0"
        integer z_index "DEFAULT 0"
        jsonb content
        uuid locked_by_user_id FK
        uuid created_by_user_id FK
        timestamp created_at
        timestamp updated_at
    }
    agenda_items {
        uuid id PK
        uuid board_id FK
        string title "NOT NULL"
        boolean completed "DEFAULT false"
        integer sort_order
        timestamp created_at
        timestamp updated_at
    }
    operations {
        uuid id PK
        uuid board_id FK
        uuid user_id FK
        enum operation_type "create/update/delete/move"
        uuid object_id
        jsonb payload
        bigint client_timestamp
        timestamp server_timestamp
        timestamp created_at
    }
    images {
        uuid id PK
        uuid board_id FK
        uuid uploaded_by_user_id FK
        string storage_key "NOT NULL"
        string original_filename
        string content_type
        bigint byte_size
        timestamp created_at
    }
    template_types {
        integer id PK
        string name
    }

    users ||--o{ boards : "owns"
    users ||--o{ board_members : "joins"
    boards ||--o{ board_members : "has"
    boards ||--o{ canvas_objects : "contains"
    boards ||--o{ agenda_items : "has"
    boards ||--o{ operations : "logs"
    boards ||--o{ images : "stores"
    boards }o--o| template_types : "uses"
    canvas_objects }o--o| users : "locked_by"
    canvas_objects }o--|| users : "created_by"
    operations }o--|| users : "performed_by"
    images }o--|| users : "uploaded_by"
```

## マスタデータ

| マスタ名 | 件数 |
|---|---|
| tool_types | 9件（付箋・テキスト・図形・矢印・画像・フレーム・スタンプ・マーカー・消しゴム） |
| shape_types | 8件（矩形・角丸矩形・円・三角・菱形・六角形・吹き出し・スター） |
| stamp_types | 12件 |
| template_types | 6件（ブレインストーミング・KPT・スプリント計画・ユーザーストーリー・マインドマップ・自由） |
| age_groups | 6件（10代〜60代以上） |
