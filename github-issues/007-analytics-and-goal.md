# #007: 통계 및 목표 관리

**Epic:** EPIC-5 (ANALYTICS_GOAL)  
**Type:** Functional  
**Priority:** P1 (High)  
**Labels:** `epic:analytics`, `type:backend`, `type:database`  
**Related REQ:** REQ-FUNC-019, REQ-FUNC-020, REQ-FUNC-021, REQ-FUNC-022  
**Dependencies:** #005  
**Parallelizable With:** #008, #006, #010  
**Blocks:** None

---

## 📋 Description

축적된 습관 기록 데이터를 분석하여 통계를 제공하고, 사용자의 목표 달성 현황을 관리합니다.

## 📌 Scope / Out of Scope

### In Scope
- Goal Entity 및 Repository 구현
- 통계 집계 로직 (일/주/월별)
- 목표 설정 및 달성 현황 관리 API
- 기본적인 통계 시각화 데이터 제공

### Out of Scope
- 고급 통계 분석 및 머신러닝 (#007 이후 확장)
- 복잡한 차트 렌더링 (프론트엔드에서 처리)
- 데이터 내보내기 (#008에서 처리)

## 🎯 Goals

- Goal Entity 및 Repository 구현
- 통계 집계 로직 구현
- 목표 달성률 계산 로직 구현
- 통계 및 목표 관리 API 구현

## 🛠️ Technical Stack

**Backend Core:**
- Java 21 LTS
- Spring Boot 4.0.1
- Spring Data JPA / Hibernate 7.2.0
- Gradle 9.2.1

**Database:**
- MySQL 8.x (Production)
- H2 Database (Development/Testing)

**API:**
- RESTful API (JSON)
- OpenAPI 3.0 (Swagger/SpringDoc)

**Testing:**
- JUnit 5
- Mockito
- Spring Boot Test

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

## 📡 API Specification

### GET /api/v1/statistics - 통계 데이터 조회

**Query Parameters:**
- `period` (String, 필수): 기간 타입 (`day`, `week`, `month`, `year`)
- `habitId` (Long, 선택): 습관 ID 필터

**Response Body 예시 (200 OK):**
```json
{
  "period": "week",
  "startDate": "2025-01-13",
  "endDate": "2025-01-19",
  "totalSessions": 12,
  "totalDuration": 3600,
  "habits": [
    {
      "habitId": 1,
      "habitName": "명상",
      "sessionCount": 5,
      "totalDuration": 1500,
      "averageDuration": 300
    }
  ]
}
```

### POST /api/v1/goals - 목표 생성

**Request Body 예시:**
```json
{
  "habitId": 1,
  "periodType": "WEEK",
  "targetValue": 5
}
```

**Response Body 예시 (201 Created):**
```json
{
  "id": 1,
  "habitId": 1,
  "periodType": "WEEK",
  "targetValue": 5,
  "currentValue": 0,
  "achievementRate": 0.0,
  "createdAt": "2025-01-15T10:30:00",
  "updatedAt": "2025-01-15T10:30:00"
}
```

## 🔄 Logic Steps (런타임 처리 순서)

### GET /api/v1/statistics - 통계 데이터 조회

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@GetMapping("/statistics")` 핸들러 메서드 호출
   - Query Parameter `period`, `habitId` 추출

2. **Service 메서드 호출** (`StatisticsService.getStatistics(period, habitId)`)

3. **읽기 전용 트랜잭션 시작** (`@Transactional(readOnly = true)`)

4. **기간 계산** (Service Layer)
   - `period`에 따라 시작일/종료일 계산
   - 예: `week` → 현재 주의 월요일 ~ 일요일

5. **통계 집계 쿼리 실행** (Repository Layer)
   - `logEntryRepository.countByTimestampBetweenAndHabitId(startDate, endDate, habitId)` 실행
   - SQL: `SELECT COUNT(*), SUM(duration) FROM log_entries WHERE timestamp BETWEEN ? AND ? AND habit_id = ?`

6. **데이터베이스 쿼리 실행** (Database)
   - MySQL/H2에서 집계 쿼리 실행
   - 결과 반환

7. **통계 데이터 구성** (Service Layer)
   - 집계 결과를 `StatisticsResponse` DTO로 변환
   - 습관별 통계 계산

8. **읽기 전용 트랜잭션 종료** (`@Transactional(readOnly = true)`)

9. **HTTP Response 생성** (Controller)
   - `200 OK` 상태 코드와 함께 응답 반환

### POST /api/v1/goals - 목표 생성

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@PostMapping("/goals")` 핸들러 메서드 호출
   - Request Body를 `CreateGoalRequest` DTO로 역직렬화

2. **Request Validation** (Controller Layer)
   - `@Valid` 어노테이션으로 DTO 검증
   - `habitId`, `periodType`, `targetValue` 필수 체크

3. **Service 메서드 호출** (`GoalService.create(request)`)

4. **트랜잭션 시작** (`@Transactional`)

5. **관련 리소스 존재 확인** (Service Layer)
   - `habitRepository.findById(request.getHabitId())` 실행
   - 없으면: `HabitNotFoundException` throw → `404 Not Found` 반환

6. **Entity 생성** (Service Layer)
   - `Goal.builder()` 사용하여 Entity 생성
   - `habit`, `periodType`, `targetValue` 설정

7. **데이터베이스 저장** (Repository Layer)
   - `goalRepository.save(goal)` 실행
   - JPA가 INSERT 쿼리 생성 및 실행

8. **트랜잭션 커밋** (`@Transactional`)

9. **Entity → DTO 변환 및 응답** (Service → Controller)
   - `GoalResponse.from(savedGoal)` 호출
   - `201 Created` 상태 코드와 함께 응답 반환

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **중 (Medium)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 3-4일 내에 독립적으로 완료할 수 있는 작업 단위입니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-GOAL-DB-01** | 하 (Low) | 2-3시간 | Goal Entity, Repository 인터페이스 | 관계 매핑 |
| **TASK-STATS-SERVICE-01** | 중 (Medium) | 6-8시간 | 통계 집계 로직, SQL 최적화 | 복잡한 집계 쿼리 |
| **TASK-GOAL-SERVICE-01** | 하 (Low) | 2-3시간 | 목표 CRUD 로직 | 표준 패턴 |
| **TASK-STATS-CONTROLLER-01** | 중 (Medium) | 3-4시간 | REST API 엔드포인트, DTO 매핑 | 5개 엔드포인트 |
| **TASK-STATS-TEST-01** | 중 (Medium) | 4-6시간 | 단위/통합/API 테스트 작성 | 집계 로직 테스트 |

**총 예상 시간: 17-24시간 (3-4일)**

## 📌 Notes

- 이 Task는 #005 완료 후 시작해야 합니다 (LogEntry 데이터 필요).
- 통계 집계 쿼리는 성능을 고려하여 최적화해야 합니다.
- 대량 데이터 처리 시 페이징을 고려합니다.

