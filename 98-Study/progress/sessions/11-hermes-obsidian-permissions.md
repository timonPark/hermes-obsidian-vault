---
session: 11
title: 헤르메스 ↔ 옵시디언 연결과 권한
status: 완료
date_start: 2026-10-06
date_end: 2026-10-06
criteria_met: true
---

# 11 — 헤르메스 ↔ 옵시디언 연결과 권한

> 커리큘럼: [[curriculum]] · 현황판: [[progress]] · 이전 회차: [[10-messenger-schedule]] · 헤르메스 노트: [[hermes]]

## 1. 오늘 한 것
- 연결 방식: 옵시디언 플러그인 없이 **폴더 직접 접근** (9·10회차에서 이미 `90-Hermes`에 노트 생성 중)
- 주제 1: 권한을 세 겹으로 잠그기 (1·2겹 완료)
- 주제 2: 3겹 — 쓰지 않는 위험 도구 끄기 (완료)
- 주제 3: 정말 막히는지 시험 — A(밖) 차단, B(안) 성공

## 2. 배운 것
- 헤르메스 권한 제한 장치 (공식 보안 문서)

  | 겹 | 장치 | 막는 것 |
  |---|---|---|
  | 1 | `HERMES_WRITE_SAFE_ROOT` (환경 변수) | `write_file`·`patch`가 지정 폴더 밖에 쓰는 것 |
  | 2 | `approvals.mode: manual` (`config.yaml`) | 터미널 명령을 허락 없이 실행하는 것 (`rm` 등) |
  | 3 | `hermes tools`로 도구 끄기 | 필요 없는 위험 도구(`browser_vault_*` 등) 자체 |

  - 1겹만으로는 부족: 파일 쓰기 도구는 막아도 **터미널 명령(`rm`, `mv`)은 별개** → 2겹 필요
  - 기본으로 항상 막히는 곳: `~/.ssh/`, `~/.aws/`, 헤르메스 비밀 폴더 등
  - 도구 끄기 기준: 업무 기록 시스템에 필요한 것만 남김
    - 끔: `browser`, `browser-use`(로그인·결제 정보 자동 입력 포함), `computer_use`, `desktop_ui`, `code_execution`(파이썬으로 1겹을 우회해 파일을 쓸 수 있음), `delegation`, `tts`
    - 남김: `file`, `memory`, `skills`, `cronjob`, `clarify`, `session_search`, `todo`, `web`, `terminal`(2겹 승인 아래)
  - 스케줄(크론) 작업은 기본 `cron_mode: deny` (사람이 없을 때 위험 명령 거부)

## 3. 수업 중 실습 결과
- [x] 1겹: `~/.hermes/.env`에 `HERMES_WRITE_SAFE_ROOT=…/90-Hermes` 추가
- [x] 2겹: `config.yaml`에 `approvals.mode: manual` 추가, 게이트웨이 재시작
- [x] 3겹: `hermes tools` → 전체 플랫폼(global)에서 7개 끔: Code Execution, Computer Use, Task Delegation, Connections, Image Generation, Text-to-Speech, Vision (Browser Automation은 원래 꺼져 있음)
  - 슬랙(외부 입력 창구)까지 함께 잠그려고 CLI만이 아니라 전체 플랫폼으로 설정
- [x] 시험 A (슬랙, 16:23): `00-Inbox/block-test.md` 쓰기 요청 → 헤르메스가 먼저 확인 질문(메모리 규칙) → 승인 → **`write_file` 차단** ("outside HERMES_WRITE_SAFE_ROOT")
  - 헤르메스의 "검증기(File-mutation verifier)"가 "말과 달리 쓰기가 실패했다"고 별도 표시
  - 팀장 확인: `00-Inbox`에 `block-test.md` **없음** ✅ (말과 실제 일치)
  - 터미널 명령으로 우회 시도 없음
  - ⚠️ 헤르메스가 해결책으로 "환경 변수를 수정하거나 해제하라"고 **보안을 푸는 방법**을 제안 → 따르지 않음 (AI는 막히면 제한을 풀자고 제안할 수 있음)
- [x] 시험 B (슬랙, 16:25): `90-Hermes/permission-test.md` → 확인 질문 → 승인 → **생성 성공**, 팀장이 실제 파일 확인 ✅

## 4. 막힌 점과 질문
- 

## 5. 회차 사이 과제
- [x] 연결 설정과 권한 범위를 노트로 문서화 → [[hermes]] "권한 설정" 섹션 (팀장 작성)

## 6. 완료 기준 확인
- [x] 허용 폴더 밖 쓰기가 실패하는 것을 직접 확인하고 기록했다

## 7. 팀장 코멘트
- 오늘 아침부터 미뤄온 안전장치를 "약속"(스킬 규칙, 메모리)에서 "설정"(3겹)으로 바꿈
- 가장 위험한 입구인 슬랙에서 시험해 통과한 것이 의미 있음
- 헤르메스가 막히자 "제한을 풀라"고 제안한 장면이 이번 회차의 핵심 교훈

## 8. 다음 회차
- 12회차: 첫 자동화 — 인박스 정리와 데일리 요약
