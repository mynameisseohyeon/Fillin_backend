# FILL:IN

> FILL:IN은 직장인과 은퇴 전문가가 자신의 경험과 전문성을 수업으로 등록하고,  
> 멘티가 필요한 수업과 시간을 직접 선택해 예약할 수 있는 멘토링 플랫폼입니다.
<table>
  <tr>
    <td width="50%">
      <img
        src="https://github.com/user-attachments/assets/9cb023f1-f090-417f-94c4-4acfc9a4c8f5"
        alt="FILL:IN 화면 1"
        width="100%"
      />
    </td>
    <td width="50%">
      <img
        src="https://github.com/user-attachments/assets/6ddefd5c-aa4e-4dba-bc1c-d4a0e421fdf8"
        alt="FILL:IN 화면 2"
        width="100%"
      />
    </td>
  </tr>
</table>

| 항목 | 내용 |
|---|---|
| 프로젝트 | FILL:IN |
| 형태 | 팀 프로젝트 |
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
<img width="60%" alt="25" src="https://github.com/user-attachments/assets/97eddf5a-cf0a-4537-b721-570358f42eee" />

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

### API 문서화 및 공통 예외처리
<img width="60%" alt="24" src="https://github.com/user-attachments/assets/808b0cca-b9ba-4402-a93a-bd3ef0d10108" />

일정 조회에 사용되는 날짜·제목·상태 파라미터를 Swagger에 문서화하고, <br/>
프론트엔드에서 캘린더와 일정 목록을 연동할 수 있도록 API 사용 방식을 공유했습니다.

프로젝트 전반에서 동일한 오류 형식을 사용할 수 있도록  
`BusinessException`, `ErrorCode`, `GlobalExceptionHandler` 기반의 공통 예외 처리 구조를 사용했습니다.

---

## 트러블슈팅

<img width="70%" alt="26" src="https://github.com/user-attachments/assets/20a6c6bd-9105-40b8-a296-10e3c3669689" />

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

### 2. Schedule과 ScheduleTime 저장 과정의 데이터 불일치

| PAAR | 내용 |
|---|---|
| **Problem** | 예약의 기본 정보는 `Schedule`, 실제 수업 시간은 `ScheduleTime`에 나누어 저장됩니다. 두 저장 작업이 각각 처리되면 `Schedule` 저장 후 `ScheduleTime` 저장에 실패했을 때 시간 정보가 없는 불완전한 예약 데이터가 남을 수 있었습니다. |
| **Approach** | 예약 정보와 수업 시간은 하나의 예약을 구성하는 데이터이므로, 두 저장 작업을 하나의 작업 단위로 처리해야 한다고 판단했습니다. |
| **Action** | 예약 생성 로직에 `@Transactional`을 적용해 `Schedule`과 `ScheduleTime` 저장을 하나의 트랜잭션으로 묶었습니다. 두 저장이 모두 성공한 경우에만 커밋하고, 중간에 예외가 발생하면 전체 작업이 롤백되도록 구성했습니다. |
| **Result** | 시간 정보가 없는 예약 데이터가 생성되는 문제를 방지하고, 예약 정보와 실제 수업 시간 사이의 데이터 정합성을 확보했습니다. |

```text
Schedule 저장
      ↓
ScheduleTime 저장
      ↓
모두 성공 ─────────→ Commit
      │
      └─ 하나라도 실패 → Rollback
```


---


## Architecture

<img width="60%" alt="스크린샷 2026-07-15 오후 9 28 24" src="https://github.com/user-attachments/assets/9473f883-cb5d-48a6-bec4-e92fd6ad0b77" />


---


## ERD

<img width="60%" alt="FILL:IN ERD" src="https://github.com/user-attachments/assets/6ed7f8c5-44c2-4e5b-9d0e-19da7583fac2" />

`Member`가 등록한 `Lesson`을 기준으로 예약 가능한 시간·옵션·리뷰가 연결되고, <br/>
멘티의 신청이 발생하면 `Schedule`이 생성됩니다.  <br/><br/>

`Schedule`은 예약 상태와 참여자 정보를, <br/>
`ScheduleTime`은 실제 수업 시작·종료 시간을 관리하며 결제 이력과 함께 예약 단위로 연결됩니다.
