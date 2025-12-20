# 🔌 mysave API 명세서

## 📁 북마크
| 기능 | 사용자 | Method | URL | param | 설명 |
| :--- | :---: | :---: | :--- | :---: | :--- |
| **북마크 생성** | 일반 | `POST` | `/api/bookmarks` | 없음 | 북마크 저장 |
| **북마크 목록 조회** | 일반 | `GET` | `/api/bookmarks` | 없음 | 등록된 북마크 리스트 조회 |
| **북마크 상세 조회** | 일반 | `GET` | `/api/bookmarks/{id}` | `id` | 선택한 북마크 상세 정보 조회 |
| **북마크 수정** | 일반 | `PATCH` | `/api/bookmarks/{id}` | `id` | 북마크 정보 수정 |
| **북마크 삭제** | 일반 | `DELETE` | `/api/bookmarks/{id}` | `id` | 북마크 삭제 |

## 👤 사용자
| 기능 | 사용자 | Method | URL | param | 설명 |
| :--- | :---: | :---: | :--- | :---: | :--- |
| **내 정보 조회** | 일반 | `GET` | `/api/users/me` | 없음 | 로그인된 사용자 정보 조회 |
| **알림 이메일 설정** | 일반 | `PATCH` | `/api/users/notification-email` | 없음 | 리마인더 알림 이메일 등록/수정 |

## 🔐 카카오 로그인
| 기능 | 사용자 | Method | URL | param | 설명 |
| :--- | :---: | :---: | :--- | :---: | :--- |
| **카카오 로그인 URL 발급** | 비회원 | `GET` | `/api/auth/kakao/login-url` | 없음 | 카카오 로그인 연결 URL 생성 |
| **카카오 인증 콜백 처리** | 비회원 | `GET` | `/api/auth/kakao/callback` | 없음 | 인증 완료 후 사용자 정보 처리 |
