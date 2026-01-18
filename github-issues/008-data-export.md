# #008: 데이터 내보내기 및 공유

**Epic:** EPIC-6 (EXPORT_LOG)  
**Type:** Functional  
**Priority:** P2 (Medium)  
**Labels:** `epic:export`, `type:backend`  
**Related REQ:** REQ-FUNC-007, REQ-FUNC-010, REQ-FUNC-011  
**Dependencies:** #005  
**Parallelizable With:** #007, #006, #010  
**Blocks:** None

---

## 📋 Description

사용자의 습관 기록 데이터를 CSV/XLSX 형식으로 추출하여 내보낼 수 있는 기능을 구현합니다.

## 📌 Scope / Out of Scope

### In Scope
- CSV/XLSX 파일 생성 로직 구현
- 데이터 내보내기 API 구현
- 파일 다운로드 기능

### Out of Scope
- 클라우드 저장소 연동 (Post-MVP)
- 데이터 가져오기(Import) 기능 (Post-MVP)
- 실시간 동기화 (Post-MVP)

## 🎯 Goals

- CSV/XLSX 파일 생성 로직 구현
- 데이터 내보내기 API 구현
- 파일 다운로드 기능 구현

## 🛠️ Technical Stack

**Backend Core:**
- Java 21 LTS
- Spring Boot 4.0.1
- Spring Data JPA / Hibernate 7.2.0
- Gradle 9.2.1

**File Processing:**
- Apache Commons CSV (CSV 생성)
- Apache POI (XLSX 생성, 선택사항)

**API:**
- RESTful API (JSON)
- 파일 다운로드 (application/octet-stream)

**Testing:**
- JUnit 5
- Mockito
- Spring Boot Test

## ✅ Tasks

### TASK-EXPORT-SERVICE-01: Export Service
- [ ] `ExportService` 클래스 구현
- [ ] CSV 포맷 변환 로직 구현 (REQ-FUNC-007)
  - [ ] LogEntry 데이터를 CSV 문자열로 변환
  - [ ] 날짜 포맷팅 처리
  - [ ] 특수문자 처리 (쉼표, 따옴표 등)
- [ ] XLSX 포맷 변환 로직 구현 (선택사항)
  - [ ] Apache POI 또는 다른 라이브러리 사용
- [ ] 파일 생성 로직 구현
  - [ ] 임시 파일 생성
  - [ ] 파일명 규칙 정의 (날짜 포함)

### TASK-EXPORT-CONTROLLER-01: Export Controller
- [ ] `ExportController` 클래스 구현
- [ ] `GET /api/v1/export/csv` - CSV 파일 다운로드
  - [ ] 쿼리 파라미터: `startDate`, `endDate`, `habitId` (optional)
- [ ] `GET /api/v1/export/xlsx` - XLSX 파일 다운로드 (선택사항)
- [ ] 파일 다운로드 응답 헤더 설정
  - [ ] `Content-Type`, `Content-Disposition` 설정

### TASK-EXPORT-TEST-01: Export Tests
- [ ] `ExportService` 단위 테스트 작성
- [ ] CSV 변환 로직 테스트
- [ ] 파일 생성 로직 테스트
- [ ] `ExportController` API 테스트 작성

## 📝 Acceptance Criteria

- [ ] CSV 파일 다운로드 API가 정상 작동함
- [ ] 생성된 CSV 파일이 정상적으로 열림
- [ ] 데이터가 정확하게 변환됨
- [ ] 특수문자 처리가 정상 작동함
- [ ] 날짜 필터링이 정상 작동함
- [ ] 단위 테스트 커버리지 80% 이상
- [ ] API 문서(Swagger)에 정상 반영됨

## 🔗 Related Documentation

- [REST API 설계 규칙](.cursor/rules/401-rest-api-design-rules.mdc)
- [Task 문서](Tasks%20copy/Functional/008_Data_Export.md)

## 📡 API Specification

### GET /api/v1/export/csv - CSV 파일 다운로드

**Query Parameters:**
- `startDate` (String, 선택): 시작 날짜 (ISO 8601 형식, 예: `2025-01-01`)
- `endDate` (String, 선택): 종료 날짜 (ISO 8601 형식, 예: `2025-01-31`)
- `habitId` (Long, 선택): 습관 ID 필터

**Response:**
- `200 OK`: CSV 파일 (Content-Type: `text/csv`)
- `Content-Disposition: attachment; filename="habits_export_2025-01-15.csv"`

**CSV 파일 예시:**
```csv
id,habit_name,timestamp,text_note,duration,created_at
1,명상,2025-01-15T09:00:00,오늘도 좋은 하루 시작!,1800,2025-01-15T09:30:00
2,독서,2025-01-15T20:00:00,책 읽기 완료,3600,2025-01-15T21:00:00
```

## 🔄 Logic Steps (런타임 처리 순서)

### GET /api/v1/export/csv - CSV 파일 다운로드

**실행 순서:**
1. **HTTP Request 수신** (Controller)
   - `@GetMapping("/export/csv")` 핸들러 메서드 호출
   - Query Parameter `startDate`, `endDate`, `habitId` 추출

2. **Service 메서드 호출** (`ExportService.exportToCsv(startDate, endDate, habitId)`)

3. **읽기 전용 트랜잭션 시작** (`@Transactional(readOnly = true)`)

4. **데이터 조회** (Repository Layer)
   - `logEntryRepository.findByTimestampBetweenAndHabitId(startDate, endDate, habitId)` 실행
   - SQL: `SELECT * FROM log_entries WHERE timestamp BETWEEN ? AND ? AND habit_id = ?`

5. **데이터베이스 쿼리 실행** (Database)
   - MySQL/H2에서 쿼리 실행
   - 결과 반환

6. **CSV 변환** (Service Layer)
   - `LogEntry` 리스트를 CSV 문자열로 변환
   - 헤더 라인 생성: `id,habit_name,timestamp,text_note,duration,created_at`
   - 각 레코드를 CSV 형식으로 변환 (특수문자 처리)

7. **읽기 전용 트랜잭션 종료** (`@Transactional(readOnly = true)`)

8. **HTTP Response 생성** (Controller)
   - `ResponseEntity.ok().header("Content-Type", "text/csv").header("Content-Disposition", "attachment; filename=\"habits_export_" + date + ".csv\"").body(csvBytes)` 생성
   - `200 OK` 상태 코드와 함께 CSV 파일 반환

## 📊 Difficulty Assessment (난이도 평가)

### 전체 난이도: **중 (Medium)**

**단일 에이전트 작업 단위:** 이 이슈는 한 명의 개발자가 2-3일 내에 독립적으로 완료할 수 있는 작업 단위입니다.

### 세부 난이도 분석

| Task | 난이도 | 예상 시간 | 주요 작업량 | 비고 |
|------|--------|----------|------------|------|
| **TASK-EXPORT-SERVICE-01** | 중 (Medium) | 5-6시간 | CSV 변환 로직, 특수문자 처리 | 파일 포맷 처리 |
| **TASK-EXPORT-CONTROLLER-01** | 하 (Low) | 2-3시간 | 파일 다운로드 API 구현 | HTTP 헤더 설정 |
| **TASK-EXPORT-TEST-01** | 중 (Medium) | 3-4시간 | 단위/통합/API 테스트 작성 | 파일 생성 테스트 |

**총 예상 시간: 10-13시간 (2-3일)**

## 📌 Notes

- 이 Task는 #005 완료 후 시작해야 합니다 (LogEntry 데이터 필요).
- 파일은 서버 메모리에 임시로 생성하며, 다운로드 후 삭제합니다.
- 대량 데이터 처리 시 스트리밍 방식을 고려합니다.
- REQ-FUNC-011에 따라 외부 API 연동 없이 로컬에서만 처리합니다.

