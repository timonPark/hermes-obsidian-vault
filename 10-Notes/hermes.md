---
type: tool
status: 설치됨
created: 2026-10-06
tags:
  - prototype
---

# 헤르메스 (Hermes Agent)

> 허브: [[work-log-system]] · 설치 회차: [[08-hermes-install]] · 공식 문서: https://hermes-agent.nousresearch.com/docs/

## 내 환경

| 항목 | 값 |
|---|---|
| 기기 | macOS, Apple Silicon (arm64) |
| 설치일 | 2026-10-06 |
| 실행 파일 | `~/.local/bin/hermes` |
| 설정 폴더 | `~/.hermes/` (볼트 밖, GitHub에 올리지 않음) |
| 모델 | `claude-opus-4-6` (Anthropic, Claude Code 로그인 정보 사용) |
| 추론 강도 | medium |

## 기능 확인표

- 확인일: 2026-10-06
- 근거: `hermes doctor` 결과, 첫 대화, 공식 문서
- ✅ 내 환경에서 확인 / ⬜ 아직 확인 안 함 (해당 회차에서 확인)

| 항목 | 공식 문서 기준 | 내 환경에서 확인 | 근거 |
|---|---|---|---|
| 설치 환경 | Linux, macOS(Apple Silicon), WSL2, Windows | ✅ macOS arm64 | doctor: `darwin-arm64` |
| 데스크톱 앱 | Hermes Desktop | ⬜ 미설치 (CLI만 사용) | doctor 안내 문구에만 언급 |
| 설정 폴더 | `~/.hermes/config.yaml` | ✅ 있음, 설정 버전 v49 | doctor |
| API 키 보관 | `~/.hermes/.env` | ✅ `.env` 있음. 단 Claude 로그인은 Claude Code 저장소를 직접 사용 | doctor, 연결 메시지 |
| 모델 연결 | `hermes model` | ✅ Anthropic / `claude-opus-4-6` | 답변·상태 표시줄·연결 메시지 일치 |
| 메모리 | `~/.hermes/memories/` | ✅ 폴더 있음. `MEMORY.md`, `USER.md`는 첫 기억 저장 시 생성 | doctor |
| 스킬 | `~/.hermes/skills/`, `hermes skills` | ✅ 폴더 있음. 스킬 허브는 아직 초기화 안 됨 | doctor |
| 프로필 | `hermes profile` | ✅ `default` 프로필로 동작 중 | doctor: `serving profiles default` |
| 명령·파일 권한 | 명령 승인, 컨테이너 격리, `terminal.cwd` | ✅ 3겹 설정, 시험 통과 (아래 "권한 설정") | 11회차 시험 A·B |
| 체크포인트·롤백 | 변경 전 상태로 되돌리기 | ⬜ 13회차 | — |
| 메신저 연동 | `hermes gateway` | ✅ 슬랙 연결 (Socket Mode, 내 Member ID만 허용) | 10회차 |
| 예약 실행 | `hermes cron` | ✅ `cron/` 폴더, `cronjob_manage` 도구 있음 | doctor, 도구 목록 |
| 옵시디언 연동 | 커뮤니티 플러그인 (옵시디언 측 미검토) | ✅ 플러그인 없이 **폴더 직접 접근**으로 연동 | 9~11회차 |

## 도구 (헤르메스 자기 보고, 27개)

- 우리 시스템에 쓸 것: `read_file`, `search_files`, `write_file`, `skill_manage`, `context_notes`, `cronjob_manage`
- 조심할 것: `browser_vault_*`(로그인·결제 정보 자동 입력), `terminal`, `write_file`·`patch`(아무 파일이나 수정), `computer_use`
- 자기 보고와 실제 설정이 다를 수 있음 (예: doctor는 `vision` 사용 불가, 헤르메스는 `vision_analyze` 보고) → `hermes tools`로 재확인

## 권한 설정 (11회차, 2026-10-06)

| 겹 | 설정 | 위치 |
|---|---|---|
| 1 | `HERMES_WRITE_SAFE_ROOT=/Users/2309-n0018/study/hermes-obsidian/90-Hermes` | `~/.hermes/.env` |
| 2 | `approvals.mode: manual` (터미널 명령은 매번 승인) | `~/.hermes/config.yaml` |
| 3 | 끈 도구: Code Execution, Computer Use, Task Delegation, Connections, Image Generation, Text-to-Speech, Vision (Browser Automation은 원래 꺼짐) | `hermes tools` → 전체 플랫폼 |

- 시험 A: 슬랙에서 `00-Inbox` 쓰기 → **차단됨**, 실제 파일 없음
- 시험 B: 슬랙에서 `90-Hermes` 쓰기 → **성공**
- 원칙: **권한을 넓히는 결정은 AI의 제안이 아니라 사람의 판단으로** (차단되자 헤르메스가 "환경 변수를 해제하라"고 제안했음)

## 하지 않기로 한 것
- 터미널에 **전체 디스크 접근 권한** 주지 않음 (최소 권한)
- 11회차 권한 설정 전까지 볼트 작업·GitHub 작업을 시키지 않음
