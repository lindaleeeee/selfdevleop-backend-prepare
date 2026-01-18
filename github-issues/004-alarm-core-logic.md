# #004: 알람 코어 로직 및 스케줄러

**Epic:** EPIC-3 (ALARM_CORE)  
**Type:** Functional  
**Priority:** P0 (Critical)  
**Labels:** `epic:alarm`, `type:backend`, `type:integration`  
**Related REQ:** REQ-FUNC-004, REQ-FUNC-005, REQ-FUNC-006, REQ-FUNC-008, REQ-FUNC-009  
**Dependencies:** #001 ✅ (완료)  
**Parallelizable With:** #003, #011  
**Blocks:** #005

---

## 📋 Description

알람/타이머 스케줄링 및 OS 알림 시스템 연동 핵심 로직을 구현합니다.

**Note:** 백엔드에서는 알람 스케줄링 로직과 API를 제공하며, 실제 OS 알림은 모바일 앱에서 처리합니다.

## 📌 Scope / Out of Scope

### In Scope
- Alarm Entity 및 Repository 구현
- 알람/타이머 CRUD API (생성, 조회, 수정, 삭제, 토글)
- 알람 스케줄링 로직 (정시 알람, 상대 시간 타이머)
- 알람 유효성 검사 (과거 시간 방지 등)
- 기본적인 단위 테스트 및 통합 테스트

### Out of Scope
- 실제 OS 알림 발송 (모바일 앱에서 처리)
- 알람 울림 후 플로우 처리 (#005에서 처리)
- 알람 히스토리 및 통계 (#007에서 처리)
- 사용자 인증/인가 (별도 이슈에서 처리)

## 🎯 Goals

- Alarm Entity 및 Repository 구현
- 알람/타이머 CRUD API 구현
- 알람 스케줄링 로직 구현
- 알람 상태 관리 로직 구현

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
- Jakarta Bean Validation (`@Valid`, `@NotNull`, `@Min`, `@Max`, etc.)

**Testing:**
- JUnit 5
- Mockito
- Spring Boot Test

## ✅ Tasks

### TASK-ALARM-DB-01: Alarm Entity
- [ ] `Alarm` JPA Entity 설계 및 구현
  - [ ] 필드: `id`, `type` (fixed/relative), `timeOrOffset`, `label`, `isEnabled`, `daysOfWeek`, `createdAt`, `updatedAt`
  - [ ] `@Entity`, `@Table` 어노테이션 적용
  - [ ] Enum 타입 정의 (`AlarmType`, `DayOfWeek` 등)
- [ ] `AlarmRepository` 인터페이스 생성
- [ ] 활성 알람 조회 쿼리 구현
- [ ] 시간대별 알람 조회 쿼리 구현

### TASK-ALARM-SERVICE-01: Alarm Service
- [ ] `AlarmService` 클래스 구현
- [ ] 알람 생성 로직 구현
  - [ ] 정시 알람 생성 (REQ-FUNC-004)
  - [ ] 상대 시간 타이머 생성 (REQ-FUNC-005)
  - [ ] 라벨 설정 (REQ-FUNC-006)
- [ ] 알람 수정 로직 구현
- [ ] 알람 삭제 로직 구현
- [ ] 알람 토글(On/Off) 로직 구현
- [ ] 알람 스케줄링 로직 구현
- [ ] 알람 유효성 검사 (과거 시간 방지 등)

### TASK-ALARM-CONTROLLER-01: Alarm Controller
- [ ] `AlarmController` 클래스 구현
- [ ] `GET /api/v1/alarms` - 알람 목록 조회
- [ ] `GET /api/v1/alarms/{id}` - 알람 상세 조회
- [ ] `POST /api/v1/alarms` - 알람 생성
- [ ] `PUT /api/v1/alarms/{id}` - 알람 수정
- [ ] `PATCH /api/v1/alarms/{id}/toggle` - 알람 토글
- [ ] `DELETE /api/v1/alarms/{id}` - 알람 삭제
- [ ] Request/Response DTO 구현

### TASK-ALARM-TEST-01: Alarm Tests
- [ ] `AlarmService` 단위 테스트 작성
- [ ] `AlarmRepository` 통합 테스트 작성
- [ ] `AlarmController` API 테스트 작성
- [ ] 스케줄링 로직 테스트

## 📝 Acceptance Criteria

- [ ] 정시 알람 생성 API가 정상 작동함
- [ ] 상대 시간 타이머 생성 API가 정상 작동함
- [ ] 알람 토글 API가 정상 작동함
- [ ] 알람 수정/삭제 API가 정상 작동함
- [ ] 알람 유효성 검사가 정상 작동함
- [ ] 단위 테스트 커버리지 80% 이상
- [ ] API 문서(Swagger)에 정상 반영됨

## 🔗 Related Documentation

- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 및 데이터베이스 규칙](.cursor/rules/402-jpa-database-rules.mdc)
- [Task 문서](Tasks%20copy/Functional/004_Alarm_Core_Logic.md)

## 📡 API Specification

### POST /api/v1/alarms - 알람 생성

**Request Body 예시:**
```json
{
  "type": "FIXED",
  "time": "09:00:00",
  "label": "아침 명상",
  "daysOfWeek": ["MONDAY", "WEDNESDAY", "FRIDAY"],
  "isEnabled": true
}
```

**Response Body 예시 (201 Created):**
```json
{
  "id": 1,
  "type": "FIXED",
  "time": "09:00:00",
  "label": "아침 명상",
  "daysOfWeek": ["MONDAY", "WEDNESDAY", "FRIDAY"],
  "isEnabled": true,
  "createdAt": "2025-01-15T10:30:00",
  "updatedAt": "2025-01-15T10:30:00"
}
```

**Error Response 예시 (400 Bad Request):**
```json
{
  "code": "VALIDATION_FAILED",
  "message": "입력값 검증에 실패했습니다",
  "fieldErrors": [
    {
      "field": "time",
      "message": "알람 시간은 필수입니다"
    }
  ],
  "timestamp": "2025-01-15T10:30:00"
}
```

### PATCH /api/v1/alarms/{id}/toggle - 알람 토글

**Response Body 예시 (200 OK):**
```json
{
  "id": 1,
  "type": "FIXED",
  "time": "09:00:00",
  "label": "아침 명상",
  "daysOfWeek": ["MONDAY", "WEDNESDAY", "FRIDAY"],
  "isEnabled": false,
  "createdAt": "2025-01-15T10:30:00",
  "updatedAt": "2025-01-15T10:35:00"
}
```

## 🔄 Logic Steps (런타임 처리 순서)

### POST /api/v1/alarms - 알람 생성

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@PostMapping` 핸들러 메서드 호출
   - Request Body를 `CreateAlarmRequest` DTO로 역직렬화

2. **Request Validation** (Controller Layer)
   - `@Valid` 어노테이션으로 DTO 검증
   - `type` 필수 체크, `time` 형식 검증 (`HH:mm:ss`)
   - 실패 시: `400 Bad Request` 반환

3. **Service 메서드 호출** (`AlarmService.create()`)

4. **트랜잭션 시작** (`@Transactional`)

5. **Business Validation** (Service Layer)
   - 과거 시간 체크: `LocalTime.parse(time)`가 현재 시간보다 과거인지 확인
   - 실패 시: `IllegalArgumentException` throw → `400 Bad Request` 반환

6. **Entity 생성** (Service Layer)
   - `Alarm.builder()` 사용하여 Entity 생성
   - `type`, `time`, `label`, `daysOfWeek`, `isEnabled` 설정

7. **데이터베이스 저장** (Repository Layer)
   - `alarmRepository.save(alarm)` 실행
   - JPA가 INSERT 쿼리 생성 및 실행

8. **트랜잭션 커밋** (`@Transactional`)

9. **Entity → DTO 변환 및 응답** (Service → Controller)
   - `AlarmResponse.from(savedAlarm)` 호출
   - `201 Created` 상태 코드와 함께 응답 반환

### PATCH /api/v1/alarms/{id}/toggle - 알람 토글

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@PatchMapping("/{id}/toggle")` 핸들러 메서드 호출
   - Path Variable `id` 추출

2. **Service 메서드 호출** (`AlarmService.toggle(id)`)

3. **트랜잭션 시작** (`@Transactional`)

4. **리소스 존재 확인** (Service Layer)
   - `alarmRepository.findById(id)` 실행
   - 없으면: `AlarmNotFoundException` throw → `404 Not Found` 반환

5. **토글 처리** (Service Layer)
   - `alarm.setIsEnabled(!alarm.getIsEnabled())` 실행

6. **데이터베이스 저장** (Repository Layer)
   - `alarmRepository.save(alarm)` 실행
   - JPA가 UPDATE 쿼리 생성: `UPDATE alarms SET is_enabled = ? WHERE id = ?`

7. **트랜잭션 커밋** (`@Transactional`)

8. **Entity → DTO 변환 및 응답** (Service → Controller)
   - `AlarmResponse.from(updatedAlarm)` 호출
   - `200 OK` 상태 코드와 함께 응답 반환

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **중 (Medium)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 2-3일 내에 독립적으로 완료할 수 있는 작업 단위입니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-ALARM-DB-01** | 하 (Low) | 2-3시간 | Entity 설계, Repository 인터페이스 | Enum 타입, 복합 쿼리 |
| **TASK-ALARM-SERVICE-01** | 중 (Medium) | 5-7시간 | 비즈니스 로직, 스케줄링 로직, 유효성 검사 | 시간 검증, 스케줄링 알고리즘 |
| **TASK-ALARM-CONTROLLER-01** | 중 (Medium) | 3-4시간 | REST API 엔드포인트, DTO 매핑 | 6개 엔드포인트 구현 |
| **TASK-ALARM-TEST-01** | 중 (Medium) | 4-6시간 | 단위/통합/API 테스트 작성 | 스케줄링 로직 테스트 |

**총 예상 시간: 14-20시간 (2-3일)**

### 작업량 분해

**Day 1 (6-8시간):**
- Entity 및 Repository 구현 (3시간)
- Service 기본 구조 및 생성 로직 (3-4시간)

**Day 2 (6-8시간):**
- Service 수정/삭제/토글 로직 (3시간)
- 스케줄링 로직 및 유효성 검사 (3-4시간)
- Controller 구현 (2시간)

**Day 3 (2-4시간):**
- 테스트 작성 (4-6시간)
- 버그 수정 및 리팩토링 (2시간)

## 📌 Notes

- 이 Task는 #001 ✅ (완료) 후 즉시 시작 가능합니다.
- #003 (Habit Management)와 병렬 개발 가능합니다.
- 실제 OS 알림 연동은 모바일 앱에서 처리되며, 백엔드는 알람 데이터와 스케줄 정보만 제공합니다.

