# #004: 알람 코어 로직 및 스케줄러

**Epic:** EPIC-3 (ALARM_CORE)  
**Type:** Functional  
**Priority:** P0 (Critical)  
**Labels:** `epic:alarm`, `type:backend`, `type:integration`  
**Related REQ:** REQ-FUNC-004, REQ-FUNC-005, REQ-FUNC-006, REQ-FUNC-008, REQ-FUNC-009  
**Dependencies:** #001 ✅ (완료)  
**Blocks:** #005

---

## 📋 Description

알람/타이머 스케줄링 및 OS 알림 시스템 연동 핵심 로직을 구현합니다.

**Note:** 백엔드에서는 알람 스케줄링 로직과 API를 제공하며, 실제 OS 알림은 모바일 앱에서 처리합니다.

## 🎯 Goals

- Alarm Entity 및 Repository 구현
- 알람/타이머 CRUD API 구현
- 알람 스케줄링 로직 구현
- 알람 상태 관리 로직 구현

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

## 📌 Notes

- 이 Task는 #001 ✅ (완료) 후 즉시 시작 가능합니다.
- #003 (Habit Management)와 병렬 개발 가능합니다.
- 실제 OS 알림 연동은 모바일 앱에서 처리되며, 백엔드는 알람 데이터와 스케줄 정보만 제공합니다.

