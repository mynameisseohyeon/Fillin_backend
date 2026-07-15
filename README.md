# FILL:IN

> FILL:IN은 직장인과 은퇴 전문가가 자신의 경험과 전문성을 수업으로 등록하고,  
> 멘티가 필요한 수업과 시간을 직접 선택해 예약할 수 있는 멘토링 플랫폼입니다.

| 항목 | 내용 |
|---|---|
| 프로젝트 | FILL:IN |
| 형태 | 팀 프로젝트 |
| 담당 역할 | Backend Developer |
| 주요 담당 | 일정 조회 및 검색, KST·UTC 시간 변환, 조회 조건 통합, Swagger 문서화 |
| 프로젝트 기간 | 2026.01.06 ~ 2026.01.22 |
| 팀 인원 | 4명 |


---

## Tech Stack
Backend

<p> <img src="https://img.shields.io/badge/Java_21-007396?style=for-the-badge&logo=openjdk&logoColor=white" /> <img src="https://img.shields.io/badge/Spring_Boot_3.x-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" /> <img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white" /> <img src="https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white" /> <img src="https://img.shields.io/badge/QueryDSL-0769AD?style=for-the-badge&logo=hibernate&logoColor=white" /> </p>

Database & Payment

<p> <img src="https://img.shields.io/badge/MySQL_8.x-4479A1?style=for-the-badge&logo=mysql&logoColor=white" /> <img src="https://img.shields.io/badge/Toss_Payments-0064FF?style=for-the-badge&logo=toss&logoColor=white" /> </p>

Frontend

<p> <img src="https://img.shields.io/badge/React_18.3-61DAFB?style=for-the-badge&logo=react&logoColor=black" /> <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" /> <img src="https://img.shields.io/badge/Vite_6.3-646CFF?style=for-the-badge&logo=vite&logoColor=white" /> <img src="https://img.shields.io/badge/Tailwind_CSS_v4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white" /> <img src="https://img.shields.io/badge/Zustand-443E38?style=for-the-badge&logo=react&logoColor=white" /> <img src="https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white" /> </p>

Infrastructure & Documentation

<p> <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" /> <img src="https://img.shields.io/badge/Python_Automation-3776AB?style=for-the-badge&logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logo=swagger&logoColor=black" /> <img src="https://img.shields.io/badge/OpenAPI-6BA539?style=for-the-badge&logo=openapiinitiative&logoColor=white" /> </p>

Collaboration

<p> <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" /> <img src="https://img.shields.io/badge/Notion-000000?style=for-the-badge&logo=notion&logoColor=white" /> <img src="https://img.shields.io/badge/Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white" /> <img src="https://img.shields.io/badge/Figma-F24E1E?style=for-the-badge&logo=figma&logoColor=white" /> <img src="https://img.shields.io/badge/Gemini_AI_Review-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white" /> </p>

---
## 주요 기능

| 기능        | 설명                                     |
| --------- | -------------------------------------- |
| 전문가·수업 탐색 | 분야와 카테고리별 전문가 및 수업 검색, 가격·리뷰 정보 제공     |
| 시간 기반 예약  | 멘토의 가능 시간 등록, 멘티의 시간 선택 및 일정 조회        |
| 결제·정산     | Toss Payments 결제, 결제 금액 검증, 수업 완료 후 정산 |
| 리뷰·프로필    | 멘토 경력 관리, 수강 완료 후 리뷰 및 평점 제공           |

---

## 담당 기능

### 일정 조회 및 캘린더 API

사용자가 멘토 또는 멘티로 참여한 일정을 목적별로 조회할 수 있도록
전체·예정·과거 일정과 날짜별 캘린더 조회 API를 구현했습니다.

| 기능    | 구현 내용                        |
| ----- | ---------------------------- |
| 일정 조회 | 전체·예정·과거·날짜별 일정 조회           |
| 검색 조건 | 날짜·제목·일정 상태 필터링              |
| 시간 처리 | KST 조회 범위를 UTC `Instant`로 변환 |
| 목록 처리 | `Pageable` 기반 페이지네이션         |
| 문서화   | Swagger 검색 파라미터 설명 추가        |

조회 API별로 반복되던 검색 조건 처리는 `getFilteredPage`로 분리해 공통으로 사용했습니다.

```text
조회 요청
  → 날짜·제목·상태 조건 정리
  → KST 시간을 UTC Instant로 변환
  → 일정 조회
  → Page 응답 반환
```

### API 문서화 및 협업

일정 조회에 사용되는 날짜·제목·상태 파라미터를 Swagger에 문서화하고, <br/>
프론트엔드에서 캘린더와 일정 목록을 연동할 수 있도록 API 사용 방식을 공유했습니다.


---

## 트러블슈팅

### 1. UTC / KST 날짜 경계로 인한 일정 조회 불일치

| PAAR | 내용 |
|---|---|
| **Problem** | 사용자는 KST 날짜를 기준으로 캘린더를 조회하지만, 일정 시간은 `Instant`로 저장됩니다. 날짜 검색 범위를 서버 기본 시간대나 `LocalDateTime` 상태로 전달하면 자정 전후 일정이 선택한 날짜에서 누락되거나 인접 날짜에 포함될 수 있었습니다. |
| **Approach** | 사용자가 입력한 `LocalDate`로 하루의 시작과 종료 시점을 계산한 뒤, `Asia/Seoul` 시간대를 명시해 UTC `Instant`로 변환하도록 조회 흐름을 정리했습니다. |
| **Action** | Repository의 조회 범위 타입을 `Instant`로 변경하고, 조회 서비스에서 시작·종료 시점을 `atZone(ZoneId.of("Asia/Seoul")).toInstant()`로 변환해 전달했습니다. |
| **Result** | KST 기준 날짜와 데이터베이스 조회 범위의 기준이 일치해 날짜 경계의 조회 오류 가능성을 줄였고, 서버 실행 환경의 기본 시간대에 덜 의존하는 구조를 만들었습니다. |

```text
사용자 날짜 선택
    → KST 하루 범위 계산
    → UTC Instant 변환
    → Repository 기간 조회
    → 화면에서 사용자 시간대로 표시
```

---

### 2. 전체·예정·과거 일정 조회 로직의 중복과 정렬 기준 불명확

| PAAR | 내용 |
|---|---|
| **Problem** | 캘린더, 예정 일정, 과거 일정이 서로 다른 조회 목적을 가지지만 날짜·제목·상태 필터링 과정은 유사했습니다. 조회 API별로 같은 조건 처리 코드가 반복되면 수정 시 누락될 가능성이 있고, 예정·과거 일정의 정렬 기준도 명확하게 관리하기 어려웠습니다. |
| **Approach** | API는 캘린더·예정·과거 조회로 분리하되, 실제 필터 파라미터 정리와 Repository 호출은 공통 메서드로 모으는 방식을 선택했습니다. |
| **Action** | `getCalendarSchedules`, `getUpcomingSchedules`, `getPastSchedules`로 사용 목적을 분리하고, 공통 조회 로직을 `getFilteredPage`로 추출했습니다. 예정 일정은 현재 이후, 과거 일정은 현재 이전으로 범위를 제한하고 페이지네이션과 정렬 조건을 적용했습니다. |
| **Result** | 조회 목적이 API 이름과 코드 구조에 드러나도록 개선했고, 날짜·제목·상태 필터의 중복 처리를 줄였습니다. 또한 사용자가 예정 일정은 가까운 순서로, 과거 일정은 최근 순서로 확인할 수 있는 기반을 마련했습니다. |

```text
Calendar  ─┐
Upcoming  ─┼─→ 공통 필터 정리 → 기간을 Instant로 변환 → Repository 조회 → DTO 변환
Past      ─┘
```

---

## Architecture



---

## ERD

<img width="1175" height="826" alt="FILL:IN ERD" src="https://github.com/user-attachments/assets/6ed7f8c5-44c2-4e5b-9d0e-19da7583fac2" />

---


