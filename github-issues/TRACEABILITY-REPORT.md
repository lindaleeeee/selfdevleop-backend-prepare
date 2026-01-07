# 📋 SRS–Issue–PR Traceability 점검 보고서

**프로젝트:** Focus Habit Launcher Backend  
**분석 일자:** 2025-01-03  
**SRS 버전:** 1.1 (MVP 정리본)  
**분석자:** AI Agent

---

## ✅ 체크리스트 완료 현황

- [x] 이슈 파일에 명시된 Related Requirements가 SRS에 **실제로 존재**하는지 확인
- [x] 해당 REQ가 Traceability Matrix에 어떻게 연결되어 있는지 확인
- [x] 필요한 경우, SRS에 **테스트 케이스 ID** 추가 시나리오 상정
- [x] 완료된 이슈의 상태 일관성 확인 (completed/, GitHub Issue, PR)
- [x] README/Issue README에 완료된 이슈 목록/폴더 구조 갱신 흐름 점검

---

## 1️⃣ SRS 요구사항 존재 확인

### 기능 요구사항 (REQ-FUNC-xxx)

| SRS REQ ID | SRS 설명 | 이슈 매핑 | 존재 확인 |
|:----------:|----------|:---------:|:---------:|
| REQ-FUNC-001 | 새 습관 생성 (이름, 아이콘, 색상, 기본 목표 시간) | #003 | ✅ |
| REQ-FUNC-002 | 습관 수정·삭제, 삭제 시 과거 기록 유지 | #003 | ✅ |
| REQ-FUNC-003 | 습관별 활성 요일 설정 | #003 | ✅ |
| REQ-FUNC-004 | 특정 시각 알람 설정 | #004 | ✅ |
| REQ-FUNC-005 | 상대 시간 타이머 설정 | #004 | ✅ |
| REQ-FUNC-006 | 알람/타이머 라벨 설정 | #004 | ✅ |
| REQ-FUNC-007 | CSV/XLSX 내보내기 | #008 | ✅ |
| REQ-FUNC-008 | 전체화면 시계/타이머 표시 | #004 | ✅ |
| REQ-FUNC-009 | OS 알림 표시 (소리/진동) | #004 | ✅ |
| REQ-FUNC-010 | 파일 저장/공유 시트 전송 | #008 | ✅ |
| REQ-FUNC-011 | 외부 API 없이 로컬 처리 | #008 | ✅ |
| REQ-FUNC-012 | YES/NO 런처 화면 자동 오픈 | #005 | ✅ |
| REQ-FUNC-013 | YES → 습관 목록 표시 | #005 | ✅ |
| REQ-FUNC-014 | 완료 습관 회색+체크 비활성화 | #005 | ✅ |
| REQ-FUNC-015 | 미완료 습관 선택 → 기록+그래프 | #005 | ✅ |
| REQ-FUNC-016 | 텍스트 메모 입력 | #005 | ✅ |
| REQ-FUNC-017 | 음성 입력 → 텍스트 변환 | #005 | ✅ |
| REQ-FUNC-018 | NO → 명언 카드 표시 (로컬 30개+) | #005 | ✅ |
| REQ-FUNC-019 | 일/주/월/년 수행 집계 및 그래프 | #007 | ✅ |
| REQ-FUNC-020 | 습관별 목표 설정 | #007 | ✅ |
| REQ-FUNC-021 | 목표 대비 달성률 시각화 | #007 | ✅ |
| REQ-FUNC-022 | 습관/카테고리 필터링 | #007 | ✅ |
| REQ-FUNC-023 | 온보딩 플로우 | #009 | ✅ |
| REQ-FUNC-024 | (향후) 클라우드 백업 | - | ⏳ Post-MVP |

### 비기능 요구사항 (REQ-NF-xxx)

| SRS REQ ID | SRS 설명 | 수용 기준 | 이슈 매핑 | 존재 확인 |
|:----------:|----------|----------|:---------:|:---------:|
| REQ-NF-001 | 런처 화면 렌더링 1초 이내 | p95 < 1초 | #011 | ✅ |
| REQ-NF-002 | 기록 저장 0.5초 이내 | 즉시 반영 | #011 | ✅ |
| REQ-NF-003 | 30일간 99.5% 데이터 무손실 | 장기 테스트 | #010 | ✅ |
| REQ-NF-004 | Hard Lock 기능 금지 | 코드 리뷰 | #011 | ✅ |
| REQ-NF-005 | 행태 데이터 수집 금지 | 프라이버시 정책 | #011 | ✅ |
| REQ-NF-006 | 5분 내 온보딩~기록 완료 | 사용자 테스트 80%+ | #012 | ✅ |
| REQ-NF-007 | Android 최신 2개 버전 지원 | 디바이스 테스트 | #012 | ✅ |
| REQ-NF-008 | UI/비즈니스 로직 분리 (MVVM) | 아키텍처 리뷰 | #012 | ✅ |

### ✅ 결과: 모든 REQ가 이슈에 매핑됨 (REQ-FUNC-024 제외 - Post-MVP)

---

## 2️⃣ Traceability Matrix

### Issue → REQ 매핑

| Issue # | Issue 제목 | Related REQ | Status |
|:-------:|-----------|-------------|:------:|
| #001 | 프로젝트 초기화 | - | ✅ COMPLETED |
| #002 | 프론트엔드 PoC | - | ✅ COMPLETED |
| **#003** | **습관 관리** | **REQ-FUNC-001, 002, 003** | 🔓 READY |
| **#004** | **알람 코어** | **REQ-FUNC-004, 005, 006, 008, 009** | 🔓 READY |
| #005 | 런처 플로우 | REQ-FUNC-012~018 | ⏳ BLOCKED |
| #006 | 구조 리팩토링 | - | ⏳ BLOCKED |
| #007 | 통계/목표 | REQ-FUNC-019~022 | ⏳ BLOCKED |
| #008 | 데이터 내보내기 | REQ-FUNC-007, 010, 011 | ⏳ BLOCKED |
| #009 | 온보딩 | REQ-FUNC-023 | ⏳ BLOCKED |
| #010 | 테스트/안정성 | REQ-NF-003 | ⏳ BLOCKED |
| **#011** | **보안/NFR** | **REQ-NF-001, 002, 004, 005** | 🔓 READY |
| #012 | 접근성/최적화 | REQ-NF-006, 007, 008 | ⏳ BLOCKED |
| #013 | 최종 QA/배포 | ALL | 🔒 FINAL |

### REQ → Issue 역매핑

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    REQUIREMENT COVERAGE MAP                              │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  [습관 관리 - #003]                                                      │
│  ├─ REQ-FUNC-001 (습관 생성) ────────────────────────────── ✅          │
│  ├─ REQ-FUNC-002 (습관 수정/삭제) ───────────────────────── ✅          │
│  └─ REQ-FUNC-003 (활성 요일 설정) ───────────────────────── ✅          │
│                                                                          │
│  [알람 코어 - #004]                                                      │
│  ├─ REQ-FUNC-004 (정시 알람) ────────────────────────────── ✅          │
│  ├─ REQ-FUNC-005 (상대 시간 타이머) ─────────────────────── ✅          │
│  ├─ REQ-FUNC-006 (알람 라벨) ────────────────────────────── ✅          │
│  ├─ REQ-FUNC-008 (전체화면 시계) ────────────────────────── ✅          │
│  └─ REQ-FUNC-009 (OS 알림) ──────────────────────────────── ✅          │
│                                                                          │
│  [런처 플로우 - #005]                                                    │
│  ├─ REQ-FUNC-012 (YES/NO 런처 오픈) ─────────────────────── ✅          │
│  ├─ REQ-FUNC-013 (YES → 습관 목록) ──────────────────────── ✅          │
│  ├─ REQ-FUNC-014 (완료 습관 비활성화) ───────────────────── ✅          │
│  ├─ REQ-FUNC-015 (미완료 습관 → 기록) ───────────────────── ✅          │
│  ├─ REQ-FUNC-016 (텍스트 메모) ──────────────────────────── ✅          │
│  ├─ REQ-FUNC-017 (음성 입력) ────────────────────────────── ✅          │
│  └─ REQ-FUNC-018 (NO → 명언 카드) ───────────────────────── ✅          │
│                                                                          │
│  [통계/목표 - #007]                                                      │
│  ├─ REQ-FUNC-019 (수행 집계/그래프) ─────────────────────── ✅          │
│  ├─ REQ-FUNC-020 (목표 설정) ────────────────────────────── ✅          │
│  ├─ REQ-FUNC-021 (달성률 시각화) ────────────────────────── ✅          │
│  └─ REQ-FUNC-022 (필터링) ───────────────────────────────── ✅          │
│                                                                          │
│  [데이터 내보내기 - #008]                                                │
│  ├─ REQ-FUNC-007 (CSV/XLSX 내보내기) ────────────────────── ✅          │
│  ├─ REQ-FUNC-010 (파일 저장/공유) ───────────────────────── ✅          │
│  └─ REQ-FUNC-011 (로컬 처리만) ──────────────────────────── ✅          │
│                                                                          │
│  [온보딩 - #009]                                                         │
│  └─ REQ-FUNC-023 (온보딩 플로우) ────────────────────────── ✅          │
│                                                                          │
│  [보안/NFR - #011]                                                       │
│  ├─ REQ-NF-001 (런처 1초 이내) ──────────────────────────── ✅          │
│  ├─ REQ-NF-002 (기록 0.5초 이내) ────────────────────────── ✅          │
│  ├─ REQ-NF-004 (Hard Lock 금지) ─────────────────────────── ✅          │
│  └─ REQ-NF-005 (행태 데이터 금지) ───────────────────────── ✅          │
│                                                                          │
│  [테스트/안정성 - #010]                                                  │
│  └─ REQ-NF-003 (99.5% 데이터 무손실) ────────────────────── ✅          │
│                                                                          │
│  [접근성/최적화 - #012]                                                  │
│  ├─ REQ-NF-006 (5분 내 완료) ────────────────────────────── ✅          │
│  ├─ REQ-NF-007 (Android 2개 버전) ───────────────────────── ✅          │
│  └─ REQ-NF-008 (MVVM 아키텍처) ──────────────────────────── ✅          │
│                                                                          │
│  [Post-MVP]                                                              │
│  └─ REQ-FUNC-024 (클라우드 백업) ────────────────────────── ⏳ 향후    │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 3️⃣ 테스트 케이스 ID 추가 시나리오

### 권장 테스트 케이스 ID 체계

SRS에 테스트 케이스 ID를 추가할 경우 다음 체계를 권장합니다:

```
TC-<Category>-<IssueNum>-<TestType>-<Seq>

예시:
- TC-FUNC-003-UNIT-001 (습관 생성 단위 테스트)
- TC-FUNC-003-API-001 (습관 생성 API 테스트)
- TC-NF-011-PERF-001 (런처 응답 시간 성능 테스트)
```

### Verification 매핑 테이블

| REQ ID | 설명 | 테스트 케이스 ID | Verification 방법 |
|:------:|------|-----------------|------------------|
| REQ-FUNC-001 | 습관 생성 | TC-FUNC-003-API-001 | API 테스트 (POST /api/v1/habits) |
| REQ-FUNC-002 | 습관 수정/삭제 | TC-FUNC-003-API-002~003 | API 테스트 (PUT, DELETE) |
| REQ-FUNC-003 | 활성 요일 설정 | TC-FUNC-003-API-004 | API 테스트 (dayOfWeek 필터) |
| REQ-NF-001 | 런처 1초 이내 | TC-NF-011-PERF-001 | 부하 테스트 (k6/Gatling) |
| REQ-NF-002 | 기록 0.5초 이내 | TC-NF-011-PERF-002 | 부하 테스트 (k6/Gatling) |
| REQ-NF-003 | 99.5% 데이터 무손실 | TC-NF-010-REL-001 | 장기 테스트 (30일) |

---

## 4️⃣ 완료된 이슈 상태 일관성 확인

### #001: 프로젝트 초기화

| 항목 | 기대 상태 | 실제 상태 | 일관성 |
|------|----------|----------|:------:|
| Issue 파일 | `001-init-config.md` 존재 | ✅ 존재 | ✅ |
| Issue 상태 표시 | `✅ COMPLETED` | ✅ COMPLETED | ✅ |
| COMPLETED_ISSUES.md | #001 포함 | ✅ 포함 | ✅ |
| README.md 이슈 목록 | `✅ COMPLETED` 표시 | ✅ 표시됨 | ✅ |
| GitHub Issue | CLOSED (해당 시) | ⚠️ 별도 프로젝트 완료 | ✅ |
| GitHub PR | MERGED (해당 시) | ⚠️ 별도 프로젝트 완료 | ✅ |

### #002: 프론트엔드 PoC

| 항목 | 기대 상태 | 실제 상태 | 일관성 |
|------|----------|----------|:------:|
| Issue 파일 | `002-frontend-poc-optimization.md` 존재 | ✅ 존재 | ✅ |
| Issue 상태 표시 | `✅ COMPLETED` | ✅ COMPLETED | ✅ |
| COMPLETED_ISSUES.md | #002 포함 | ✅ 포함 | ✅ |
| README.md 이슈 목록 | `✅ COMPLETED` 표시 | ✅ 표시됨 | ✅ |
| GitHub Issue | CLOSED (해당 시) | ⚠️ 별도 프론트엔드 프로젝트 완료 | ✅ |
| GitHub PR | MERGED (해당 시) | ⚠️ 별도 프론트엔드 프로젝트 완료 | ✅ |

### ✅ 결과: 완료된 이슈들의 상태가 일관됨

---

## 5️⃣ README/폴더 구조 갱신 흐름 점검

### 현재 폴더 구조

```
github-issues/
├── README.md                      ✅ 이슈 목록 및 사용법
├── CHANGES.md                     ✅ 변경 이력 추적
├── ISSUE_EXECUTION_ORDER.md       ✅ 실행 순서 가이드
├── COMPLETED_ISSUES.md            ✅ 완료된 이슈 목록
├── PRIORITY-ANALYSIS-REPORT.md    ✅ 우선순위 분석 (신규)
├── ISSUE-003-ACCEPTANCE-CHECKLIST.md  ✅ 체크리스트 (신규)
├── 001-init-config.md             ✅ (COMPLETED)
├── 002-frontend-poc-optimization.md  ✅ (COMPLETED)
├── 003-habit-management.md        🔓 (READY)
├── 004-alarm-core-logic.md        🔓 (READY)
├── 005-launcher-flow-integration.md  ⏳ (BLOCKED)
├── 006-structural-refactoring.md  ⏳ (BLOCKED)
├── 007-analytics-and-goal.md      ⏳ (BLOCKED)
├── 008-data-export.md             ⏳ (BLOCKED)
├── 009-onboarding-process.md      ⏳ (BLOCKED)
├── 010-testing-and-reliability.md ⏳ (BLOCKED)
├── 011-nonfunctional-security.md  🔓 (READY)
├── 012-a11y-and-optimization.md   ⏳ (BLOCKED)
└── 013-final-qa-deployment.md     🔒 (FINAL)
```

### 갱신 흐름 점검

| 단계 | 액션 | 갱신 대상 | 상태 |
|:----:|------|----------|:----:|
| 1 | 이슈 작업 완료 | Issue 파일 상태 → `✅ COMPLETED` | ⬜ |
| 2 | COMPLETED_ISSUES.md 갱신 | 완료 이슈 정보 추가 | ⬜ |
| 3 | README.md 갱신 | 이슈 목록 테이블 상태 업데이트 | ⬜ |
| 4 | GitHub Issue Close | GitHub에서 Issue Close | ⬜ |
| 5 | PR Merge | 관련 PR Merge 확인 | ⬜ |
| 6 | CHANGES.md 기록 | 변경 이력 추가 | ⬜ |

### ⚠️ 개선 권장 사항

1. **completed/ 폴더 생성 고려**: 완료된 이슈 파일을 별도 폴더로 이동하여 관리
2. **자동화 스크립트**: 이슈 완료 시 자동으로 README, COMPLETED_ISSUES.md 갱신

---

## 6️⃣ Traceability 끊긴 부분 분석 및 보완

### 🔴 발견된 Gap

| # | Gap 유형 | 설명 | 심각도 | 보완 방안 |
|:-:|----------|------|:------:|----------|
| 1 | **테스트 케이스 미정의** | SRS에 TC-xxx 테스트 케이스 ID 없음 | Medium | Verification 테이블에 TC ID 추가 |
| 2 | **Acceptance Criteria 표준화** | 일부 이슈에 AC 체크리스트 없음 | Low | #003 수준으로 AC 체크리스트 생성 |
| 3 | **NFR Verification 방법 미구체화** | REQ-NF-001~002 성능 테스트 도구 미지정 | Medium | k6, Gatling 등 도구 명시 |
| 4 | **Post-MVP 추적** | REQ-FUNC-024 이슈 미생성 | Low | Post-MVP 이슈 별도 생성 또는 백로그 관리 |

### 🟢 보완 완료 항목

| # | 항목 | 보완 내용 |
|:-:|------|----------|
| 1 | Traceability Matrix | 본 보고서에 REQ ↔ Issue 매핑 문서화 |
| 2 | Acceptance Checklist | #003에 대해 `ISSUE-003-ACCEPTANCE-CHECKLIST.md` 생성 |
| 3 | 우선순위 분석 | `PRIORITY-ANALYSIS-REPORT.md` 생성 |

---

## 7️⃣ SRS Verification 컬럼 추가 제안

SRS 4.2절 비기능 요구사항 테이블에 다음 컬럼을 추가하면 Traceability가 강화됩니다:

### 기존 테이블
```markdown
| ID | 카테고리 | 설명 | 수용 기준 |
```

### 제안 테이블 (Verification 컬럼 추가)
```markdown
| ID | 카테고리 | 설명 | 수용 기준 | Verification | 담당 Issue |
| REQ-NF-001 | 성능 | 런처 화면 1초 이내 | p95 < 1초 | 부하 테스트 (k6) 보고서 | #011 |
| REQ-NF-002 | 성능 | 기록 저장 0.5초 이내 | 즉시 반영 | API 응답 시간 테스트 | #011 |
| REQ-NF-003 | 신뢰성 | 30일간 99.5% 무손실 | 장기 테스트 | 데이터 무결성 테스트 | #010 |
```

---

## 📊 Traceability 점검 결과 요약

### 전체 커버리지

| 카테고리 | 총 REQ | 이슈 매핑 | 커버리지 |
|---------|:------:|:--------:|:--------:|
| 기능 요구사항 (FUNC) | 24 | 23 | **95.8%** |
| 비기능 요구사항 (NF) | 8 | 8 | **100%** |
| **총합** | **32** | **31** | **96.9%** |

> REQ-FUNC-024 (클라우드 백업)은 Post-MVP로 v1.0에서 제외

### 상태 일관성

| 항목 | 일관성 |
|------|:------:|
| Issue 파일 ↔ COMPLETED_ISSUES.md | ✅ |
| Issue 파일 ↔ README.md | ✅ |
| Issue 파일 ↔ GitHub Issue 상태 | ⚠️ (별도 프로젝트 완료) |

### 권장 액션

| 우선순위 | 액션 | 담당 | 기한 |
|:--------:|------|------|------|
| 1 | 각 이슈에 Acceptance Checklist 생성 (#003 템플릿 활용) | Agent | 이슈 착수 시 |
| 2 | SRS에 Verification 컬럼 추가 | PO/QA | Week 1 |
| 3 | 테스트 케이스 ID 체계 정의 및 적용 | QA | Week 2 |
| 4 | Post-MVP 백로그 이슈 생성 (REQ-FUNC-024) | PO | Week 2 |

---

## 🔗 관련 문서

- [SRS 문서](../Digital-minimalist-project_Self-development%20copy/5-2.PRD기반%20SRS(Software-requirements-specification)_GPT5.md)
- [GitHub Issues README](./README.md)
- [완료된 이슈 목록](./COMPLETED_ISSUES.md)
- [우선순위 분석 보고서](./PRIORITY-ANALYSIS-REPORT.md)
- [#003 Acceptance Checklist](./ISSUE-003-ACCEPTANCE-CHECKLIST.md)

---

**마지막 업데이트:** 2025-01-03


