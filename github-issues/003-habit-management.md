# #003: 습관 관리 데이터 및 로직 구현

**Epic:** EPIC-2 (HABIT_MGMT)  
**Type:** Functional  
**Priority:** P0 (Critical)  
**Labels:** `epic:habit`, `type:backend`, `type:database`  
**Related REQ:** REQ-FUNC-001, REQ-FUNC-002, REQ-FUNC-003  
**Dependencies:** #001 ✅ (완료)  
**Blocks:** #005, #007, #009

---

## 📋 Description

사용자가 습관을 생성, 수정, 삭제할 수 있는 데이터 레이어와 비즈니스 로직을 구현합니다.

## 🎯 Goals

- Habit Entity 및 Repository 구현
- 습관 CRUD API 구현
- 습관 활성 요일 설정 기능 구현
- 습관 관리 비즈니스 로직 구현

## ✅ Tasks

### TASK-HABIT-DB-01: Habit Entity
- [ ] `Habit` JPA Entity 설계 및 구현
  - [ ] 필드: `id`, `name`, `icon`, `color`, `activeDays`, `defaultDuration`, `isArchived`
  - [ ] `@Entity`, `@Table` 어노테이션 적용
  - [ ] `@CreatedDate`, `@LastModifiedDate` 적용
- [ ] `HabitRepository` 인터페이스 생성
- [ ] 기본 CRUD 쿼리 메서드 정의
- [ ] 요일별 활성 습관 필터링 쿼리 구현

### TASK-HABIT-SERVICE-01: Habit Service
- [ ] `HabitService` 클래스 구현
- [ ] 습관 생성 로직 구현
  - [ ] 입력값 유효성 검사 (이름 필수, 색상 선택 등)
  - [ ] 중복 이름 체크
- [ ] 습관 수정 로직 구현
- [ ] 습관 삭제 로직 구현 (Soft Delete 고려)
- [ ] 요일별 활성 습관 조회 로직 구현

### TASK-HABIT-CONTROLLER-01: Habit Controller
- [ ] `HabitController` 클래스 구현
- [ ] `GET /api/v1/habits` - 습관 목록 조회
- [ ] `GET /api/v1/habits/{id}` - 습관 상세 조회
- [ ] `POST /api/v1/habits` - 습관 생성
- [ ] `PUT /api/v1/habits/{id}` - 습관 수정
- [ ] `DELETE /api/v1/habits/{id}` - 습관 삭제
- [ ] Request/Response DTO 구현
- [ ] `@Valid` 어노테이션을 통한 입력 검증

### TASK-HABIT-TEST-01: Habit Tests
- [ ] `HabitService` 단위 테스트 작성
- [ ] `HabitRepository` 통합 테스트 작성
- [ ] `HabitController` API 테스트 작성
- [ ] 요일 필터링 로직 테스트

## 📝 Acceptance Criteria

- [ ] 습관 생성 API가 정상 작동함
- [ ] 습관 수정/삭제 API가 정상 작동함
- [ ] 요일별 활성 습관 필터링이 정상 작동함
- [ ] 입력값 유효성 검사가 정상 작동함
- [ ] 단위 테스트 커버리지 80% 이상
- [ ] API 문서(Swagger)에 정상 반영됨

## 🔗 Related Documentation

- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 및 데이터베이스 규칙](.cursor/rules/402-jpa-database-rules.mdc)
- [예외 처리 규칙](.cursor/rules/403-exception-handling-rules.mdc)
- [Task 문서](Tasks%20copy/Functional/003_Habit_Management.md)

## 📌 Notes

- 이 Task는 #001 ✅ (완료) 후 즉시 시작 가능합니다.
- #004 (Alarm Core)와 병렬 개발 가능합니다.
- 데이터베이스 마이그레이션은 Flyway 또는 Liquibase를 사용합니다.

