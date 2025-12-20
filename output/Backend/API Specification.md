# 🔌 mysave API 명세서

## 1. 개요
* **프로젝트명:** mysave
* **기능:** 북마크 관리 및 사용자 설정, 소셜 로그인

---

## 2. API 상세 명세

### 📁 북마크 (Bookmarks)
| 기능 | 사용자 | Method | URL | Param | 설명 |
| :--- | :---: | :---: | :--- | :---: | :--- |
| **북마크 생성** | 일반 | `POST` | `/api/bookmarks` | - | 북마크 저장 |
| **북마크 목록 조회** | 일반 | `GET` | `/api/bookmarks` | - | 등록된 북마크 리스트 조회 |
| **북마크 상세 조회** | 일반 | `GET` | `/api/bookmarks/{id}` | `id` | 선택한 북마크 상세 정보 조회 |
| **북마크 수정** | 일반 | `PATCH` | `/api/bookmarks/{id}` | `id` | 북마크 정보 수정 |
| **북마크 삭제** | 일반 | `DELETE` | `/api/bookmarks/{id}` | `id` | 북마크 삭제 |

### 👤 사용자 (Users)
| 기능 | 사용자 | Method | URL | Param | 설명 |
| :--- | :---: | :---: | :--- | :---: | :--- |
| **내 정보 조회** | 일반 | `GET` | `/api/users/me` | - | 로그인된 사용자 정보 조회 |
| **알림 이메일 설정** | 일반 | `PATCH` | `/api/users/notification-email` | - | 리마인더 알림 이메일 등록/수정 |

### 🔐 인증 (Authentication)
| 기능 | 사용자 | Method | URL | Param | 설명 |
| :--- | :---: | :---: | :--- | :---: | :--- |
| **카카오 로그인** | 일반 | - | - | - | 카카오 OAuth2 연동 로그인 |
