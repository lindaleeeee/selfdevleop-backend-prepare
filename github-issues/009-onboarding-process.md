# #009: 온보딩 및 초기 설정

**Epic:** EPIC-7 (ONBOARDING)  
**Type:** Functional  
**Priority:** P2 (Medium)  
**Labels:** `epic:onboarding`, `type:backend`, `type:database`  
**Related REQ:** REQ-FUNC-023  
**Dependencies:** #003, #004  
**Parallelizable With:** #006, #010, #012  
**Blocks:** None

---

## 📋 Description

앱 최초 실행 시 사용자에게 필요한 기본 습관 데이터를 설정하는 온보딩 프로세스를 지원하는 API를 구현합니다.

## 📌 Scope / Out of Scope

### In Scope
- 기본 습관 데이터 시드 로직 구현
- 기본 알람 프리셋 데이터 시드 로직 구현
- 온보딩 완료 상태 관리 API

### Out of Scope
- 온보딩 UI/UX (프론트엔드에서 처리)
- 사용자 튜토리얼 (프론트엔드에서 처리)
- 개인화된 추천 (Post-MVP)

## 🎯 Goals

- 기본 습관 데이터 시드 로직 구현
- 기본 알람 프리셋 데이터 시드 로직 구현
- 온보딩 상태 관리 API 구현

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

## 📡 API Specification

### POST /api/v1/onboarding/complete - 온보딩 완료 처리

**Request Body 예시:**
```json
{}
```

**Response Body 예시 (200 OK):**
```json
{
  "isCompleted": true,
  "completedAt": "2025-01-15T10:30:00"
}
```

### GET /api/v1/onboarding/status - 온보딩 상태 조회

**Response Body 예시 (200 OK):**
```json
{
  "isCompleted": false,
  "hasDefaultHabits": true,
  "hasDefaultAlarms": true
}
```

## 🔄 Logic Steps (런타임 처리 순서)

### POST /api/v1/onboarding/complete - 온보딩 완료 처리

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@PostMapping("/onboarding/complete")` 핸들러 메서드 호출

2. **Service 메서드 호출** (`OnboardingService.complete()`)

3. **트랜잭션 시작** (`@Transactional`)

4. **온보딩 상태 업데이트** (Service Layer)
   - 온보딩 완료 플래그 설정 (DB 또는 메모리)

5. **트랜잭션 커밋** (`@Transactional`)

6. **응답 생성** (Controller)
   - `200 OK` 상태 코드와 함께 응답 반환

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **하 (Low)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 1-2일 내에 독립적으로 완료할 수 있는 작업 단위입니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-ONBOARD-DATA-01** | 하 (Low) | 3-4시간 | 데이터 시드 스크립트 작성 | 초기 데이터 준비 |
| **TASK-ONBOARD-SERVICE-01** | 하 (Low) | 2-3시간 | 온보딩 서비스 로직 | 간단한 상태 관리 |
| **TASK-ONBOARD-CONTROLLER-01** | 하 (Low) | 2-3시간 | REST API 엔드포인트 | 3개 엔드포인트 |
| **TASK-ONBOARD-TEST-01** | 하 (Low) | 2-3시간 | 단위/통합/API 테스트 작성 | 기본 테스트 |

**총 예상 시간: 9-13시간 (1-2일)**

## 📌 Notes

- 이 Task는 #003과 #004 완료 후 시작해야 합니다.
- 데이터 시드는 개발 환경에서만 자동 실행되도록 설정합니다.
- 프로덕션 환경에서는 수동 실행 또는 마이그레이션 스크립트로 처리합니다.

