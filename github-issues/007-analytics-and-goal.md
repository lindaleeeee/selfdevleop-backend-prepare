# #007: 통계 및 목표 관리

**Epic:** EPIC-5 (ANALYTICS_GOAL)  
**Type:** Functional  
**Priority:** P1 (High)  
**Labels:** `epic:analytics`, `type:backend`, `type:database`  
**Related REQ:** REQ-FUNC-019, REQ-FUNC-020, REQ-FUNC-021, REQ-FUNC-022  
**Dependencies:** #005  
**Blocks:** None

---

## 📋 Description

축적된 습관 기록 데이터를 분석하여 통계를 제공하고, 사용자의 목표 달성 현황을 관리합니다.

## 🎯 Goals

- Goal Entity 및 Repository 구현
- 통계 집계 로직 구현
- 목표 달성률 계산 로직 구현
- 통계 및 목표 관리 API 구현

## ✅ Tasks

### TASK-GOAL-DB-01: Goal Entity
- [ ] `Goal` JPA Entity 설계 및 구현
  - [ ] 필드: `id`, `habitId`, `periodType` (Day/Week/Month/Year), `targetValue`, `createdAt`, `updatedAt`
  - [ ] `@ManyToOne` 관계 설정 (Habit)
  - [ ] Enum 타입 정의 (`PeriodType`)
- [ ] `GoalRepository` 인터페이스 생성
- [ ] 습관별 목표 조회 쿼리 구현
- [ ] 기간별 목표 조회 쿼리 구현

### TASK-STATS-SERVICE-01: Statistics Service
- [ ] `StatisticsService` 클래스 구현
- [ ] 일/주/월/년 단위 수행 횟수 집계 로직 구현 (REQ-FUNC-019)
- [ ] 일/주/월/년 단위 수행 시간 집계 로직 구현
- [ ] SQL 쿼리 최적화 (GROUP BY 등 활용)
- [ ] 목표 달성률 계산 로직 구현 (REQ-FUNC-021)
  - [ ] 실제 값 대비 목표 달성률(%) 계산
- [ ] 습관/카테고리별 필터링 로직 구현 (REQ-FUNC-022)

### TASK-GOAL-SERVICE-01: Goal Service
- [ ] `GoalService` 클래스 구현
- [ ] 목표 생성 로직 구현 (REQ-FUNC-020)
- [ ] 목표 수정 로직 구현
- [ ] 목표 삭제 로직 구현
- [ ] 목표 유효성 검사

### TASK-STATS-CONTROLLER-01: Statistics Controller
- [ ] `StatisticsController` 클래스 구현
- [ ] `GET /api/v1/statistics` - 통계 데이터 조회
  - [ ] 쿼리 파라미터: `period` (day/week/month/year), `habitId` (optional)
- [ ] `GET /api/v1/goals` - 목표 목록 조회
- [ ] `POST /api/v1/goals` - 목표 생성
- [ ] `PUT /api/v1/goals/{id}` - 목표 수정
- [ ] `DELETE /api/v1/goals/{id}` - 목표 삭제
- [ ] Request/Response DTO 구현

### TASK-STATS-TEST-01: Statistics Tests
- [ ] `StatisticsService` 단위 테스트 작성
- [ ] `GoalService` 단위 테스트 작성
- [ ] 통계 집계 로직 테스트
- [ ] 목표 달성률 계산 로직 테스트

## 📝 Acceptance Criteria

- [ ] 통계 데이터 조회 API가 정상 작동함
- [ ] 목표 생성/수정/삭제 API가 정상 작동함
- [ ] 목표 달성률 계산이 정확함
- [ ] 기간별 집계가 정확함
- [ ] 필터링 기능이 정상 작동함
- [ ] 단위 테스트 커버리지 80% 이상
- [ ] API 문서(Swagger)에 정상 반영됨

## 🔗 Related Documentation

- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 및 데이터베이스 규칙](.cursor/rules/402-jpa-database-rules.mdc)
- [Task 문서](Tasks%20copy/Functional/007_Analytics_and_Goal.md)

## 📌 Notes

- 이 Task는 #005 완료 후 시작해야 합니다 (LogEntry 데이터 필요).
- 통계 집계 쿼리는 성능을 고려하여 최적화해야 합니다.
- 대량 데이터 처리 시 페이징을 고려합니다.

