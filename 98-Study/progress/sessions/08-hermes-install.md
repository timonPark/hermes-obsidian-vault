---
session: 8
title: 헤르메스 설치, 모델 연결, 기능 확인
status: 완료
date_start: 2026-10-06
date_end: 2026-10-06
criteria_met: true
---

# 08 — 헤르메스 설치, 모델 연결, 기능 확인

> 커리큘럼: [[curriculum]] · 현황판: [[progress]] · 이전 회차: [[07-agent-concepts-security]]

## 1. 오늘 한 것
- 주제 1: 헤르메스 설치 (공식 설치 문서 기준) — 완료
- 주제 2: 첫 대화와 실행·종료
- 주제 3: 기능 확인표 → [[hermes]] 노트에 정리

## 2. 배운 것
- 공식 설치 (macOS): `curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`
  - macOS는 **Apple Silicon 전용** (Intel 미지원) → `uname -m`이 `arm64`인지 먼저 확인
  - 설치 위치: 실행 파일 `~/.local/bin/hermes`, 소스 `~/.hermes/hermes-agent/`, 사용자 데이터 `~/.hermes/`
  - 설치 후: `source ~/.zshrc` → `hermes doctor`로 점검
- 모델 연결 방식 (학습자 결정): 초반은 헤드리스 — 이 연결은 학습자가 직접 구성, 팀장은 안내하지 않음. 대안으로 헤르메스 공식 구독 로그인(ChatGPT 구독, GitHub Copilot) 안내

## 3. 수업 중 실습 결과
- [x] `uname -m` → `arm64` 확인 (doctor 결과의 `darwin-arm64`로 확인)
- [x] 설치 스크립트 실행
- [x] `hermes doctor` 결과 확인 — 설치 정상
  - Python 3.14.7, `~/.local/bin/hermes`, `~/.hermes/`(skills, memories, sessions, logs, cron, SOUL.md) 생성
  - 경고 4건: 선택 기능(브라우저 도구, 웹·TUI 작업공간)의 npm 취약점 3건(업스트림 수정 대기, 로컬 조치 무의미) + API 키 미설정
  - 주의 사항
    - doctor가 "전체 디스크 접근 권한"을 터미널에 주라고 권함 → **주지 않음** (최소 권한 원칙)
    - 이미 백그라운드 게이트웨이 프로세스가 떠 있음 (`the host gateway ... serving profiles default`)
    - GitHub가 `gh` CLI로 **전체 권한 인증**된 상태로 인식됨 → 헤르메스가 GitHub를 조작할 수 있음
    - `computer_use`, `desktop_ui`, `terminal`, `file` 등 강력한 도구가 기본 활성 → 11회차에서 범위 제한
    - "API key or custom endpoint configured" ✓ 표시 → 학습자 확인: **설치 중 직접 입력함** (내용은 공유하지 않음)
- [x] `ls -a ~ | grep hermes` → `.hermes` 생성 확인 (6회차에는 없었음)
- [x] 모델 연결: `hermes` 첫 실행 시 제공자 선택 → 학습자가 Anthropic(Claude Code) 선택, 기본 모델 `claude-opus-4-6`
  - ⚠️ 연결 과정에서 화면에 출력된 **장기 OAuth 토큰(유효 1년)을 대화창에 그대로 붙여넣음** → 즉시 폐기 안내 (토큰 값은 어디에도 기록하지 않음)
- [x] 첫 대화
  - Q1 모델: `claude-opus-4-6` (Anthropic) — 답변·상태 표시줄·연결 메시지 세 곳이 일치하는지 교차 확인
  - Q2 도구: 기본 22개 + 필요 시 불러오는 도구 5개 = 27개 (헤르메스 자기 보고)
    - 고위험: `browser_vault_*`(저장된 로그인·**결제 정보** 자동 입력), `terminal`, `write_file`·`patch`(아무 파일이나 수정), `computer_use`(데스크톱 조작)
    - 우리 시스템에 쓸 것: `read_file`, `search_files`, `write_file`(90-Hermes 한정), `skill_manage`, `context_notes`(메모리), `cronjob_manage`
    - 교차 확인: doctor에서는 `vision`이 "사용 불가"였는데 헤르메스는 `vision_analyze`를 목록에 넣음 → 자기 보고는 `hermes tools`로 재확인 필요
- [x] 기능 확인표 채우기 → [[hermes]] (13개 중 9개 확인, 4개는 해당 회차에서: 데스크톱 앱 미설치, 권한 11, 체크포인트 13, 옵시디언 연동 11)
- [x] `/exit`로 종료

## 4. 막힌 점과 질문
- 설치 중 GitHub 저장소 내려받기(clone) 단계에서 멈춘 것처럼 보임 → `du -sh ~/.hermes/hermes-agent`로 진행 여부 확인 안내. 이후 `.hermes` 생성 확인

## 5. 회차 사이 과제
- [ ] 일주일 사용 비용(또는 구독 사용량) 기록

## 6. 완료 기준 확인
- [x] 헤르메스를 실행·종료할 수 있다
- [x] 기능 확인표를 채웠다 (지금 확인 가능한 9개 완료, 나머지 4개는 해당 회차 과제로 — 역할 규칙 8번)

## 7. 팀장 코멘트
- 설치·연결·첫 대화까지 완료. AI의 자기 보고를 다른 근거(상태 표시줄, doctor)와 맞춰 보는 습관을 처음 실천
- 헤르메스에는 기본으로 강력한 도구가 많이 켜져 있음 → 11회차 권한 설정 전까지는 대화·스킬 연습만

## 8. 다음 회차
- 9회차: 메모리, 스킬, 도구, 프로필
