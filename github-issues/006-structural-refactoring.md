# #006: 구조적 리팩토링 및 에러 처리

**Epic:** Refactoring  
**Type:** Functional  
**Priority:** P2 (Medium)  
**Labels:** `type:refactoring`, `type:backend`  
**Related REQ:** -  
**Dependencies:** #003, #004, #005  
**Parallelizable With:** #007, #008, #010, #012  
**Blocks:** None

---

## 📋 Description

복잡한 컴포넌트를 분리하고, 전역적인 에러 처리 메커니즘을 도입하여 코드 유지보수성을 높입니다.

## 📌 Scope / Out of Scope

### In Scope
- 전역 예외 처리 핸들러 구현
- 에러 응답 구조 표준화
- 코드 구조 개선 및 리팩토링
- 중복 코드 제거

### Out of Scope
- 새로운 기능 추가 (별도 이슈에서 처리)
- 데이터베이스 스키마 변경 (필요 시 별도 이슈)
- 성능 최적화 (#012에서 처리)

## 🎯 Goals

- 전역 예외 처리 핸들러 구현
- 에러 응답 구조 표준화
- 코드 구조 개선
- 매직 넘버 제거 및 상수화

## 🛠️ Technical Stack

**Backend Core:**
- Java 21 LTS
- Spring Boot 4.0.1
- Spring AOP (예외 처리)

**API:**
- RESTful API (JSON)
- 표준 HTTP 상태 코드

## ✅ Tasks

### TASK-REFACTOR-EXCEPTION-01: Global Exception Handler
- [ ] `GlobalExceptionHandler` 클래스 구현 (`@ControllerAdvice`)
- [ ] 커스텀 예외 클래스 정의
  - [ ] `HabitNotFoundException`
  - [ ] `AlarmNotFoundException`
  - [ ] `ValidationException`
- [ ] 에러 응답 DTO 구조 정의
- [ ] `MethodArgumentNotValidException` 처리
- [ ] `EntityNotFoundException` 처리
- [ ] 일반 예외 처리

### TASK-REFACTOR-CONSTANTS-01: Constants Extraction
- [ ] `Constants` 클래스 생성
- [ ] 매직 넘버 상수화
- [ ] 에러 메시지 상수화
- [ ] API 경로 상수화

### TASK-REFACTOR-STRUCTURE-01: Code Structure Improvement
- [ ] 복잡한 Service 메서드 분리
- [ ] 공통 로직 유틸리티 클래스로 추출
- [ ] DTO 매퍼 클래스 생성 (선택사항)

## 📝 Acceptance Criteria

- [ ] 전역 예외 핸들러가 정상 작동함
- [ ] 모든 API에서 일관된 에러 응답 형식 사용
- [ ] 매직 넘버가 상수로 추출됨
- [ ] 코드 복잡도가 감소함

## 🔗 Related Documentation

- [예외 처리 규칙](.cursor/rules/403-exception-handling-rules.mdc)
- [공통 에러 패턴](.cursor/rules/110-common-error-patterns.mdc)
- [Task 문서](Tasks%20copy/Functional/006_Structural_Refactoring.md)

## 🔄 Logic Steps (런타임 처리 순서)

### 예외 발생 시 전역 처리 흐름

**실행 순서:**
1. **예외 발생** (Service/Controller Layer)
   - 비즈니스 로직에서 예외 throw (예: `HabitNotFoundException`)

2. **Spring AOP 인터셉트** (AOP Layer)
   - `@ControllerAdvice`가 예외를 캐치
   - `GlobalExceptionHandler`의 적절한 `@ExceptionHandler` 메서드 호출

3. **예외 타입별 처리** (Exception Handler)
   - `HabitNotFoundException` → `handleHabitNotFoundException()` 실행
   - `MethodArgumentNotValidException` → `handleValidationException()` 실행
   - 일반 `Exception` → `handleException()` 실행

4. **에러 응답 생성** (Exception Handler)
   - `ErrorResponse.of(code, message)` 호출
   - 필드 에러가 있으면 `fieldErrors` 추가
   - `timestamp` 자동 설정

5. **HTTP Response 생성** (Exception Handler)
   - `ResponseEntity.status(HttpStatus.XXX).body(errorResponse)` 생성
   - 적절한 HTTP 상태 코드 설정 (404, 400, 409, 500 등)

6. **클라이언트 응답 전송** (Spring Framework)
   - JSON 직렬화 후 HTTP 응답 전송

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **하 (Low)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 1-2일 내에 독립적으로 완료할 수 있는 작업 단위입니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-REFACTOR-EXCEPTION-01** | 하 (Low) | 3-4시간 | GlobalExceptionHandler 구현 | 표준 패턴 |
| **TASK-REFACTOR-CONSTANTS-01** | 하 (Low) | 2-3시간 | 상수 추출 및 정리 | 매직 넘버 제거 |
| **TASK-REFACTOR-STRUCTURE-01** | 중 (Medium) | 4-6시간 | 코드 구조 개선 | 점진적 리팩토링 |

**총 예상 시간: 9-13시간 (1-2일)**

## 📌 Notes

- 이 Task는 기능 개발과 병렬로 진행 가능합니다.
- 점진적으로 리팩토링을 진행하며, 기존 기능에 영향을 주지 않도록 주의합니다.

