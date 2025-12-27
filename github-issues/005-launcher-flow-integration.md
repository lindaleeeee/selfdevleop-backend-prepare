# #005: 런처 플로우 및 데이터 연동

**Epic:** EPIC-4 (LAUNCHER_FLOW)  
**Type:** Functional  
**Priority:** P0 (Critical)  
**Labels:** `epic:launcher`, `type:backend`, `type:integration`  
**Related REQ:** REQ-FUNC-012, REQ-FUNC-013, REQ-FUNC-014, REQ-FUNC-015, REQ-FUNC-016, REQ-FUNC-017, REQ-FUNC-018  
**Dependencies:** #002 ✅ (완료), #003, #004  
**Blocks:** #007, #008

---

## 📋 Description

알람이 울렸을 때 런처 플로우를 지원하는 API를 구현하고, 실제 데이터(DB)와 연동하여 기록을 저장합니다.

**참고:** 프론트엔드 PoC (#002)가 별도 프로젝트에서 완료되었으므로, 이 작업에서는 백엔드 API를 구현하여 프론트엔드와 연동할 수 있도록 합니다.

## 🎯 Goals

- LogEntry Entity 및 Repository 구현
- 세션 로깅 API 구현
- 명언 데이터 관리 API 구현
- 런처 플로우 관련 API 구현

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

## 📌 Notes

- 이 Task는 #003과 #004 완료 후 시작해야 합니다.
- 프론트엔드 PoC (#002)가 완료되었으므로, 백엔드 API 구현 후 프론트엔드와 연동 테스트를 진행합니다.
- 음성 인식은 모바일 앱에서 처리되며, 백엔드는 음성 파일 경로만 저장합니다.
- 명언 데이터는 초기 데이터로 DB에 시드됩니다.

