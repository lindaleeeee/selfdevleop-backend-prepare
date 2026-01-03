# GitHub Issues 문서

> **목적:** Focus Habit Launcher Backend 프로젝트의 개발 작업을 GitHub Issues로 관리하기 위한 문서 모음

---

## 📁 구조

```
github-issues/
├── README.md (본 파일)
├── CHANGES.md (이슈 발행 변경사항 추적)
├── ISSUE_EXECUTION_ORDER.md (이슈 수행 순서 및 병렬 개발 가이드)
├── COMPLETED_ISSUES.md (완료된 이슈 목록)
├── 001-init-config.md
├── 002-frontend-poc-optimization.md
├── 003-habit-management.md
├── 004-alarm-core-logic.md
├── 005-launcher-flow-integration.md
├── 006-structural-refactoring.md
├── 007-analytics-and-goal.md
├── 008-data-export.md
├── 009-onboarding-process.md
├── 010-testing-and-reliability.md
├── 011-nonfunctional-security.md
├── 012-a11y-and-optimization.md
└── 013-final-qa-deployment.md
```

---

## 📋 이슈 목록

### Functional Requirements (기능 요구사항)

| Issue # | 제목 | Epic | Priority | Dependencies | Status |
|---------|------|------|----------|--------------|--------|
| #001 | 프로젝트 초기화 및 기본 환경 설정 | EPIC-0 | P0 | None | ✅ **COMPLETED** |
| #002 | 프론트엔드 PoC UI 구현 및 성능 최적화 | EPIC-1 | P1 | #001 | ✅ **COMPLETED** |
| #003 | 습관 관리 데이터 및 로직 구현 | EPIC-2 | P0 | #001 |
| #004 | 알람 코어 로직 및 스케줄러 | EPIC-3 | P0 | #001 |
| #005 | 런처 플로우 및 데이터 연동 | EPIC-4 | P0 | #003, #004 |
| #006 | 구조적 리팩토링 및 에러 처리 | Refactoring | P2 | #003, #004, #005 |
| #007 | 통계 및 목표 관리 | EPIC-5 | P1 | #005 |
| #008 | 데이터 내보내기 및 공유 | EPIC-6 | P2 | #005 |
| #009 | 온보딩 및 초기 설정 | EPIC-7 | P2 | #003, #004 |

### Non-Functional Requirements (비기능 요구사항)

| Issue # | 제목 | Epic | Priority | Dependencies |
|---------|------|------|----------|--------------|
| #010 | 테스트 코드 작성 및 안정성 확보 | QA & Reliability | P1 | #003, #004, #005, #007 |
| #011 | 비기능 요구사항 및 보안 점검 | Non-Functional | P1 | #001, #003, #004, #005 |
| #012 | 접근성 개선 및 최적화 | Accessibility | P2 | #001, #003, #004, #005 |
| #013 | 최종 QA 및 배포 준비 | Deployment | P0 | All |

---

## 🚀 사용 방법

### 1. GitHub Issues 생성

각 `.md` 파일의 내용을 GitHub Issues로 생성합니다:

**⚠️ 중요:** 완료된 이슈(#001, #002)는 GitHub에 발행하지 않습니다. 이들은 별도 프로젝트에서 완료되었습니다.

1. GitHub 저장소의 Issues 탭으로 이동
2. "New Issue" 클릭
3. 해당 이슈 파일의 내용을 복사하여 붙여넣기
4. Labels, Assignees, Milestone 설정
5. "Submit new issue" 클릭

**제외할 이슈:**
- ✅ #001: Init Config (EPIC-0) - 별도 프로젝트에서 완료
- ✅ #002: Frontend PoC - 별도 프론트엔드 프로젝트에서 완료

### 2. 이슈 번호 매핑

- 파일명의 번호 (#001, #002 등)를 GitHub Issue 번호로 사용
- 의존성은 "Dependencies" 섹션에 명시된 이슈 번호를 참조

### 3. 진행 상황 추적

- [ISSUE_EXECUTION_ORDER.md](ISSUE_EXECUTION_ORDER.md)를 참조하여 작업 순서 확인
- 각 이슈의 체크리스트를 업데이트하여 진행 상황 추적

---

## 📊 의존관계 요약

### Critical Path (반드시 순차 진행)
```
#001 → #003, #004 → #005 → #007, #008 → #013
```

### 완료된 작업
- ✅ **#001: Init Config** - 별도 프로젝트에서 완료됨 (EPIC-0)
- ✅ **#002: Frontend PoC** - 별도 프론트엔드 프로젝트에서 완료됨

### 병렬 개발 가능 영역
- **#003과 #004**: 완전히 독립적, 동시 진행 가능
- **#007과 #008**: 서로 독립적, 동시 진행 가능
- **#006, #010, #011, #012**: 기능 개발과 병렬 진행 가능

---

## 🔗 관련 문서

- [이슈 발행 변경사항 추적](CHANGES.md) - GitHub 이슈 발행 현황 및 변경 이력
- [이슈 수행 순서 가이드](ISSUE_EXECUTION_ORDER.md)
- [완료된 이슈 목록](COMPLETED_ISSUES.md)
- [Task 추출 결과](Tasks%20copy/6.%20Task%EC%B6%94%EC%B6%9C%EA%B2%B0%EA%B3%BC.md)
- [MVP 개발 Task 추출 통합 작업계획](../Digital-minimalist-project_Self-development%20copy/6-1.MVP%EA%B0%9C%EB%B0%9C-Task%EC%B6%94%EC%B6%9C%ED%86%B5%ED%95%A9%EC%9E%91%EC%97%85%EA%B3%84%ED%9A%8D.md)

---

## 📝 이슈 템플릿 구조

각 이슈 파일은 다음 구조를 따릅니다:

```markdown
# #XXX: [제목]

**Epic:** [Epic 이름]
**Type:** [Functional/Non-Functional]
**Priority:** [P0/P1/P2]
**Labels:** [라벨 목록]
**Related REQ:** [관련 요구사항]
**Dependencies:** [의존 이슈]
**Blocks:** [차단하는 이슈]

## 📋 Description
[설명]

## 🎯 Goals
[목표]

## ✅ Tasks
[세부 작업 목록]

## 📝 Acceptance Criteria
[완료 기준]

## 🔗 Related Documentation
[관련 문서 링크]

## 📌 Notes
[참고사항]
```

---

## ✅ 완료된 이슈

- **#001: Init Config** - 별도 프로젝트에서 완료됨 (EPIC-0)
- **#002: Frontend PoC** - 별도 프론트엔드 프로젝트에서 완료됨

자세한 내용은 [COMPLETED_ISSUES.md](COMPLETED_ISSUES.md)를 참조하세요.

---

**마지막 업데이트:** 2025-01-15

