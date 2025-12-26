# Tasks 분류 가이드

> **기준 문서:** `6-3.SRS-GPT5기반-TASK체크리스트.md`  
> **분류 기준:** SRS v1.1의 Functional Requirements와 Non-Functional Requirements

---

## 📁 폴더 구조

```
Tasks copy/
├── Functional/              # 기능 요구사항 (REQ-FUNC-xxx)
│   ├── 001_Init_Config.md
│   ├── 002_Frontend_PoC_Optimization.md
│   ├── 003_Habit_Management.md
│   ├── 004_Alarm_Core_Logic.md
│   ├── 005_Launcher_Flow_Integration.md
│   ├── 006_Structural_Refactoring.md
│   ├── 007_Analytics_and_Goal.md
│   ├── 008_Data_Export.md
│   └── 009_Onboarding_Process.md
│
├── Non-Functional/          # 비기능 요구사항 (REQ-NF-xxx)
│   ├── 010_Testing_and_Reliability.md
│   ├── 011_NonFunctional_Security.md
│   ├── 012_A11y_and_Optimization.md
│   └── 013_Final_QA_Deployment.md
│
├── 6. Task추출결과.md
├── 7.Prototype_PoC.md
├── Improvement_Tasks_Issue.md
└── README.md (본 파일)
```

---

## 📋 Functional Requirements (기능 요구사항)

**정의:** 시스템이 수행해야 하는 기능적 동작을 정의하는 요구사항

### 관련 REQ-FUNC-xxx 매핑

| 파일 | 관련 REQ | Epic | 설명 |
|------|---------|------|------|
| `001_Init_Config.md` | - | EPIC-0 | 프로젝트 초기 설정 및 아키텍처 구축 |
| `002_Frontend_PoC_Optimization.md` | - | EPIC-1 | 프론트엔드 PoC 및 성능 최적화 |
| `003_Habit_Management.md` | REQ-FUNC-001~003 | EPIC-2 | 습관 생성/수정/삭제 및 활성 요일 설정 |
| `004_Alarm_Core_Logic.md` | REQ-FUNC-004~006, 008, 009 | EPIC-3 | 알람/타이머 설정 및 OS 알림 연동 |
| `005_Launcher_Flow_Integration.md` | REQ-FUNC-012~018 | EPIC-4 | 알람 울림 → YES/NO → 기록 → 명언 플로우 |
| `006_Structural_Refactoring.md` | - | Refactoring | 코드 구조 개선 및 에러 처리 강화 |
| `007_Analytics_and_Goal.md` | REQ-FUNC-019~022 | EPIC-5 | 통계 집계, 그래프 시각화, 목표 관리 |
| `008_Data_Export.md` | REQ-FUNC-007, 010, 011 | EPIC-6 | CSV/XLSX 데이터 내보내기 및 공유 |
| `009_Onboarding_Process.md` | REQ-FUNC-023 | EPIC-7 | 초기 사용자 온보딩 및 기본 설정 |

---

## 🔧 Non-Functional Requirements (비기능 요구사항)

**정의:** 시스템의 품질 속성(성능, 보안, 신뢰성 등)을 정의하는 요구사항

### 관련 REQ-NF-xxx 매핑

| 파일 | 관련 REQ | 설명 |
|------|---------|------|
| `010_Testing_and_Reliability.md` | REQ-NF-003 | 테스트 코드 작성 및 데이터 무손실 신뢰성 확보 |
| `011_NonFunctional_Security.md` | REQ-NF-001, 002, 004, 005 | 성능 최적화, 보안/프라이버시 점검 |
| `012_A11y_and_Optimization.md` | REQ-NF-006, 007, 008 | 접근성, 사용성, 이식성, 유지보수성 개선 |
| `013_Final_QA_Deployment.md` | - | 최종 QA 및 배포 준비 |

---

## 🎯 분류 기준 상세

### Functional Requirements 분류 기준
- **사용자가 직접 사용하는 기능** (CRUD, UI 화면, 비즈니스 로직)
- **SRS의 REQ-FUNC-001 ~ 023**에 해당하는 모든 기능
- **Epic 기반 기능 개발** (HABIT_MGMT, ALARM_CORE, LAUNCHER_FLOW 등)

### Non-Functional Requirements 분류 기준
- **성능 (Performance):** REQ-NF-001, 002
- **신뢰성 (Reliability):** REQ-NF-003
- **보안/프라이버시 (Security/Privacy):** REQ-NF-004, 005
- **사용성 (Usability):** REQ-NF-006
- **이식성 (Portability):** REQ-NF-007
- **유지보수성 (Maintainability):** REQ-NF-008

---

## 📊 Task 통계

- **Functional Tasks:** 9개
- **Non-Functional Tasks:** 4개
- **Total:** 13개 Task 파일

---

## 🔗 참고 문서

- `6-3.SRS-GPT5기반-TASK체크리스트.md` - Task 추출 및 분류 기준
- `5-2.PRD기반 SRS(Software-requirements-specification)_GPT5.md` - 소프트웨어 요구사항 명세서
- `6. Task추출결과.md` - 통합 Task 목록

---

**마지막 업데이트:** 2025-01-15

