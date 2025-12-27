# #008: 데이터 내보내기 및 공유

**Epic:** EPIC-6 (EXPORT_LOG)  
**Type:** Functional  
**Priority:** P2 (Medium)  
**Labels:** `epic:export`, `type:backend`  
**Related REQ:** REQ-FUNC-007, REQ-FUNC-010, REQ-FUNC-011  
**Dependencies:** #005  
**Blocks:** None

---

## 📋 Description

사용자의 습관 기록 데이터를 CSV/XLSX 형식으로 추출하여 내보낼 수 있는 기능을 구현합니다.

## 🎯 Goals

- CSV/XLSX 파일 생성 로직 구현
- 데이터 내보내기 API 구현
- 파일 다운로드 기능 구현

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

## 📌 Notes

- 이 Task는 #005 완료 후 시작해야 합니다 (LogEntry 데이터 필요).
- 파일은 서버 메모리에 임시로 생성하며, 다운로드 후 삭제합니다.
- 대량 데이터 처리 시 스트리밍 방식을 고려합니다.
- REQ-FUNC-011에 따라 외부 API 연동 없이 로컬에서만 처리합니다.

