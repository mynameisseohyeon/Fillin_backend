# FILL:IN 
> **"전문가의 자투리 시간으로 당신의 성장을 채우고, 나의 유휴 시간을 수익으로 메우는 틈새 능력 마켓"**

---

## 1. 프로젝트 개요
**N잡러 시대의 도래:** 역대 최대치인 67만 명의 N잡러 시대, 직장인들의 유휴 시간과 전문 지식을 수익화할 창구가 필요합니다.
**Micro-Consulting 수요 증가:** 긴 교육 과정보다 "이력서 30분 피드백"과 같이 즉각적이고 구체적인 실무 도움을 원하는 사용자가 증가하고 있습니다.
**자원의 효율 극대화:** 사장되는 전문 지식을 '자투리 시간'이라는 컨셉에 맞춰 최적화된 소비 모델로 제공하고자 합니다.

---

## 2. 핵심 솔루션
**FILL:IN (채우다, 메우다):** 전문가의 경험으로 사용자의 고민을 채우고, 플랫폼을 통해 서로의 빈 공간을 메워가는 가치를 실현합니다.
**Time Slot 기반 거래:** 강사가 설정한 15/30분 단위의 가용 시간 슬롯을 사용자가 짧은 단위로 구매합니다.
**에스크로 기반 안전 거래:** 노쇼(No-Show)를 방지하고, 서비스 완료 시점에 정산이 이루어지는 신뢰 기반 시스템입니다.

---

## 3. 개발 환경 및 기술 스택

<img width="800" alt="기술스택" src="https://github.com/user-attachments/assets/d8f62472-7f70-4f4f-8a13-a581803623b7" />

| 분류 | 기술 스택 |
| :-- | :-- |
| **Front-end** | <img src="https://img.shields.io/badge/React_18.3-61DAFB?style=flat-square&logo=React&logoColor=black"/> <img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white"/> <img src="https://img.shields.io/badge/Vite_6.3-646CFF?style=flat-square&logo=vite&logoColor=white"/> <img src="https://img.shields.io/badge/Tailwind_v4-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white"/> <img src="https://img.shields.io/badge/Zustand-443E38?style=flat-square&logo=react&logoColor=white"/> <img src="https://img.shields.io/badge/Axios-5A29E4?style=flat-square&logo=axios&logoColor=white"/> |
| **Back-end** | <img src="https://img.shields.io/badge/Spring_Boot_3.x-6DB33F?style=flat-square&logo=springboot&logoColor=white"/> <img src="https://img.shields.io/badge/Java_21-007396?style=flat-square&logo=java&logoColor=white"/> <img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=flat-square&logo=springsecurity&logoColor=white"/> <img src="https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=flat-square&logo=spring&logoColor=white"/> <img src="https://img.shields.io/badge/MySQL_8.x-4479A1?style=flat-square&logo=mysql&logoColor=white"/> <img src="https://img.shields.io/badge/QueryDSL-0769AD?style=flat-square&logo=hibernate&logoColor=white"/> |
| **Infra** | <img src="https://img.shields.io/badge/Toss_Payments-0064FF?style=flat-square&logo=toss&logoColor=white"/> <img src="https://img.shields.io/badge/Python_Automation-3776AB?style=flat-square&logo=python&logoColor=white"/> <img src="https://img.shields.io/badge/Gemini_AI_Review-412991?style=flat-square&logo=google-gemini&logoColor=white"/> <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white"/> |
| **Collaboration** | <img src="https://img.shields.io/badge/Figma-F24E1E?style=flat-square&logo=figma&logoColor=white"/> <img src="https://img.shields.io/badge/Notion-000000?style=flat-square&logo=notion&logoColor=white"/> <img src="https://img.shields.io/badge/Discord-5865F2?style=flat-square&logo=discord&logoColor=white"/> <img src="https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white"/> |

---

## 4. 페이지별 기능

### 메인 및 전문가 탐색
**카테고리 필터링:** QueryDSL을 활용해 대량의 전문가 데이터 중 사용자가 원하는 카테고리를 초고속으로 검색합니다.

### 마이크로 예약 시스템
**Time Slot Picker:** 15/30분 단위로 세분화된 가용 시간을 직관적으로 선택합니다.
**동시성 제어:** 인기 멘토의 슬롯에 예약이 몰려도 비관적 락(Pessimistic Lock)을 통해 중복 예약을 원천 차단합니다.

### 포인트 결제 및 에스크로
**Toss Payments:** 토스페이먼츠 SDK를 연동하여 간편한 포인트 충전 환경을 제공합니다.
**안전 정산:** 결제된 금액은 플랫폼이 보관(Escrow)하며, 상담 종료가 확인된 시점에만 전문가에게 정산됩니다.

### 리뷰 및 프로필 관리
**닉네임/이미지 관리:** Spring Security와 연동된 회원 정보 수정을 통해 퍼스널 브랜딩을 지원합니다.
**평점 시스템:** 실제 상담을 완료한 유저만 리뷰를 남길 수 있도록 제한하여 신뢰도를 높였습니다.

---

## 5. 백엔드 핵심 트러블 슈팅

### 인기 시간대 중복 예약 발생 
**문제:** 여러 명의 사용자가 동시에 같은 슬롯에 결제를 요청할 경우 데이터 정합성이 깨지는 현상 발견.
**해결:** JPA의 비관적 락을 적용하여 특정 슬롯의 데이터 수정 권한을 원자적으로 관리하도록 로직 개선.
**결과:** 동시 결제 시에도 중복 예약이 발생하지 않는 안정적인 예약 환경 구축.

### 정산 스케줄러 부하 최적화
**문제:** 정해진 시간에 수만 건의 예약 종료 여부를 판단할 때 시스템 부하 우려.
**해결:** `Bulk Update` 쿼리를 적용하여 상태 변경 속도를 개선하고, 정산 로직을 비동기로 처리하여 메인 서버 성능 유지.

---

## 6. 데이터베이스 구조 (ERD)
<img width="1175" height="826" alt="002" src="https://github.com/user-attachments/assets/6ed7f8c5-44c2-4e5b-9d0e-19da7583fac2" />


---
