# 🚀 MySave - [기초웹개발론 기말 프로젝트 8조]


## 1. 프로젝트 저장소 링크 (Repositories)
이 프로젝트는 Frontend와 Backend 저장소가 분리되어 관리됩니다. 소스코드는 아래 링크에서 확인하실 수 있습니다.

| 파트 | 저장소 링크 | 비고 |
| :-- | :-- | :-- |
| **Frontend** | [MySave_FE 바로가기](https://github.com/MySave1/MySave_FE) | React, Vite 기반 |
| **Backend** | [MySave_BE 바로가기](https://github.com/MySave1/MySave_BE) | Node.js, Express 기반 |

---

## 2. 배포 주소 (Deployment)
* **Frontend:** [배포된 URL 입력]
* **Backend API:** [서버 URL 입력]
* **Swagger/API Docs:** [API 문서 URL 입력]

---

## 3. 시스템 구조 및 기술 스택 (Architecture & Tech Stack)

### 3-1. 전체 시스템 아키텍처 (System Architecture)
[전체구조도]<img width="1043" height="582" alt="architecture" src="https://github.com/user-attachments/assets/04883c36-d47e-412d-a543-93dc95d4992b" />


본 서비스는 **Chrome Extension**을 통해 데이터를 수집하고, **Web Dashboard**에서 데이터를 시각화 및 관리하는 구조로 동작합니다.

* **Data Flow:** 사용자가 웹 서핑 중 Chrome Extension을 통해 `URL`, `제목`, `태그`를 저장하면, Spring Boot 서버가 이를 처리하여 PostgreSQL에 저장합니다.
* **Visualization:** 저장된 데이터는 Web Dashboard(HTML/CSS/JS)를 통해 카드 뉴스 형태의 UI로 제공되며, 리마인드 및 요약 기능을 제공합니다.

<br>

### 3-2. 기술 스택 (Tech Stack)

| 구분 | 기술 (Technology) | 설명 (Description) |
| :--- | :--- | :--- |
| **Frontend** | ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | • 대시보드 및 리스트 UI 구현<br>• `Fetch API`를 활용한 비동기 데이터 통신<br>• 반응형 웹 디자인 적용 |
| **Backend** | ![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white) ![Java](https://img.shields.io/badge/Java-007396?style=flat-square&logo=java&logoColor=white) | • RESTful API 서버 구축<br>• 북마크(CRUD), 리마인드, 태그 기능 비즈니스 로직 처리<br>• Layered Architecture (Controller-Service-Repository) 적용 |
| **Database** | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) | • 관계형 데이터베이스(RDBMS) 구축<br>• 사용자, 북마크, 태그 데이터 모델링 및 저장 |
| **Extension** | ![Chrome](https://img.shields.io/badge/Chrome_Extension-4285F4?style=flat-square&logo=google-chrome&logoColor=white) | • 현재 탭의 정보(URL, Title) 스크래핑<br>• 백엔드 API로 데이터 전송 (POST 요청) |
| **Infra** | ![AWS EC2](https://img.shields.io/badge/AWS_EC2-FF9900?style=flat-square&logo=amazon-aws&logoColor=white) | • 클라우드 서버 호스팅<br>• Spring Boot 및 DB 서버 배포 환경 |

---

## 4. 실행 방법 및 환경 정보 (Environment)
### 🔹 Frontend 환경
* **Node Version:** v18.xx.x
* **Framework:** React v18
* **실행 방법:**
  ```bash
  git clone [https://github.com/MySave1/MySave_FE.git](https://github.com/MySave1/MySave_FE.git)
  npm install
  npm run dev
