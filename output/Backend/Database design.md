# 📂 데이터베이스 설계 명세서 (Database Schema)

<img width="978" height="623" alt="image" src="https://github.com/user-attachments/assets/595254d0-9033-4338-a483-9720f569707f" />


## 1. ER Diagram (Entity-Relationship Diagram)

```mermaid
erDiagram
    users ||--o{ bookmarks : "Creates (1:N)"
    users ||--o{ tags : "Manages (1:N)"
    users ||--o{ reminders : "Sets (1:N)"
    
    bookmarks ||--o{ bookmark_tags : "Has (1:N)"
    tags ||--o{ bookmark_tags : "Tagged in (1:N)"
    
    bookmarks |o--o{ reminders : "Target (1:N)"
    bookmarks ||--|| bookmark_ai_summaries : "Summarized (1:1)"

    users {
        bigint id PK
        varchar oauth_provider "NN, Default: 'kakao'"
        varchar oauth_id "NN"
        varchar email
        varchar name
        text profile_image
        text refresh_token
        timestamptz last_login_at
        timestamptz created_at "Default: NOW()"
        timestamptz updated_at
    }

    bookmarks {
        bigint id PK
        bigint user_id FK "NN"
        text url "NN"
        text title
        text description
        text favicon_url
        varchar source "NN, Default: 'extension'"
        boolean is_archived "NN, Default: false"
        int visit_count "NN, Default: 0"
        timestamptz last_visited_at
        timestamptz created_at "Default: NOW()"
        timestamptz updated_at
    }

    tags {
        bigint id PK
        bigint user_id FK "NN"
        varchar name "NN"
        timestamptz created_at "Default: NOW()"
    }

    bookmark_tags {
        bigint bookmark_id PK, FK "NN"
        bigint tag_id PK, FK "NN"
    }

    reminders {
        bigint id PK
        bigint user_id FK "NN"
        bigint bookmark_id FK
        timestamptz remind_at "NN"
        varchar status "NN, Default: 'scheduled'"
        timestamptz created_at "Default: NOW()"
        timestamptz completed_at
    }

    bookmark_ai_summaries {
        bigint id PK
        bigint bookmark_id FK, UQ "NN"
        text summary_short
        text summary_full
        varchar model
        timestamptz created_at "Default: NOW()"
    }
```

---

## 2. Table Details (테이블 상세)

### 👤 1. users
사용자 정보를 저장하며, 카카오 등 OAuth 로그인을 기반으로 관리합니다.

| Column | Type | Nullable | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| **id** | `BIGSERIAL` | ❌ | *(Auto)* | Primary Key |
| **oauth_provider** | `VARCHAR(30)` | ❌ | `'kakao'` | OAuth 제공자 (UK 복합키) |
| **oauth_id** | `VARCHAR(100)` | ❌ | | OAuth 제공자 내 사용자 ID (UK 복합키) |
| email | `VARCHAR(255)` | ✅ | | 사용자 이메일 |
| name | `VARCHAR(100)` | ✅ | | 사용자 이름 |
| profile_image | `TEXT` | ✅ | | 프로필 이미지 URL |
| refresh_token | `TEXT` | ✅ | | OAuth Refresh Token |
| last_login_at | `TIMESTAMPTZ` | ✅ | | 마지막 로그인 일시 |
| created_at | `TIMESTAMPTZ` | ❌ | `NOW()` | 계정 생성일 |
| updated_at | `TIMESTAMPTZ` | ✅ | | 계정 수정일 |

> **Constraints & Indexes**
> * `UNIQUE (oauth_provider, oauth_id)`
> * `INDEX idx_users_oauth`
> * `INDEX idx_users_email`

### 🔖 2. bookmarks
사용자가 저장한 북마크(URL)와 관련 메타데이터를 저장합니다.

| Column | Type | Nullable | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| **id** | `BIGSERIAL` | ❌ | *(Auto)* | Primary Key |
| **user_id** | `BIGINT` | ❌ | | Foreign Key (`users.id`) |
| **url** | `TEXT` | ❌ | | 북마크 URL |
| title | `TEXT` | ✅ | | 웹페이지 제목 |
| description | `TEXT` | ✅ | | 웹페이지 설명 |
| favicon_url | `TEXT` | ✅ | | 파비콘 URL |
| source | `VARCHAR(30)` | ❌ | `'extension'` | 저장 출처 (`extension`, `web`, `mobile`) |
| is_archived | `BOOLEAN` | ❌ | `FALSE` | 보관 여부 |
| visit_count | `INT` | ❌ | `0` | 방문 횟수 |
| last_visited_at | `TIMESTAMPTZ` | ✅ | | 마지막 방문 일시 |
| created_at | `TIMESTAMPTZ` | ❌ | `NOW()` | 생성일 |
| updated_at | `TIMESTAMPTZ` | ✅ | | 수정일 |

> **Constraints & Indexes**
> * `CHECK (source IN ('extension', 'web', 'mobile'))`
> * `INDEX idx_bookmarks_user_created (user_id, created_at DESC)`

### 🏷️ 3. tags
사용자가 생성한 태그 목록입니다.

| Column | Type | Nullable | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| **id** | `BIGSERIAL` | ❌ | *(Auto)* | Primary Key |
| **user_id** | `BIGINT` | ❌ | | Foreign Key (`users.id`) |
| **name** | `VARCHAR(50)` | ❌ | | 태그명 |
| created_at | `TIMESTAMPTZ` | ❌ | `NOW()` | 생성일 |

> **Constraints & Indexes**
> * `UNIQUE (user_id, name)`: 유저별 중복 태그 방지
> * `INDEX idx_tags_user`

### 🔗 4. bookmark_tags (M:N)
북마크와 태그 간의 다대다 관계를 연결하는 매핑 테이블입니다.

| Column | Type | Nullable | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| **bookmark_id** | `BIGINT` | ❌ | | Foreign Key (`bookmarks.id`) |
| **tag_id** | `BIGINT` | ❌ | | Foreign Key (`tags.id`) |

> **Constraints**
> * `PRIMARY KEY (bookmark_id, tag_id)`
> * `ON DELETE CASCADE`: 북마크나 태그 삭제 시 매핑 정보도 자동 삭제

### ⏰ 5. reminders
북마크 재방문 알림 스케줄입니다.

| Column | Type | Nullable | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| **id** | `BIGSERIAL` | ❌ | *(Auto)* | Primary Key |
| **user_id** | `BIGINT` | ❌ | | Foreign Key (`users.id`) |
| bookmark_id | `BIGINT` | ✅ | | Foreign Key (`bookmarks.id`), Nullable |
| **remind_at** | `TIMESTAMPTZ` | ❌ | | 알림 발송 예정 시간 |
| **status** | `VARCHAR(20)` | ❌ | `'scheduled'` | 상태 (`scheduled`, `sent`, `canceled`, `failed`) |
| created_at | `TIMESTAMPTZ` | ❌ | `NOW()` | 생성일 |
| completed_at | `TIMESTAMPTZ` | ✅ | | 완료(발송/취소) 일시 |

> **Constraints & Indexes**
> * `CHECK (status IN ('scheduled', 'sent', 'canceled', 'failed'))`
> * `INDEX idx_reminders_user_at`

### 🤖 6. bookmark_ai_summaries
북마크된 콘텐츠의 AI 요약 데이터입니다. (북마크와 1:1 관계)

| Column | Type | Nullable | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| **id** | `BIGSERIAL` | ❌ | *(Auto)* | Primary Key |
| **bookmark_id** | `BIGINT` | ❌ | | Foreign Key (`bookmarks.id`) |
| summary_short | `TEXT` | ✅ | | 짧은 요약 |
| summary_full | `TEXT` | ✅ | | 전체 요약 |
| model | `VARCHAR(50)` | ✅ | | 사용된 AI 모델명 |
| created_at | `TIMESTAMPTZ` | ❌ | `NOW()` | 생성일 |

> **Constraints & Indexes**
> * `UNIQUE (bookmark_id)`: 북마크 하나당 하나의 요약만 존재
> * `INDEX idx_ai_summary_bookmark`
