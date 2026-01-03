# GitHub Issues 발행 변경사항 추적

> **목적:** GitHub Issues 발행 내역 및 변경사항을 추적하고 관리하기 위한 문서

---

## 📊 이슈 발행 현황

### 발행된 이슈 목록

| Issue # | GitHub Issue # | 제목 | 상태 | 발행일 | 최종 업데이트 | 링크 |
|---------|----------------|------|------|--------|--------------|------|
| #000 | #14 | 이슈별 작업 브랜치 생성 및 초기 설정 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/14) |
| #003 | #3 | 습관 관리 데이터 및 로직 구현 | OPEN | 2025-12-27 | 2026-01-02 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/3) |
| #004 | #4 | 알람 코어 로직 및 스케줄러 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/4) |
| #005 | #5 | 런처 플로우 및 데이터 연동 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/5) |
| #006 | #6 | 구조적 리팩토링 및 에러 처리 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/6) |
| #007 | #7 | 통계 및 목표 관리 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/7) |
| #008 | #8 | 데이터 내보내기 및 공유 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/8) |
| #009 | #9 | 온보딩 및 초기 설정 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/9) |
| #010 | #10 | 테스트 코드 작성 및 안정성 확보 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/10) |
| #011 | #11 | 비기능 요구사항 및 보안 점검 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/11) |
| #012 | #12 | 접근성 개선 및 최적화 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/12) |
| #013 | #13 | 최종 QA 및 배포 준비 | OPEN | 2025-12-27 | 2025-12-27 | [보기](https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues/13) |

### 미발행 이슈

| Issue # | 제목 | 상태 | 비고 |
|---------|------|------|------|
| #001 | 프로젝트 초기화 및 기본 환경 설정 | COMPLETED | 별도 프로젝트에서 완료됨 (발행 불필요) |
| #002 | 프론트엔드 PoC UI 구현 및 성능 최적화 | COMPLETED | 별도 프론트엔드 프로젝트에서 완료됨 (발행 불필요) |

---

## 📝 변경 이력

### 2026-01-15

**작업 내용:**
- CHANGES.md 파일 생성
- GitHub 이슈 발행 현황 확인 및 문서화
- 이슈 발행 상태 추적 시스템 구축

**발행된 이슈:**
- 총 12개 이슈 발행 완료 (#000, #003~#013)
- 모든 이슈 상태: OPEN

**참고사항:**
- #001, #002는 별도 프로젝트에서 완료되어 GitHub에 발행하지 않음
- #003 이슈가 2026-01-02에 최종 업데이트됨 (가장 최근 활동)

---

## 🔗 관련 링크

- **GitHub 저장소:** https://github.com/lindaleeeee/selfdevleop-backend-prepare
- **이슈 목록:** https://github.com/lindaleeeee/selfdevleop-backend-prepare/issues
- **이슈 실행 순서:** [ISSUE_EXECUTION_ORDER.md](ISSUE_EXECUTION_ORDER.md)
- **완료된 이슈:** [COMPLETED_ISSUES.md](COMPLETED_ISSUES.md)

---

## 📌 사용 방법

### 이슈 발행 확인

```bash
# 모든 이슈 목록 확인
gh issue list --limit 50

# 특정 이슈 상세 확인
gh issue view <issue-number>

# 이슈 상태 업데이트
gh issue edit <issue-number> --state closed
```

### 이 파일 업데이트

1. 새로운 이슈가 발행되면 "발행된 이슈 목록" 섹션에 추가
2. 이슈 상태가 변경되면 해당 행의 "상태" 및 "최종 업데이트" 날짜 수정
3. 변경 이력 섹션에 변경사항 기록

---

**마지막 업데이트:** 2026-01-15

