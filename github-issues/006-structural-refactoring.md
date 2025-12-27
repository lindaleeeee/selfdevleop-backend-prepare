# #006: 구조적 리팩토링 및 에러 처리

**Epic:** Refactoring  
**Type:** Functional  
**Priority:** P2 (Medium)  
**Labels:** `type:refactoring`, `type:backend`  
**Related REQ:** -  
**Dependencies:** #003, #004, #005  
**Blocks:** None

---

## 📋 Description

복잡한 컴포넌트를 분리하고, 전역적인 에러 처리 메커니즘을 도입하여 코드 유지보수성을 높입니다.

## 🎯 Goals

- 전역 예외 처리 핸들러 구현
- 에러 응답 구조 표준화
- 코드 구조 개선
- 매직 넘버 제거 및 상수화

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

## 📌 Notes

- 이 Task는 기능 개발과 병렬로 진행 가능합니다.
- 점진적으로 리팩토링을 진행하며, 기존 기능에 영향을 주지 않도록 주의합니다.

