# #009: 온보딩 및 초기 설정

**Epic:** EPIC-7 (ONBOARDING)  
**Type:** Functional  
**Priority:** P2 (Medium)  
**Labels:** `epic:onboarding`, `type:backend`, `type:database`  
**Related REQ:** REQ-FUNC-023  
**Dependencies:** #003, #004  
**Blocks:** None

---

## 📋 Description

앱 최초 실행 시 사용자에게 필요한 기본 습관 데이터를 설정하는 온보딩 프로세스를 지원하는 API를 구현합니다.

## 🎯 Goals

- 기본 습관 데이터 시드 로직 구현
- 기본 알람 프리셋 데이터 시드 로직 구현
- 온보딩 상태 관리 API 구현

## ✅ Tasks

### TASK-ONBOARD-DATA-01: Default Seeding
- [ ] 기본 습관 데이터 시드 스크립트 작성
  - [ ] 명상, 독서, 운동, 영어, 영양제 등 기본 습관
- [ ] 기본 알람 프리셋 데이터 시드 스크립트 작성
- [ ] 데이터 시드 실행 로직 구현
  - [ ] `@PostConstruct` 또는 CommandLineRunner 사용
  - [ ] 중복 데이터 방지 로직

### TASK-ONBOARD-SERVICE-01: Onboarding Service
- [ ] `OnboardingService` 클래스 구현
- [ ] 온보딩 완료 여부 확인 로직
- [ ] 기본 데이터 시드 실행 로직
- [ ] 온보딩 상태 업데이트 로직

### TASK-ONBOARD-CONTROLLER-01: Onboarding Controller
- [ ] `OnboardingController` 클래스 구현
- [ ] `POST /api/v1/onboarding/complete` - 온보딩 완료 처리
- [ ] `GET /api/v1/onboarding/status` - 온보딩 상태 조회
- [ ] `POST /api/v1/onboarding/seed` - 기본 데이터 시드 실행 (개발용)

### TASK-ONBOARD-TEST-01: Onboarding Tests
- [ ] `OnboardingService` 단위 테스트 작성
- [ ] 데이터 시드 로직 테스트
- [ ] `OnboardingController` API 테스트 작성

## 📝 Acceptance Criteria

- [ ] 기본 습관 데이터가 정상적으로 시드됨
- [ ] 기본 알람 프리셋 데이터가 정상적으로 시드됨
- [ ] 온보딩 상태 관리 API가 정상 작동함
- [ ] 중복 데이터가 생성되지 않음
- [ ] 단위 테스트 커버리지 80% 이상
- [ ] API 문서(Swagger)에 정상 반영됨

## 🔗 Related Documentation

- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 및 데이터베이스 규칙](.cursor/rules/402-jpa-database-rules.mdc)
- [Task 문서](Tasks%20copy/Functional/009_Onboarding_Process.md)

## 📌 Notes

- 이 Task는 #003과 #004 완료 후 시작해야 합니다.
- 데이터 시드는 개발 환경에서만 자동 실행되도록 설정합니다.
- 프로덕션 환경에서는 수동 실행 또는 마이그레이션 스크립트로 처리합니다.

