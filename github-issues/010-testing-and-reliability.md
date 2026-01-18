# #010: 테스트 코드 작성 및 안정성 확보

**Epic:** QA & Reliability  
**Type:** Non-Functional  
**Priority:** P1 (High)  
**Labels:** `type:testing`, `type:reliability`, `type:qa`  
**Related REQ:** REQ-NF-003  
**Dependencies:** #003, #004, #005, #007  
**Parallelizable With:** #006, #011, #012  
**Blocks:** #013

---

## 📋 Description

주요 비즈니스 로직과 API에 대한 테스트 코드를 작성하여 앱의 안정성과 데이터 무손실을 확보합니다.

## 📌 Scope / Out of Scope

### In Scope
- 단위 테스트 작성 (Service, Repository 레이어)
- 통합 테스트 작성 (Controller 레이어)
- 테스트 커버리지 80% 이상 달성
- 데이터 무손실 검증

### Out of Scope
- E2E 테스트 (프론트엔드와 통합 테스트, 별도 프로젝트)
- 성능 테스트 (#011에서 처리)
- 보안 테스트 (#011에서 처리)

## 🎯 Goals

- 단위 테스트 작성
- 통합 테스트 작성
- API 테스트 작성
- 데이터 무손실 검증 로직 구현

## 🛠️ Technical Stack

**Testing Framework:**
- JUnit 5
- Mockito
- Spring Boot Test
- TestContainers (통합 테스트)
- REST Assured 또는 MockMvc (API 테스트)

**Coverage Tool:**
- JaCoCo (코드 커버리지 측정)

**CI/CD:**
- GitHub Actions (테스트 자동화)

## ✅ Tasks

### TASK-TEST-UNIT-01: Unit Tests
- [ ] Service 레이어 단위 테스트 작성
  - [ ] `HabitService` 테스트
  - [ ] `AlarmService` 테스트
  - [ ] `LogEntryService` 테스트
  - [ ] `StatisticsService` 테스트
  - [ ] `GoalService` 테스트
- [ ] Repository 레이어 단위 테스트 작성
- [ ] 유틸리티 함수 테스트 작성
- [ ] Mockito를 사용한 의존성 모킹

### TASK-TEST-INTEGRATION-01: Integration Tests
- [ ] Controller → Service → Repository 통합 테스트 작성
- [ ] TestContainers를 사용한 데이터베이스 통합 테스트
- [ ] 트랜잭션 테스트 작성
- [ ] 데이터 일관성 테스트 작성

### TASK-TEST-API-01: API Tests
- [ ] REST Assured 또는 MockMvc를 사용한 API 테스트 작성
- [ ] 모든 엔드포인트에 대한 테스트 작성
- [ ] 에러 케이스 테스트 작성
- [ ] 인증/인가 테스트 작성 (향후)

### TASK-REL-BACKUP-01: Data Reliability
- [ ] 데이터 무손실 검증 로직 구현 (REQ-NF-003)
- [ ] 트랜잭션 롤백 메커니즘 테스트
- [ ] 데이터 백업 로직 구현 (선택사항)
- [ ] 데이터 복구 메커니즘 구현 (선택사항)

### TASK-TEST-COVERAGE-01: Test Coverage
- [ ] 테스트 커버리지 측정 도구 설정 (JaCoCo)
- [ ] 커버리지 목표 설정 (80% 이상)
- [ ] 커버리지 리포트 생성
- [ ] 커버리지 부족 영역 보완

## 📝 Acceptance Criteria

- [ ] 모든 Service 레이어에 단위 테스트 작성됨
- [ ] 주요 API 엔드포인트에 통합 테스트 작성됨
- [ ] 테스트 커버리지 80% 이상 달성
- [ ] 데이터 무손실 검증 로직이 정상 작동함
- [ ] CI/CD 파이프라인에서 테스트 자동 실행됨

## 🔗 Related Documentation

- [Spring Boot 규칙](.cursor/rules/400-spring-boot-rules.mdc)
- [Task 문서](Tasks%20copy/Non-Functional/010_Testing_and_Reliability.md)

## 🔄 Logic Steps (런타임 처리 순서)

### 단위 테스트 실행 흐름

**실행 순서:**
1. **테스트 클래스 로드** (JUnit 5)
   - `@SpringBootTest` 또는 `@ExtendWith(MockitoExtension.class)` 어노테이션 처리

2. **의존성 주입 및 Mock 설정** (Mockito)
   - `@Mock` 또는 `@MockBean` 어노테이션으로 의존성 모킹
   - `when().thenReturn()` 또는 `given().willReturn()` 사용

3. **테스트 메서드 실행** (JUnit 5)
   - `@Test` 어노테이션이 붙은 메서드 실행
   - `@BeforeEach`, `@AfterEach` 훅 실행

4. **Service 메서드 호출** (테스트 대상)
   - 실제 Service 메서드 호출
   - Mock된 Repository가 동작

5. **검증** (Assertions)
   - `assertEquals()`, `assertNotNull()` 등으로 결과 검증
   - `verify()`로 Mock 호출 검증

6. **테스트 결과 리포트** (JUnit 5)
   - 성공/실패 결과 리포트 생성

### 통합 테스트 실행 흐름

**실행 순서:**
1. **Spring Context 로드** (`@SpringBootTest`)
   - 실제 Spring Application Context 로드
   - TestContainers로 데이터베이스 컨테이너 시작

2. **데이터베이스 초기화** (TestContainers)
   - H2 또는 MySQL 컨테이너 시작
   - 스키마 생성 및 초기 데이터 삽입

3. **테스트 메서드 실행** (JUnit 5)
   - `@Transactional` 어노테이션으로 트랜잭션 관리
   - 각 테스트 후 롤백

4. **실제 Repository 호출** (테스트 대상)
   - 실제 데이터베이스 쿼리 실행

5. **검증** (Assertions)
   - 데이터베이스 상태 검증
   - 트랜잭션 롤백 확인

6. **리소스 정리** (TestContainers)
   - 테스트 완료 후 컨테이너 종료

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **중 (Medium)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 지속적으로 진행하며, 각 기능 개발 시 함께 테스트 코드를 작성합니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-TEST-UNIT-01** | 중 (Medium) | 8-12시간 | Service/Repository 단위 테스트 | Mockito 사용 |
| **TASK-TEST-INTEGRATION-01** | 중 (Medium) | 6-8시간 | 통합 테스트 작성 | TestContainers 사용 |
| **TASK-TEST-API-01** | 중 (Medium) | 6-8시간 | API 테스트 작성 | REST Assured/MockMvc |
| **TASK-REL-BACKUP-01** | 중 (Medium) | 4-6시간 | 데이터 무손실 검증 | 트랜잭션 테스트 |
| **TASK-TEST-COVERAGE-01** | 하 (Low) | 2-3시간 | 커버리지 도구 설정 | JaCoCo 설정 |

**총 예상 시간: 26-37시간 (지속적 작업)**

### 작업량 분해

**각 기능 개발 시마다 (병렬 작업):**
- 기능 개발 완료 후 즉시 단위 테스트 작성 (2-3시간)
- 통합 테스트 작성 (1-2시간)

**전체 기능 완료 후:**
- API 테스트 작성 (6-8시간)
- 커버리지 측정 및 보완 (4-6시간)

## 📌 Notes

- 이 Task는 기능 개발과 병렬로 진행 가능합니다.
- 각 기능 개발 시 함께 테스트 코드를 작성하는 것을 권장합니다.
- 테스트는 CI/CD 파이프라인에 통합되어야 합니다.

