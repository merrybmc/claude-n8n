# n8n MCP 서버 - 21개 도구 카탈로그

## 1. 워크플로우 생명주기
- 워크플로우 CRUD 과정 담당

- **health_check**: n8n 서버가 살아있는지 확인
- **n8n_create_workflow**: 워크플로우 생성
- **n8n_list_workflow**: 워크플로우 전체목록 조회
- **n8n_get_workflow**: 특정 워크플로우 상세정보 조회
- **n8n_update_full_workflow**: 워크플로우 전체를 새 내용으로 교체
- **n8n_update_partial_workflow**: 워크플로우 일부 수정
- **n8n_delete_workflow**: 워크플로우 삭제
- **n8n_workflow_versions**: 워크플로우 변경이력 확인

## 2. 워크플로우 검증 및 테스트
- 워크플로우를 만들기 전에 미리 점검, 생성 후에 실행, 문제가 발생하면 고치는 역할

- **validate_workflow**: 워크플로우의 연결 구조가 올바른지 검증
- **n8n_validate_workflow**: n8n 서버에서 직접 워크플로우를 검증
- **validate_node**: 개별 노드 설정 확인 
- **n8n_autofix_workflow**: 검증에서 에러가나면 자동으로 수정 시도
- **n8n_test_workflow**: 워크플로우 테스트 실행 // ex "이 workflow를 테스트 해줘"

## 3. 실행 및 데이터

- **n8n_execution**: 워크플로우 실행 이력 조회 // ex. "오늘 아침에 workflow 정상 실행 되었어?"
- **n8n_manage_datatable**: n8n 내부 데이터 테이블 관리

## 4. 노드 및 템플릿

- **search_node**: 키워드로 필요한 노드 검색 // ex "이메일 전송 관련 노드 찾아줘"
- **get_node**: 특정 노드의 상세 정보, 어떤 설정값이 필요한지 확인
- **search_templates**: n8n 템플릿 라이브러리에서 기존 워크플로우 템플릿 검색
- **get_template**: 템플릿 상세 정보 조회
- **deploy_template**: 템플릿 복제

## 5. 참조

- **tools_documentation**: 21개 도구 각각의 상세 사용법 문서 조회

## 6. 도구 사용 예시
- 1. search_nodes: 필요한 노드 검색
- 2. get_nodes: 노드 상세 설정값 파악
- 3. validate_workflow: 노드 연결 구조 검증, 오류 사전 차단
- 4. n8n_create_workflow: 검증 통과한 워크플로우 생성
- 5. n8n_test_workflow: 생성된 워크플로우 테스트 실행

## 7. 워크플로우 생성 6단계 프로세스
- 모듈에 이 6단계를 적어두면 Claude Code가 매번 새로 짜지 않고 템플릿처럼 가져와서 작업 가능

- 1. 요청분석 : 사용자가 요청 파악 (Claude 판단)
- 2. 노드탐색 및 수집 : search_node, get_node로 필요한 노드 찾고 설정값 확인
- 3. 구조설계 및 검증 : validate_workflow로 연결구조 검증, 오류 수정
- 4. 생성 : n8n_create_workflow로 워크플로우 생성 
- 5. 테스트 : n8n_test_workflow로 테스트 실행 (Claude 판단)
- 6. 결과피드백 : n8n_execution으로 결과 확인 (Claude 보고)

## 8. 안전장치 생성 프로세스
- 1. 생성 (create)
    - 노드 구조 사전점검 
    - 필수 설정 누락탐지
- 2. 검증 (validate)
    - 검증 통과 후 실제 실행
- 3. 자동 수정 (autofix)
- 4. 테스트 (test)
- 5. 결과피드백 (execution)
    - 성공: 이름, URL, 노드 구성 등
    - 실패: 에러 노드, 원인, 해결 방법