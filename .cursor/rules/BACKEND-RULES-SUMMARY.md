# 백엔드 개발 규칙 수정 요약

## 📋 작업 개요
Focus Habit Launcher 백엔드 개발 프로젝트에 맞게 `.cursor/rules` 경로의 규칙들을 수정하고 보완했습니다.

---

## ✅ 수정된 규칙 파일

### 1. **001-project-overview.mdc** (완전 수정)
- **변경 전:** AI Co-Pilot for First-time Founders 프로젝트 내용
- **변경 후:** Focus Habit Launcher Backend 프로젝트 개요
- **주요 내용:**
  - 백엔드 API 중심의 비전 및 목표
  - 핵심 기능: Habit Management, Alarm/Timer, Session Logging, Statistics 등
  - 성공 지표: API 응답 시간, 데이터 신뢰성, 에러율

### 2. **002-tech-stack.mdc** (완전 수정)
- **변경 전:** 프론트엔드 기술 스택 (React, Vite, Tailwind 등)
- **변경 후:** 백엔드 기술 스택
- **주요 내용:**
  - Spring Boot 4.0.1, Java 21
  - MySQL 8.x, Spring Data JPA
  - OpenAPI/Swagger 문서화
  - 테스트 프레임워크 (JUnit 5, Mockito, TestContainers)

### 3. **003-development-guidelines.mdc** (부분 수정)
- **변경 사항:**
  - Technology Constraints: 백엔드 중심으로 수정
  - Architecture Principles: Layered Architecture, RESTful Design
  - Performance Standards: API 응답 시간 기준으로 변경
  - Development Priorities: 데이터 무결성, API 신뢰성 중심

### 4. **101-build-and-env-setup.mdc** (완전 수정)
- **변경 전:** 일반적인 빌드 프로세스 설명
- **변경 후:** Spring Boot/Gradle 빌드 가이드
- **주요 내용:**
  - Gradle 빌드 명령어
  - 프로젝트 구조 (Controller, Service, Repository 등)
  - 개발/운영 환경 변수 설정 예시

### 5. **110-common-error-patterns.mdc** (완전 수정)
- **변경 전:** 프론트-백엔드 연동 시 Vite 프록시 설정 중심
- **변경 후:** 백엔드 개발 시 자주 발생하는 에러 패턴
- **주요 내용:**
  - CORS 설정
  - 데이터베이스 연결 문제
  - JPA/Hibernate 엔티티 매핑 오류
  - 트랜잭션 관리 문제
  - NullPointerException 처리
  - Validation 에러 처리
  - 순환 의존성 문제
  - 날짜/시간 처리 문제

### 6. **000-meta-rule-script.mdc** (부분 수정)
- **변경 사항:**
  - Development Philosophy: 데이터 무결성 중심으로 변경
  - Quality Assurance: API 응답 시간 기준으로 변경
  - Technical Excellence: Spring Boot 스택 중심
  - Architecture Principles: Layered Architecture
  - Performance: 데이터베이스 쿼리 최적화 중심

---

## 🆕 새로 추가된 규칙 파일

### 7. **400-spring-boot-rules.mdc** (신규)
- **내용:** Spring Boot 개발 패턴 및 모범 사례
- **주요 항목:**
  - 프로젝트 구조 (Controller, Service, Repository)
  - 네이밍 컨벤션
  - Controller/Service 레이어 가이드라인
  - 의존성 주입 패턴
  - 설정 관리
  - 테스트 전략

### 8. **401-rest-api-design-rules.mdc** (신규)
- **내용:** REST API 설계 패턴 및 컨벤션
- **주요 항목:**
  - URL 설계 원칙
  - HTTP 메서드 사용법
  - 상태 코드 사용 가이드
  - Request/Response DTO 패턴
  - Pagination, Filtering, Sorting
  - 에러 응답 형식
  - API 문서화 (OpenAPI)

### 9. **402-jpa-database-rules.mdc** (신규)
- **내용:** JPA 및 데이터베이스 패턴
- **주요 항목:**
  - 엔티티 설계 (기본 어노테이션, 관계 매핑)
  - Repository 패턴 및 쿼리 최적화
  - 트랜잭션 관리
  - 데이터베이스 마이그레이션 (Flyway)
  - 성능 최적화 (인덱싱, 배치 작업)

### 10. **403-exception-handling-rules.mdc** (신규)
- **내용:** 예외 처리 패턴 및 에러 응답 구조
- **주요 항목:**
  - 커스텀 예외 계층 구조
  - 에러 코드 정의
  - Global Exception Handler (@ControllerAdvice)
  - 에러 응답 DTO 구조
  - Validation 예외 처리
  - 로깅 모범 사례

---

## 📝 프론트엔드 규칙 처리

### 11. **README-FRONTEND-RULES.mdc** (신규)
- **목적:** 프론트엔드 관련 규칙(306-311, 312)에 대한 설명 문서
- **내용:**
  - 해당 규칙들이 백엔드 프로젝트에 적용되지 않음을 명시
  - 향후 프론트엔드 개발 시 참고용으로 보관

### 12. **306-react-vite-tailwind-rules.mdc** (부분 수정)
- **변경 사항:** 설명에 "FRONTEND ONLY, NOT APPLICABLE TO BACKEND" 추가

---

## 🎯 규칙 적용 우선순위

### Always Apply (항상 적용)
- `000-meta-rule-script.mdc` - 메타 규칙
- `001-project-overview.mdc` - 프로젝트 개요
- `002-tech-stack.mdc` - 기술 스택
- `003-development-guidelines.mdc` - 개발 가이드라인
- `110-common-error-patterns.mdc` - 공통 에러 패턴

### Conditional Apply (조건부 적용)
- `400-spring-boot-rules.mdc` - Java 파일에만 적용 (`**/*.java`)
- `401-rest-api-design-rules.mdc` - Controller/DTO 파일에만 적용
- `402-jpa-database-rules.mdc` - Entity/Repository 파일에만 적용
- `403-exception-handling-rules.mdc` - Exception/Controller 파일에만 적용

### Not Applied (적용 안 함)
- `306-311`, `312` - 프론트엔드 관련 규칙 (백엔드 프로젝트에서는 비활성화)

---

## 📊 변경 통계

- **수정된 파일:** 6개
- **신규 생성 파일:** 5개
- **비활성화된 파일:** 7개 (프론트엔드 규칙)

---

## 🔍 주요 개선 사항

1. **프로젝트 컨텍스트 정확성**
   - 이전 프로젝트(AI Co-Pilot) 내용을 현재 프로젝트(Focus Habit Launcher)로 완전 교체

2. **기술 스택 명확화**
   - 프론트엔드 중심 → 백엔드 중심으로 전환
   - Spring Boot 4.0.1, Java 21, MySQL 8.x 명시

3. **백엔드 개발 가이드라인 보강**
   - Spring Boot 패턴, REST API 설계, JPA 사용법, 예외 처리 등 상세 규칙 추가

4. **에러 패턴 실용성 향상**
   - 실제 백엔드 개발 시 자주 발생하는 문제와 해결책 제시

5. **프론트엔드 규칙 분리**
   - 향후 프론트엔드 개발 시 참고할 수 있도록 별도 문서화

---

## 🚀 다음 단계 권장 사항

1. **프로젝트 구조 생성**
   - Controller, Service, Repository, Entity, DTO 패키지 구조 생성
   - 예제 엔티티 및 기본 CRUD 구현

2. **데이터베이스 설정**
   - MySQL 데이터베이스 생성
   - Flyway 또는 Liquibase 마이그레이션 설정

3. **API 문서화 설정**
   - SpringDoc OpenAPI 설정
   - 기본 API 엔드포인트 문서화

4. **예외 처리 구현**
   - Global Exception Handler 구현
   - 커스텀 예외 클래스 생성

5. **테스트 환경 구성**
   - JUnit 5 테스트 작성
   - TestContainers를 활용한 통합 테스트 설정

---

## 📚 참고 문서

- [Spring Boot 공식 문서](https://spring.io/projects/spring-boot)
- [Spring Data JPA 문서](https://spring.io/projects/spring-data-jpa)
- [REST API 설계 가이드](https://restfulapi.net/)
- [OpenAPI 스펙](https://swagger.io/specification/)

