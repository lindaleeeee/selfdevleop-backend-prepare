# Focus Habit Launcher Backend

> **백엔드 API 서버** - 습관 추적, 알람 관리, 데이터 시각화를 위한 RESTful API

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-4.0.1-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue.svg)](https://www.mysql.com/)
[![Gradle](https://img.shields.io/badge/Gradle-Latest-02303A.svg)](https://gradle.org/)

## 📋 목차

- [프로젝트 개요](#프로젝트-개요)
- [주요 기능](#주요-기능)
- [기술 스택](#기술-스택)
- [시작하기](#시작하기)
- [프로젝트 구조](#프로젝트-구조)
- [개발 가이드라인](#개발-가이드라인)
- [API 문서](#api-문서)
- [테스트](#테스트)
- [배포](#배포)
- [기여 가이드](#기여-가이드)

---

## 🎯 프로젝트 개요

**Focus Habit Launcher Backend**는 의지력 고갈을 겪는 지식 노동자들이 일관된 자기계발 습관을 유지할 수 있도록 돕는 백엔드 API 서버입니다. 모바일 애플리케이션(Android/iOS)을 위한 습관 추적, 알람/타이머 관리, 통계 및 데이터 시각화 기능을 제공합니다.

### 비전

사용자의 자기계발 습관을 효과적으로 추적하고 관리할 수 있는 안정적이고 신뢰할 수 있는 백엔드 API를 제공하여, 사용자가 목표를 달성하고 지속적인 성장을 이룰 수 있도록 지원합니다.

### 핵심 가치

- **데이터 무결성**: 습관 로그 및 세션 기록의 데이터 손실 제로
- **API 신뢰성**: 일관된 에러 처리 및 응답 형식
- **성능**: 핵심 엔드포인트 p95 < 1.0초 응답 시간
- **확장성**: 향후 클라우드 백업 및 멀티 디바이스 동기화 지원

---

## ✨ 주요 기능

### 1. 습관 관리 (Habit Management)
- 습관 생성, 수정, 삭제 (CRUD)
- 습관별 활성 요일 설정
- 습관별 기본 목표 시간 설정

### 2. 알람/타이머 관리 (Alarm/Timer Management)
- 정시 알람 설정 (예: 매일 07:00)
- 상대 시간 타이머 설정 (예: 지금부터 30분 뒤)
- 알람/타이머 라벨 및 반복 패턴 설정
- OS 알림 시스템 연동

### 3. 세션 로깅 (Session Logging)
- 습관 실행 세션 기록 (타임스탬프, 메모, 소요 시간)
- 텍스트 및 음성 메모 지원
- 자동 저장 및 데이터 영속성 보장

### 4. 통계 및 분석 (Statistics & Analytics)
- 일/주/월/년 단위 수행 데이터 집계
- 습관별 성취 현황 그래프 시각화
- 목표 대비 달성률 계산 및 표시

### 5. 목표 관리 (Goal Management)
- 습관별 일/주/월/년 목표 설정 (횟수 또는 시간)
- 목표 달성률 실시간 계산
- 목표 달성 현황 시각화

### 6. 데이터 내보내기 (Data Export)
- 세션 로그를 CSV/XLSX 형식으로 내보내기
- 파일 저장 및 공유 기능
- 로컬 처리 (외부 API 미사용)

### 7. 명언 관리 (Quote Management)
- NO 플로우용 동기부여 명언 데이터셋 관리
- 랜덤 명언 제공

---

## 🛠 기술 스택

### Backend Core
- **Framework**: Spring Boot 4.0.1
- **Language**: Java 21
- **Build Tool**: Gradle (latest stable)
- **API Style**: RESTful API
- **Architecture**: Layered Architecture (Controller → Service → Repository)

### Database
- **Primary DB**: MySQL 8.x (InnoDB, utf8mb4)
- **ORM**: Spring Data JPA / Hibernate
- **Migration**: Flyway or Liquibase (TBD)

### API Documentation
- **OpenAPI/Swagger**: SpringDoc OpenAPI 3.x

### Testing
- **Unit Testing**: JUnit 5, Mockito
- **Integration Testing**: Spring Boot Test, TestContainers (for DB)
- **API Testing**: REST Assured (optional)

### Security (Future)
- **Authentication**: JWT (Spring Security)
- **Encryption**: AES-256 for sensitive data at rest
- **TLS**: TLS 1.2+ for all transit

### Monitoring & Logging
- **Logging**: SLF4J + Logback
- **Monitoring**: Spring Boot Actuator (future)

---

## 🚀 시작하기

### 사전 요구사항

- **Java**: 21 이상
- **MySQL**: 8.x 이상
- **Gradle**: 프로젝트에 포함된 Gradle Wrapper 사용 (권장)

### 설치 및 실행

1. **저장소 클론**
```bash
git clone <repository-url>
cd selfdevleop-backend-prepare
```

2. **MySQL 데이터베이스 생성**
```sql
CREATE DATABASE habit_launcher_dev CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. **환경 변수 설정**

`src/main/resources/application-dev.properties` 파일 생성:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/habit_launcher_dev
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
logging.level.org.springframework.web=DEBUG
```

4. **애플리케이션 실행**

```bash
# Windows
gradlew.bat bootRun

# Linux/Mac
./gradlew bootRun
```

5. **애플리케이션 확인**

서버가 시작되면 다음 URL에서 확인할 수 있습니다:
- **애플리케이션**: http://localhost:8080
- **API 문서 (Swagger)**: http://localhost:8080/swagger-ui.html (설정 후)

### 빌드

```bash
# JAR 파일 빌드
./gradlew clean build

# 테스트 실행
./gradlew test

# 빌드된 JAR 실행
java -jar build/libs/selfdevleop-backend-prepare-0.0.1-SNAPSHOT.jar
```

---

## 📁 프로젝트 구조

```
src/
  main/
    java/
      vibe/selfdevleop/selfdevleop_backend_prepare/
        controller/     # REST API controllers
        service/        # Business logic
        repository/     # Data access layer
        entity/         # JPA entities
        dto/            # Data Transfer Objects (request/response)
        config/         # Configuration classes
        exception/      # Custom exceptions and handlers
    resources/
      application.properties
      application-dev.properties
      application-prod.properties
  test/
    java/               # Test classes
```

### 패키지 구조 설명

- **`controller/`**: REST API 엔드포인트 정의 (`@RestController`)
- **`service/`**: 비즈니스 로직 구현 (`@Service`)
- **`repository/`**: 데이터 접근 계층 (`@Repository`, JPA)
- **`entity/`**: JPA 엔티티 클래스 (`@Entity`)
- **`dto/`**: 요청/응답 데이터 전송 객체
- **`config/`**: 설정 클래스 (CORS, Security 등)
- **`exception/`**: 커스텀 예외 및 전역 예외 핸들러

---

## 📖 개발 가이드라인

### 아키텍처 원칙

- **Layered Architecture**: Controller → Service → Repository 패턴 준수
- **RESTful Design**: REST 컨벤션에 따른 리소스 명명 및 HTTP 메서드 사용
- **Separation of Concerns**: 각 레이어의 책임 명확히 분리

### 코딩 컨벤션

#### 네이밍 규칙
- **Controllers**: `*Controller` (예: `HabitController`)
- **Services**: `*Service` (예: `HabitService`)
- **Repositories**: `*Repository` (예: `HabitRepository`)
- **Entities**: 단수형 명사 (예: `Habit`, `SessionLog`)
- **DTOs**: `*Request`, `*Response`, 또는 `*Dto` (예: `CreateHabitRequest`, `HabitResponse`)

#### 코드 스타일
- Java 21 문법 활용
- Spring Boot 모범 사례 준수
- 의미 있는 주석 작성 (`.cursor/rules/201-code-commenting.mdc` 참조)
- DRY (Don't Repeat Yourself) 원칙 준수

### Git 워크플로우

- **Branching**: Git Flow / Feature Branch Workflow
- **Commit Policy**: Atomic commits, Conventional Commits 형식
- **예시**: `feat: add habit creation API`, `fix: resolve transaction rollback issue`

자세한 내용은 [`.cursor/rules/200-git-commit-push-pr.mdc`](.cursor/rules/200-git-commit-push-pr.mdc) 참조

### API 설계 원칙

- **URL 설계**: 명사 사용, 복수형 (예: `/api/v1/habits`)
- **HTTP 메서드**: GET (조회), POST (생성), PUT (전체 수정), PATCH (부분 수정), DELETE (삭제)
- **상태 코드**: 적절한 HTTP 상태 코드 사용 (200, 201, 400, 404, 500 등)
- **에러 응답**: 일관된 에러 응답 형식

자세한 내용은 [`.cursor/rules/401-rest-api-design-rules.mdc`](.cursor/rules/401-rest-api-design-rules.mdc) 참조

### 데이터베이스 설계

- **엔티티 설계**: JPA 어노테이션 활용 (`@Entity`, `@Table`, `@Column`)
- **관계 매핑**: `@OneToMany`, `@ManyToOne` 적절히 사용
- **트랜잭션**: `@Transactional` 어노테이션으로 트랜잭션 관리
- **마이그레이션**: Flyway 또는 Liquibase 사용 (TBD)

자세한 내용은 [`.cursor/rules/402-jpa-database-rules.mdc`](.cursor/rules/402-jpa-database-rules.mdc) 참조

### 예외 처리

- **커스텀 예외**: 도메인별 예외 클래스 정의
- **전역 예외 핸들러**: `@ControllerAdvice`로 일관된 에러 응답
- **에러 코드**: Enum으로 에러 코드 관리

자세한 내용은 [`.cursor/rules/403-exception-handling-rules.mdc`](.cursor/rules/403-exception-handling-rules.mdc) 참조

---

## 📚 API 문서

### Swagger UI

API 문서는 Swagger UI를 통해 제공됩니다 (설정 후):
- **URL**: http://localhost:8080/swagger-ui.html
- **OpenAPI Spec**: http://localhost:8080/v3/api-docs

### 주요 API 엔드포인트 (예정)

```
GET    /api/v1/habits              # 습관 목록 조회
POST   /api/v1/habits              # 습관 생성
GET    /api/v1/habits/{id}         # 습관 상세 조회
PUT    /api/v1/habits/{id}         # 습관 수정
DELETE /api/v1/habits/{id}         # 습관 삭제

GET    /api/v1/alarms              # 알람 목록 조회
POST   /api/v1/alarms              # 알람 생성
PUT    /api/v1/alarms/{id}         # 알람 수정
DELETE /api/v1/alarms/{id}         # 알람 삭제

POST   /api/v1/sessions            # 세션 로그 생성
GET    /api/v1/sessions            # 세션 로그 조회

GET    /api/v1/stats               # 통계 데이터 조회
GET    /api/v1/goals               # 목표 목록 조회
POST   /api/v1/goals               # 목표 생성

GET    /api/v1/export              # 데이터 내보내기
```

---

## 🧪 테스트

### 테스트 실행

```bash
# 모든 테스트 실행
./gradlew test

# 특정 테스트 클래스 실행
./gradlew test --tests "HabitServiceTest"

# 통합 테스트 실행
./gradlew integrationTest
```

### 테스트 커버리지

```bash
# 테스트 커버리지 리포트 생성
./gradlew test jacocoTestReport
```

### 테스트 전략

- **Unit Tests**: Service, Repository 레이어 단위 테스트
- **Integration Tests**: Controller → Service → Repository 통합 테스트
- **API Tests**: REST API 엔드포인트 테스트 (REST Assured)

---

## 🚢 배포

### 환경 변수 설정

프로덕션 환경에서는 다음 환경 변수를 설정해야 합니다:

```bash
DB_URL=jdbc:mysql://your-db-host:3306/habit_launcher_prod
DB_USERNAME=your_username
DB_PASSWORD=your_password
SERVER_PORT=8080
```

### 프로덕션 빌드

```bash
# 프로덕션 JAR 빌드
./gradlew clean build -Pprod

# 빌드된 JAR 실행
java -jar build/libs/selfdevleop-backend-prepare-0.0.1-SNAPSHOT.jar
```

### 성능 목표

- **API 응답 시간**: 런처 화면 p95 < 1.0초, 통계 p95 < 1.5초
- **데이터 신뢰성**: 99.5%+ 세션 로그 저장 성공률
- **에러율**: 일일 작업의 0.5% 미만 실패율
- **가동 시간**: 99.5% 가용성 SLA

---

## 🤝 기여 가이드

### 개발 프로세스

1. **이슈 생성**: 새로운 기능이나 버그 수정을 위한 이슈 생성
2. **브랜치 생성**: `feature/기능명` 또는 `fix/버그명` 형식으로 브랜치 생성
3. **개발**: 코드 작성 및 테스트
4. **커밋**: Conventional Commits 형식으로 커밋
5. **Pull Request**: PR 생성 및 코드 리뷰 요청

### 코드 리뷰 체크리스트

- [ ] 코드가 프로젝트의 코딩 컨벤션을 따르는가?
- [ ] 적절한 테스트가 작성되었는가?
- [ ] API 문서가 업데이트되었는가?
- [ ] 예외 처리가 적절한가?
- [ ] 성능에 영향을 주지 않는가?

---

## 📊 프로젝트 상태

### 현재 단계

- ✅ 프로젝트 초기 설정 완료
- ✅ 개발 환경 구성 완료
- 🚧 핵심 기능 개발 진행 중
- ⏳ 테스트 및 문서화 예정

### 로드맵

- **Phase 1**: 기본 CRUD API 구현 (습관, 알람)
- **Phase 2**: 세션 로깅 및 통계 기능 구현
- **Phase 3**: 목표 관리 및 데이터 내보내기
- **Phase 4**: 성능 최적화 및 보안 강화
- **Phase 5**: 인증/인가 및 클라우드 백업 (향후)

---

## 📝 참고 문서

### 프로젝트 문서
- [프로젝트 개요](.cursor/rules/001-project-overview.mdc)
- [기술 스택](.cursor/rules/002-tech-stack.mdc)
- [개발 가이드라인](.cursor/rules/003-development-guidelines.mdc)
- [빌드 및 환경 설정](.cursor/rules/101-build-and-env-setup.mdc)

### 개발 규칙
- [Spring Boot 규칙](.cursor/rules/400-spring-boot-rules.mdc)
- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 및 데이터베이스 규칙](.cursor/rules/402-jpa-database-rules.mdc)
- [예외 처리 규칙](.cursor/rules/403-exception-handling-rules.mdc)
- [공통 에러 패턴](.cursor/rules/110-common-error-patterns.mdc)

### 요구사항 문서
- [SRS 문서](Digital-minimalist-project_Self-development%20copy/5-2.PRD%EA%B8%B0%EB%B0%98%20SRS(Software-requirements-specification)_GPT5.md)
- [Task 체크리스트](Digital-minimalist-project_Self-development%20copy/6-3.SRS-GPT5%EA%B8%B0%EB%B0%98-TASK%EC%B2%B4%ED%81%AC%EB%A6%AC%EC%8A%A4%ED%8A%B8.md)
- [개발 Task 목록](Tasks%20copy/README.md)

---

## 🐛 문제 해결

### 자주 발생하는 문제

자세한 내용은 [공통 에러 패턴](.cursor/rules/110-common-error-patterns.mdc) 문서를 참조하세요.

1. **CORS 오류**: CORS 설정 확인
2. **데이터베이스 연결 오류**: 연결 URL 및 자격 증명 확인
3. **JPA 엔티티 매핑 오류**: 엔티티 어노테이션 및 패키지 구조 확인
4. **트랜잭션 문제**: `@Transactional` 어노테이션 확인

---

## 📄 라이선스

이 프로젝트는 [라이선스명] 라이선스를 따릅니다.

---

## 👥 팀

- **Owner**: (추후 기입)
- **Developers**: (추후 기입)

---

## 📞 문의

프로젝트 관련 문의사항이 있으시면 이슈를 생성해주세요.

---

**마지막 업데이트**: 2025-01-15

