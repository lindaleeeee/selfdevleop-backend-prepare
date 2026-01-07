# #003: 습관 관리 기능 - Acceptance Criteria 체크리스트

**Issue:** #003 습관 관리 데이터 및 로직 구현  
**Epic:** EPIC-2 (HABIT_MGMT)  
**Priority:** P0 (Critical)  
**예상 소요 시간:** 2-3일 (16-24시간)

---

## ✅ Acceptance Criteria

### 성공률: ___% (___/25)

---

## 📦 TASK-HABIT-DB-01: Entity & Repository

### Entity 구현
- [ ] `Habit` JPA Entity 클래스 생성
- [ ] 필드 구현
  - [ ] `id` (Long, PK, AUTO_INCREMENT)
  - [ ] `name` (String, NOT NULL, 100자)
  - [ ] `icon` (String, NOT NULL, 50자)
  - [ ] `color` (String, NULL, 7자)
  - [ ] `activeDays` (List<DayOfWeek>)
  - [ ] `defaultDuration` (Integer, 기본값 30)
  - [ ] `isArchived` (Boolean, 기본값 false)
- [ ] `@Entity`, `@Table(name = "habits")` 어노테이션 적용
- [ ] `@CreatedDate`, `@LastModifiedDate` 적용 (JPA Auditing)
- [ ] `@ElementCollection`으로 activeDays 매핑

### Repository 구현
- [ ] `HabitRepository` 인터페이스 생성 (extends JpaRepository)
- [ ] `existsByName(String name)` 메서드 정의
- [ ] `findByNameAndIdNot(String name, Long id)` 메서드 정의
- [ ] `findByIsArchived(Boolean isArchived, Pageable pageable)` 메서드 정의
- [ ] `findByActiveDaysContaining(DayOfWeek dayOfWeek, Pageable pageable)` 커스텀 쿼리 구현

---

## 📡 TASK-HABIT-CONTROLLER-01: REST API 엔드포인트

### GET /api/v1/habits - 습관 목록 조회
| 테스트 항목 | 상태 |
|------------|:----:|
| 기본 목록 조회 (200 OK) | ⬜ |
| `?dayOfWeek=MONDAY` 필터링 정상 작동 | ⬜ |
| `?archived=false` 필터링 정상 작동 | ⬜ |
| `?page=0&size=20` 페이지네이션 정상 작동 | ⬜ |
| `?sort=createdAt,desc` 정렬 정상 작동 | ⬜ |
| 잘못된 쿼리 파라미터 시 400 Bad Request | ⬜ |

### GET /api/v1/habits/{id} - 습관 상세 조회
| 테스트 항목 | 상태 |
|------------|:----:|
| 존재하는 ID로 조회 (200 OK) | ⬜ |
| 존재하지 않는 ID로 조회 (404 Not Found) | ⬜ |
| 응답 본문에 모든 필드 포함 | ⬜ |

### POST /api/v1/habits - 습관 생성
| 테스트 항목 | 상태 |
|------------|:----:|
| 정상 요청으로 생성 (201 Created) | ⬜ |
| `Location` 헤더 포함 (/api/v1/habits/{id}) | ⬜ |
| `name` 누락 시 400 Bad Request | ⬜ |
| `icon` 누락 시 400 Bad Request | ⬜ |
| `activeDays` 빈 배열 시 400 Bad Request | ⬜ |
| `name` 100자 초과 시 400 Bad Request | ⬜ |
| `color` 잘못된 형식(#XXXXXX 아님) 시 400 Bad Request | ⬜ |
| 중복 이름으로 생성 시 409 Conflict | ⬜ |
| `color` 미입력 시 기본값 #4A90E2 적용 | ⬜ |
| `defaultDuration` 미입력 시 기본값 30 적용 | ⬜ |

### PUT /api/v1/habits/{id} - 습관 수정
| 테스트 항목 | 상태 |
|------------|:----:|
| 정상 요청으로 수정 (200 OK) | ⬜ |
| 존재하지 않는 ID로 수정 (404 Not Found) | ⬜ |
| 부분 업데이트 정상 작동 (name만 변경) | ⬜ |
| 중복 이름으로 수정 시 409 Conflict | ⬜ |
| 자기 자신 이름은 중복 체크에서 제외 | ⬜ |
| `updatedAt` 필드 자동 갱신 | ⬜ |

### DELETE /api/v1/habits/{id} - 습관 삭제
| 테스트 항목 | 상태 |
|------------|:----:|
| 정상 삭제 (204 No Content) | ⬜ |
| Soft Delete 적용 (isArchived = true) | ⬜ |
| 존재하지 않는 ID로 삭제 (404 Not Found) | ⬜ |
| 삭제 후 목록에서 제외됨 (archived=false 필터) | ⬜ |

---

## 🔧 TASK-HABIT-SERVICE-01: 비즈니스 로직

### 생성 로직
- [ ] 중복 이름 체크 (`existsByName()`) 정상 작동
- [ ] Entity 생성 시 기본값 설정 정상 작동
- [ ] 트랜잭션 내에서 저장 정상 작동

### 수정 로직
- [ ] 리소스 존재 확인 정상 작동
- [ ] 중복 이름 체크 (자신 제외) 정상 작동
- [ ] 부분 업데이트 로직 정상 작동 (null 필드 무시)

### 삭제 로직
- [ ] 리소스 존재 확인 정상 작동
- [ ] Soft Delete (isArchived = true) 정상 작동

### 조회 로직
- [ ] 요일별 필터링 정상 작동
- [ ] 아카이브 필터링 정상 작동
- [ ] 페이지네이션 정상 작동
- [ ] 정렬 정상 작동

---

## 📋 TASK-HABIT-DTO-01: Request/Response DTO

### CreateHabitRequest
- [ ] `@NotBlank` on `name` 적용
- [ ] `@Size(min=1, max=100)` on `name` 적용
- [ ] `@NotBlank` on `icon` 적용
- [ ] `@Size(max=50)` on `icon` 적용
- [ ] `@Pattern(regexp="^#[0-9A-Fa-f]{6}$")` on `color` 적용
- [ ] `@NotEmpty` on `activeDays` 적용
- [ ] `@Min(1)`, `@Max(1440)` on `defaultDuration` 적용

### UpdateHabitRequest
- [ ] 모든 필드 Optional로 구현
- [ ] `isArchived` 필드 추가

### HabitResponse
- [ ] 모든 필드 포함 (id, name, icon, color, activeDays, defaultDuration, isArchived, createdAt, updatedAt)
- [ ] `from(Habit)` 정적 팩토리 메서드 구현

### ErrorResponse
- [ ] `code`, `message`, `fieldErrors`, `timestamp` 필드 포함
- [ ] 필드별 에러 메시지 포함

---

## 🧪 TASK-HABIT-TEST-01: 테스트 코드

### 단위 테스트
- [ ] `HabitService.create()` 테스트 (정상 케이스)
- [ ] `HabitService.create()` 테스트 (중복 이름 예외)
- [ ] `HabitService.update()` 테스트 (정상 케이스)
- [ ] `HabitService.update()` 테스트 (존재하지 않음 예외)
- [ ] `HabitService.delete()` 테스트 (정상 케이스)
- [ ] `HabitService.findAll()` 테스트 (필터링)

### 통합 테스트
- [ ] `HabitRepository` 통합 테스트 (H2 Database)
- [ ] 요일별 필터링 쿼리 테스트

### API 테스트
- [ ] POST /api/v1/habits 테스트
- [ ] GET /api/v1/habits 테스트
- [ ] GET /api/v1/habits/{id} 테스트
- [ ] PUT /api/v1/habits/{id} 테스트
- [ ] DELETE /api/v1/habits/{id} 테스트

### 테스트 커버리지
- [ ] 테스트 커버리지 80% 이상 달성

---

## 📖 문서화

- [ ] Swagger/OpenAPI 문서에 모든 엔드포인트 반영
- [ ] 각 엔드포인트에 설명 및 예제 추가
- [ ] 에러 응답 케이스 문서화

---

## ⚠️ 미구현 항목 및 향후 개선 사항

### SRS 성능 요구사항 대비 현황

| 요구사항 | 목표 | 현재 상태 |
|---------|------|----------|
| REQ-NF-001 | p95 ≤ 1.0초 | ⬜ 성능 테스트 필요 |
| REQ-NF-002 | p95 ≤ 1.5초 | ⬜ 성능 테스트 필요 |

### 필수 구현 항목 (Post-MVP)

| 항목 | 우선순위 | 관련 이슈 |
|------|---------|----------|
| 인증/인가 적용 | High | #011 |
| 사용자별 데이터 격리 | High | #011 |
| 캐싱 전략 적용 | Medium | #012 |

### 권장 개선 항목

| 항목 | 예상 효과 |
|------|----------|
| 쿼리 최적화 (N+1 방지) | 응답시간 ~30% 단축 |
| 인덱스 추가 (active_days, is_archived) | 조회 성능 향상 |

---

## 📊 최종 점검 결과

### 체크 결과 요약

| 카테고리 | 완료 | 미완료 | 완료율 |
|---------|:----:|:-----:|:-----:|
| Entity & Repository | __/13 | __ | __% |
| REST API 엔드포인트 | __/25 | __ | __% |
| 비즈니스 로직 | __/10 | __ | __% |
| DTO | __/11 | __ | __% |
| 테스트 코드 | __/14 | __ | __% |
| 문서화 | __/3 | __ | __% |
| **총합** | **__/76** | **__** | **__%** |

### 승인 조건

- [ ] 전체 완료율 **90% 이상**
- [ ] Critical 항목(🔴) 100% 완료
- [ ] 테스트 커버리지 80% 이상
- [ ] API 문서 반영 완료

---

## 📝 리뷰어 메모

**리뷰어:**  
**리뷰 일자:**  
**승인 여부:** ⬜ 승인 / ⬜ 수정 요청

### 코멘트:
```
(리뷰어 코멘트를 여기에 작성)
```

---

## 🔗 관련 문서

- [이슈 상세](./003-habit-management.md)
- [API 설계 규칙](../.cursor/rules/401-rest-api-design-rules.mdc)
- [JPA 규칙](../.cursor/rules/402-jpa-database-rules.mdc)
- [예외 처리 규칙](../.cursor/rules/403-exception-handling-rules.mdc)


