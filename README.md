# 🚀 MySave - [기초웹개발론 기말 프로젝트 8조]

## 📚 목차 (Table of Contents)

1. [프로젝트 개요](#1-프로젝트-개요-project-overview)
2. [프로젝트 저장소 링크](#2-프로젝트-저장소-링크-repositories)
3. [배포 주소](#3-배포-주소-deployment)
4. [시스템 구조 및 기술 스택](#4-시스템-구조-및-기술-스택-architecture--tech-stack)
   - [전체 시스템 아키텍처](#4-1-전체-시스템-아키텍처-system-architecture)
   - [기술 스택](#4-2-기술-스택-tech-stack)
5. [실행 방법 및 환경 정보](#5-실행-방법-및-환경-정보-environment)


---

## 1. 📌 프로젝트 개요 (Project Overview)

### 🧩 한 줄 소개
> **"MySave는 다시 읽지 않는 북마크 문제를 해결하기 위한, 리마인드 기반 개인화 북마크 관리 서비스입니다."**

### 🎯 기획 의도
웹 서핑 중 유용한 아티클을 발견해도 대부분은 **"일단 저장"**으로 끝나고 다시 열어보지 않게 됩니다.
기존 브라우저 북마크는 **저장 맥락 부재**, **분류의 어려움**, **리마인드 기능 부재** 등의 한계가 있습니다.

**MySave**는 이러한 문제를 해결하기 위해 다음과 같은 목표를 가집니다.
* **Chrome Extension**을 통한 빠르고 간편한 저장
* **메모·태그·리마인드** 기능을 결합하여 저장된 정보의 실질적 재소비 유도

### ⭐ 주요 기능
* **🔖 북마크 CRUD:** 링크 저장 시 메모를 함께 기록하여 저장 맥락 보존
* **🏷️ 태그 관리:** 태그 기반의 체계적인 분류 및 필터링
* **⏰ 리마인드 알림:** 사용자가 설정한 시점에 다시 읽기 알림 제공
* **🌐 Chrome Extension:** 브라우징 흐름을 끊지 않는 즉시 북마크 저장
* **📊 웹 대시보드:** 읽음/안읽음 상태 관리 및 시각화 된 대시보드 제공

---

## 2. 프로젝트 저장소 링크 (Repositories)
이 프로젝트는 Frontend와 Backend 저장소가 분리되어 관리됩니다. 소스코드는 아래 링크에서 확인하실 수 있습니다.

| 파트 | 저장소 링크 | 비고 |
| :-- | :-- | :-- |
| **Frontend** | [MySave_FE 바로가기](https://github.com/MySave1/MySave_FE) | HTML, CSS, JS 기반 |
| **Backend** | [MySave_BE 바로가기](https://github.com/MySave1/MySave_BE) | Springboot 기반 |

---

## 3. 배포 주소 (Deployment)
* **Frontend:** [배포된 URL 입력]
* **Backend API:** (http://13.60.25.65:8080)
* **Swagger/API Docs:** (http://13.60.25.65:8080/swagger-ui/index.html)

---

## 4. 시스템 구조 및 기술 스택 (Architecture & Tech Stack)

### 4-1. 전체 시스템 아키텍처 (System Architecture)
[전체구조도]<img width="1043" height="582" alt="architecture" src="https://github.com/user-attachments/assets/04883c36-d47e-412d-a543-93dc95d4992b" />


본 서비스는 **Chrome Extension**을 통해 데이터를 수집하고, **Web Dashboard**에서 데이터를 시각화 및 관리하는 구조로 동작합니다.

* **Data Flow:** 사용자가 웹 서핑 중 Chrome Extension을 통해 `URL`, `제목`, `태그`를 저장하면, Spring Boot 서버가 이를 처리하여 PostgreSQL에 저장합니다.
* **Visualization:** 저장된 데이터는 Web Dashboard(HTML/CSS/JS)를 통해 카드 뉴스 형태의 UI로 제공되며, 리마인드 및 요약 기능을 제공합니다.

<br>

### 4-2. 기술 스택 (Tech Stack)

| 구분 | 기술 (Technology) | 설명 (Description) |
| :--- | :--- | :--- |
| **Frontend** | ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) | • 대시보드 및 리스트 UI 구현<br>• `Fetch API`를 활용한 비동기 데이터 통신<br>• 반응형 웹 디자인 적용 |
| **Backend** | ![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white) ![Java](https://img.shields.io/badge/Java-007396?style=flat-square&logo=java&logoColor=white) | • RESTful API 서버 구축<br>• 북마크(CRUD), 리마인드, 태그 기능 비즈니스 로직 처리<br>• Layered Architecture (Controller-Service-Repository) 적용 |
| **Database** | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) | • 관계형 데이터베이스(RDBMS) 구축<br>• 사용자, 북마크, 태그 데이터 모델링 및 저장 |
| **Extension** | ![Chrome](https://img.shields.io/badge/Chrome_Extension-4285F4?style=flat-square&logo=google-chrome&logoColor=white) | • 현재 탭의 정보(URL, Title) 스크래핑<br>• 백엔드 API로 데이터 전송 (POST 요청) |
| **Infra** | ![AWS EC2](https://img.shields.io/badge/AWS_EC2-FF9900?style=flat-square&logo=amazon-aws&logoColor=white) | • 클라우드 서버 호스팅<br>• Spring Boot 및 DB 서버 배포 환경 |

---

## 5. 실행 방법 및 환경 정보 (Environment)
### 🔹 Frontend 환경
* **Node Version:** v18.xx.x
* **Framework:** React v18
* **실행 방법:**
  ```bash
  git clone [https://github.com/MySave1/MySave_FE.git](https://github.com/MySave1/MySave_FE.git)
  npm install
  npm run dev
