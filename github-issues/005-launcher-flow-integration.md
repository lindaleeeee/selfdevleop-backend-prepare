# #005: 런처 플로우 및 데이터 연동

**Epic:** EPIC-4 (LAUNCHER_FLOW)  
**Type:** Functional  
**Priority:** P0 (Critical)  
**Labels:** `epic:launcher`, `type:backend`, `type:integration`  
**Related REQ:** REQ-FUNC-012, REQ-FUNC-013, REQ-FUNC-014, REQ-FUNC-015, REQ-FUNC-016, REQ-FUNC-017, REQ-FUNC-018  
**Dependencies:** #002 ✅ (완료), #003, #004  
**Parallelizable With:** #006, #010, #012  
**Blocks:** #007, #008

---

## 📋 Description

알람이 울렸을 때 런처 플로우를 지원하는 API를 구현하고, 실제 데이터(DB)와 연동하여 기록을 저장합니다.

**참고:** 프론트엔드 PoC (#002)가 별도 프로젝트에서 완료되었으므로, 이 작업에서는 백엔드 API를 구현하여 프론트엔드와 연동할 수 있도록 합니다.

## 📌 Scope / Out of Scope

### In Scope
- LogEntry Entity 및 Repository 구현
- 세션 로깅 API (텍스트 메모, 음성 경로, 소요 시간)
- 당일 습관 목록 조회 API (완료/미완료 상태 포함)
- 명언 데이터 관리 및 랜덤 조회 API
- 완료 습관 계산 로직

### Out of Scope
- 음성 인식 처리 (모바일 앱에서 처리)
- 통계 및 분석 (#007에서 처리)
- 데이터 내보내기 (#008에서 처리)
- 프론트엔드 UI 구현 (별도 프로젝트에서 완료)

## 🎯 Goals

- LogEntry Entity 및 Repository 구현
- 세션 로깅 API 구현
- 명언 데이터 관리 API 구현
- 런처 플로우 관련 API 구현

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

**Validation:**
- Jakarta Bean Validation (`@Valid`, `@NotNull`, etc.)

**Testing:**
- JUnit 5
- Mockito
- Spring Boot Test

## ✅ Tasks

### TASK-LOG-DB-01: Log Entity
- [ ] `LogEntry` JPA Entity 설계 및 구현
  - [ ] 필드: `id`, `habitId`, `alarmId`, `timestamp`, `textNote`, `voicePath`, `duration`
  - [ ] `@ManyToOne` 관계 설정 (Habit, Alarm)
  - [ ] `@CreatedDate` 적용
- [ ] `LogEntryRepository` 인터페이스 생성
- [ ] 습관별 로그 조회 쿼리 구현
- [ ] 날짜별 로그 조회 쿼리 구현

### TASK-QUOTE-DATA-01: Quote Data
- [ ] `Quote` JPA Entity 설계 및 구현
  - [ ] 필드: `id`, `text`, `language`, `theme`, `createdAt`
- [ ] `QuoteRepository` 인터페이스 생성
- [ ] 로컬 명언 데이터셋 구축 (최소 30개)
- [ ] 랜덤 명언 조회 쿼리 구현

### TASK-LOG-SERVICE-01: Log Service
- [ ] `LogEntryService` 클래스 구현
- [ ] 세션 로그 생성 로직 구현
  - [ ] 텍스트 메모 저장 (REQ-FUNC-016)
  - [ ] 음성 메모 경로 저장 (REQ-FUNC-017)
  - [ ] 소요 시간 기록
- [ ] 습관별 로그 조회 로직 구현
- [ ] 날짜별 로그 조회 로직 구현
- [ ] 당일 완료 습관 계산 로직 구현 (REQ-FUNC-014)

### TASK-LAUNCHER-CONTROLLER-01: Launcher Controller
- [ ] `LauncherController` 클래스 구현
- [ ] `GET /api/v1/launcher/habits` - 당일 습관 목록 조회 (완료/미완료 상태 포함)
- [ ] `POST /api/v1/sessions` - 세션 로그 생성
- [ ] `GET /api/v1/quotes/random` - 랜덤 명언 조회 (REQ-FUNC-018)
- [ ] Request/Response DTO 구현

### TASK-LAUNCHER-TEST-01: Launcher Tests
- [ ] `LogEntryService` 단위 테스트 작성
- [ ] `LauncherController` API 테스트 작성
- [ ] 완료 습관 계산 로직 테스트

## 📝 Acceptance Criteria

- [ ] 세션 로그 생성 API가 정상 작동함
- [ ] 당일 습관 목록 조회 API가 정상 작동함 (완료/미완료 상태 포함)
- [ ] 랜덤 명언 조회 API가 정상 작동함
- [ ] 완료 습관 계산 로직이 정확함
- [ ] 단위 테스트 커버리지 80% 이상
- [ ] API 문서(Swagger)에 정상 반영됨

## 🔗 Related Documentation

- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 및 데이터베이스 규칙](.cursor/rules/402-jpa-database-rules.mdc)
- [Task 문서](Tasks%20copy/Functional/005_Launcher_Flow_Integration.md)

## 📡 API Specification

### GET /api/v1/launcher/habits - 당일 습관 목록 조회

**Query Parameters:**
- 없음 (현재 날짜 기준으로 자동 계산)

**Response Body 예시 (200 OK):**
```json
{
  "content": [
    {
      "id": 1,
      "name": "명상",
      "icon": "🧘",
      "color": "#4A90E2",
      "activeDays": ["MONDAY", "WEDNESDAY", "FRIDAY"],
      "defaultDuration": 30,
      "isCompleted": false
    },
    {
      "id": 2,
      "name": "독서",
      "icon": "📚",
      "color": "#FF6B6B",
      "activeDays": ["MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY"],
      "defaultDuration": 60,
      "isCompleted": true
    }
  ],
  "page": {
    "number": 0,
    "size": 20,
    "totalElements": 2,
    "totalPages": 1
  }
}
```

### POST /api/v1/sessions - 세션 로그 생성

**Request Body 예시:**
```json
{
  "habitId": 1,
  "alarmId": 5,
  "timestamp": "2025-01-15T09:00:00",
  "textNote": "오늘도 좋은 하루 시작!",
  "voicePath": "/uploads/voice/2025/01/15/voice_001.mp3",
  "duration": 1800
}
```

**Response Body 예시 (201 Created):**
```json
{
  "id": 1,
  "habitId": 1,
  "alarmId": 5,
  "timestamp": "2025-01-15T09:00:00",
  "textNote": "오늘도 좋은 하루 시작!",
  "voicePath": "/uploads/voice/2025/01/15/voice_001.mp3",
  "duration": 1800,
  "createdAt": "2025-01-15T09:30:00"
}
```

### GET /api/v1/quotes/random - 랜덤 명언 조회

**Query Parameters:**
- `theme` (String, 선택): 테마 필터 (예: "motivation", "focus")

**Response Body 예시 (200 OK):**
```json
{
  "id": 15,
  "text": "성공은 준비된 자에게 찾아온다.",
  "author": "Unknown",
  "theme": "motivation",
  "language": "ko"
}
```

## 🔄 Logic Steps (런타임 처리 순서)

### GET /api/v1/launcher/habits - 당일 습관 목록 조회

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@GetMapping("/launcher/habits")` 핸들러 메서드 호출

2. **Service 메서드 호출** (`LauncherService.getTodayHabits()`)

3. **읽기 전용 트랜잭션 시작** (`@Transactional(readOnly = true)`)

4. **현재 날짜 및 요일 계산** (Service Layer)
   - `LocalDate.now()` 실행
   - `DayOfWeek.from(currentDate)` 실행

5. **당일 활성 습관 조회** (Repository Layer)
   - `habitRepository.findByActiveDaysContaining(todayDayOfWeek)` 실행
   - `isArchived = false` 조건으로 필터링

6. **완료 습관 계산** (Service Layer)
   - 각 습관에 대해 `logEntryRepository.existsByHabitIdAndTimestampBetween(habitId, startOfDay, endOfDay)` 실행
   - `isCompleted` 필드 설정

7. **Entity → DTO 변환** (Service Layer)
   - `HabitResponse.from(habit)` 호출
   - `isCompleted` 필드 추가

8. **읽기 전용 트랜잭션 종료** (`@Transactional(readOnly = true)`)

9. **HTTP Response 생성** (Controller)
   - `200 OK` 상태 코드와 함께 응답 반환

### POST /api/v1/sessions - 세션 로그 생성

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@PostMapping("/sessions")` 핸들러 메서드 호출
   - Request Body를 `CreateSessionRequest` DTO로 역직렬화

2. **Request Validation** (Controller Layer)
   - `@Valid` 어노테이션으로 DTO 검증
   - `habitId` 필수 체크, `timestamp` 형식 검증
   - 실패 시: `400 Bad Request` 반환

3. **Service 메서드 호출** (`LogEntryService.create(request)`)

4. **트랜잭션 시작** (`@Transactional`)

5. **관련 리소스 존재 확인** (Service Layer)
   - `habitRepository.findById(request.getHabitId())` 실행
   - 없으면: `HabitNotFoundException` throw → `404 Not Found` 반환
   - `alarmId`가 있으면 `alarmRepository.findById(request.getAlarmId())` 체크

6. **Entity 생성** (Service Layer)
   - `LogEntry.builder()` 사용하여 Entity 생성
   - `habit`, `alarm`, `timestamp`, `textNote`, `voicePath`, `duration` 설정

7. **데이터베이스 저장** (Repository Layer)
   - `logEntryRepository.save(logEntry)` 실행
   - JPA가 INSERT 쿼리 생성 및 실행

8. **트랜잭션 커밋** (`@Transactional`)

9. **Entity → DTO 변환 및 응답** (Service → Controller)
   - `LogEntryResponse.from(savedLogEntry)` 호출
   - `201 Created` 상태 코드와 함께 응답 반환

### GET /api/v1/quotes/random - 랜덤 명언 조회

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@GetMapping("/quotes/random")` 핸들러 메서드 호출
   - Query Parameter `theme` 추출 (선택)

2. **Service 메서드 호출** (`QuoteService.getRandomQuote(theme)`)

3. **읽기 전용 트랜잭션 시작** (`@Transactional(readOnly = true)`)

4. **명언 조회** (Repository Layer)
   - `theme`가 있으면: `quoteRepository.findRandomByTheme(theme)` 실행
   - `theme`가 없으면: `quoteRepository.findRandom()` 실행
   - SQL: `SELECT * FROM quotes WHERE theme = ? ORDER BY RAND() LIMIT 1`

5. **데이터베이스 쿼리 실행** (Database)
   - MySQL/H2에서 쿼리 실행
   - 결과 반환

6. **Entity → DTO 변환** (Service Layer)
   - `QuoteResponse.from(quote)` 호출

7. **읽기 전용 트랜잭션 종료** (`@Transactional(readOnly = true)`)

8. **HTTP Response 생성** (Controller)
   - `200 OK` 상태 코드와 함께 응답 반환

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **중 (Medium)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 3-4일 내에 독립적으로 완료할 수 있는 작업 단위입니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-LOG-DB-01** | 하 (Low) | 2-3시간 | LogEntry Entity, Repository 인터페이스 | 관계 매핑 (@ManyToOne) |
| **TASK-QUOTE-DATA-01** | 하 (Low) | 2-3시간 | Quote Entity, 데이터 시드 | 초기 데이터 준비 |
| **TASK-LOG-SERVICE-01** | 중 (Medium) | 5-6시간 | 세션 로깅 로직, 완료 습관 계산 | 날짜 계산, 쿼리 최적화 |
| **TASK-LAUNCHER-CONTROLLER-01** | 중 (Medium) | 3-4시간 | REST API 엔드포인트, DTO 매핑 | 3개 엔드포인트 구현 |
| **TASK-LAUNCHER-TEST-01** | 중 (Medium) | 4-6시간 | 단위/통합/API 테스트 작성 | 날짜 로직 테스트 |

**총 예상 시간: 16-22시간 (3-4일)**

### 작업량 분해

**Day 1 (6-8시간):**
- LogEntry 및 Quote Entity 구현 (3시간)
- Repository 인터페이스 구현 (2시간)
- 데이터 시드 스크립트 작성 (2-3시간)

**Day 2 (6-8시간):**
- LogEntryService 구현 (4시간)
- 완료 습관 계산 로직 (2-3시간)
- QuoteService 구현 (1시간)

**Day 3 (4-6시간):**
- LauncherController 구현 (3-4시간)
- DTO 구현 (1-2시간)

**Day 4 (2-4시간):**
- 테스트 작성 (4-6시간)
- 버그 수정 및 리팩토링 (2시간)

## 📌 Notes

- 이 Task는 #003과 #004 완료 후 시작해야 합니다.
- 프론트엔드 PoC (#002)가 완료되었으므로, 백엔드 API 구현 후 프론트엔드와 연동 테스트를 진행합니다.
- 음성 인식은 모바일 앱에서 처리되며, 백엔드는 음성 파일 경로만 저장합니다.
- 명언 데이터는 초기 데이터로 DB에 시드됩니다.

