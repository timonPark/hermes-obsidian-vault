---
session: 10
title: 메신저 연결과 스케줄
status: 완료
date_start: 2026-10-06
date_end: 2026-10-06
criteria_met: true
---

# 10 — 메신저 연결과 스케줄

> 커리큘럼: [[curriculum]] · 현황판: [[progress]] · 이전 회차: [[09-memory-skills-tools]] · 헤르메스 노트: [[hermes]]

## 1. 오늘 한 것
- 주제 1: 슬랙 앱 만들기 (공식 문서 순서) — 완료
- 주제 2: 연결 정보 넣기 (토큰 2개, Member ID, `hermes gateway setup`) — 완료
- 주제 3: 슬랙에서 첫 대화 — 완료 (슬랙 → 스킬 → 저장 성공)
- 주제 4: 스케줄(예약 실행) — 등록·확인·즉시 실행·슬랙 수신 완료. 16:59 자동 실행 확인 후 삭제 예정

## 2. 배운 것
- 헤르메스 슬랙 연결 순서 (공식 문서)
  1. `hermes slack manifest --agent-view --write` → `~/.hermes/slack-manifest.json`
  2. api.slack.com/apps → Create New App → **From an app manifest** → 워크스페이스 선택 → JSON 붙여넣기
  3. Socket Mode 켜기 → 앱 토큰(`xapp-`, `connections:write`) 생성
  4. Install App → 봇 토큰(`xoxb-`)
  5. 내 Member ID (`U...`)
  6. `hermes gateway setup` → 토큰은 **터미널에만** 입력 (`~/.hermes/.env`에 저장)
  7. 게이트웨이 시작·재시작
- Socket Mode: 헤르메스가 슬랙에 먼저 연결하는 방식이라 내 컴퓨터를 인터넷에 열 필요 없음
- `SLACK_ALLOWED_USERS` 필수: 지정한 사람의 메시지만 처리 (없으면 모두 거부)
- DM은 모든 메시지에 응답, 채널에서는 `@멘션`할 때만 응답
- 스케줄 (공식 문서): 만들기 `hermes cron create "<일정>" "<할 일>"` 또는 대화로 부탁 / 목록 `hermes cron list` / 즉시 실행 `hermes cron run <id>` / 기록 `hermes cron runs <id>` / 삭제 `hermes cron remove <id>`
  - 일정 형식: `in 30m`, `every 2h`, `every monday 9am`, `0 9 * * *`
  - 결과는 지정한 곳(슬랙 등)으로 전달, **게이트웨이가 켜져 있어야 동작**
  - 시간대 처리는 공식 문서에 명시 없음 → 등록 후 `list`에서 실제 실행 시각 확인 필요
- 슬랙에서는 `/`로 시작하는 입력을 슬랙 자체 명령으로 가로챔 → `/work-log` 대신 "work-log 스킬로 기록해 줘: ..."처럼 말로 부름

## 3. 수업 중 실습 결과
- [x] 슬랙 DM으로 스케줄 등록 → `hermes cron list` 확인 (id `77362c983695`)
- [x] `hermes cron run`으로 즉시 실행 → 슬랙 수신 ✅ (전달 경로 정상)
- [x] **17:07 자동 실행 확인** — 수동 실행 없이 스케줄대로 슬랙에 "정각 알림 테스트" 도착 ✅
- [x] `hermes cron remove 77362c983695` → 목록에서 삭제 확인
- [x] 매니페스트 생성 (`pbcopy`로 복사)
- [x] 슬랙 앱 생성 (From an app manifest)
- [x] Socket Mode 앱 토큰, 워크스페이스 설치(봇 토큰), Member ID
- [x] `hermes gateway setup`으로 연결 정보 입력 (토큰은 터미널에만 입력)
- [x] 게이트웨이 재시작, 슬랙 DM으로 첫 대화
- [x] **슬랙에서 스킬 실행 → 승인 → 저장 성공** (15:49): `90-Hermes/2026-10-06-customer-meeting-prep.md`
  - `source: slack` ✅, `type: 지시` ✅, `due: 2026-10-13` ✅ ("다음 주 화요일" 정확), `people: [[김팀장]]` ✅, 원문 그대로 ✅
  - 작은 차이: `project` 칸이 빈칸이 아니라 **아예 빠짐** → 스킬 개선 후보 (속성 8개를 항상 유지)
  - 학습자는 "저장이 안 된 것 같다"고 느낌 → 실제로는 저장됨. 옵시디언 파일 목록에서 `90-Hermes` 폴더가 접혀 있었거나 갱신 전이었을 가능성

## 4. 막힌 점과 질문
- **스케줄이 정각(16:00)에 안 옴** → 증거로 원인 찾기
  - 슬랙 요청: "매시간 **정각**에 '정각 알림 테스트'라고 보내줘" (16:00 전 등록)
  - `hermes cron list` 결과: `Schedule: every 60m`, `Next run: 16:59:25`, `Deliver: origin`
  - 원인: 헤르메스가 "매시간 정각"(`0 * * * *`)을 **"60분마다"(`every 60m`)로 바꿔 등록** → 첫 실행이 등록 시각 + 60분
  - 7회차 "맥락 착각"의 실제 사례. 자연어로 스케줄을 만들면 **반드시 `list`로 일정 표현을 확인**한다
  - 정각이 필요하면 크론 표현식으로 직접 등록: `hermes cron create "0 * * * *" "..."`
- **추가 발견 (16:59)**: 다음 실행이 16:59 → **17:06**으로 바뀜
  - 원인: 16:06에 `hermes cron run`으로 수동 실행 → "60분마다"는 **마지막 실행 시각 기준**이라 일정이 밀림
  - 시계 기준(`0 * * * *`)이면 수동 실행과 무관하게 정각에 실행 → 정해진 시각이 중요한 작업은 크론 표현식으로

## 5. 회차 사이 과제
- [ ] 스케줄이 예정대로 실행됐는지 3일간 기록 → 12회차 데일리 요약 스케줄로 진행

## 6. 완료 기준 확인
- [x] 스케줄을 등록·확인·삭제했다
- [x] 실행 기록을 확인했다 (`list`의 Last run, Execution: completed)

## 7. 팀장 코멘트
- 슬랙 연결로 "입력만 하면 알아서 관리"가 실제로 동작
- 스케줄에서 AI의 해석 오류("정각" → "60분마다")와 수동 실행에 따른 일정 밀림을 직접 겪고 원인을 증거로 찾음 → 13회차 장애 훈련의 예행연습

## 8. 다음 회차
- 11회차: 헤르메스 ↔ 옵시디언 연결과 권한
