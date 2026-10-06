---
session: 5
title: 볼트 설계, Git, 백업, 동기화
status: 진행 중
date_start: 2026-10-06
date_end: 
criteria_met: false
---

# 05 — 볼트 설계, Git, 백업, 동기화

> 커리큘럼: [[curriculum]] · 현황판: [[progress]] · 이전 회차: [[04-properties-templates-daily]]

## 1. 오늘 한 것
- 주제 1: 볼트 구조 점검과 재배치
- 주제 2: Git, 백업, 동기화의 차이
- 주제 3: `.gitignore`와 첫 커밋 (학습자 Git 경험 있음 → 기본 설명 생략)
- 주제 4: 일부러 망가뜨리고 Git으로 복구
- 주제 5: Git 외 백업

## 2. 배운 것
- 백업을 시작하기 전에 구조부터 정리한다 (나중에 옮기면 변경 기록이 지저분해짐)
- 성격이 다른 폴더(학습 자료 / 업무 시스템 / 설정)가 한 층에 섞이면, 헤르메스가 업무 질문에 학습 기록을 근거로 답할 위험
- **번호 순서 = 자주 쓰는 순서**: `00-Inbox` → `10-Notes` → `20-Daily` → `30-Raw` → `90-Hermes` → `98-Study` → `99-System`
- 학습 자료를 `98-Study` 하나로 묶으면 헤르메스 접근 제외를 한 줄로 설정 가능
- Git·백업·동기화의 차이

  | | 막아주는 사고 |
  |---|---|
  | Git | 잘못 고침 (실수, AI의 엉뚱한 수정) |
  | 백업 | 통째로 날아감 (고장, 분실) |
  | 동기화 | 막지 않음 (실수도 그대로 복사) |

  - Git 기록(`.git`)은 볼트 안에 있어 노트북이 고장 나면 함께 사라짐 → 별도 백업 필요
  - 헤르메스가 노트를 고치기 시작하면(11회차) Git으로 "무엇을 바꿨는지" 보고 되돌림 (13회차 장애 훈련)
- `.gitignore` (볼트 최상위, 팀장이 작성): 비밀정보, 화면 상태·캐시, OS 파일, 대용량 미디어 제외

## 3. 수업 중 실습 결과
- [x] 볼트 구조 재배치 (학습자 승인 후 팀장이 실행)
  - `raw` → `30-Raw`, 학습 자료 6개 폴더 → `98-Study`, `attachments`·`templates` → `99-System`
  - 설정 경로 갱신: 첨부파일(`99-System/attachments`), 템플릿 폴더(`99-System/templates`), 일일 노트 템플릿(`99-System/templates/daily`)
  - 현재 문서의 경로 갱신: README, 팀장 역할 규칙, project-context, curriculum. **지난 기록(회차 기록, 진행 기록)은 당시 경로 그대로 둠**
  - 옵시디언 재시작 후에도 새 설정 경로 유지 확인 ✅, 빈 `raw` 폴더 삭제 ✅
- [x] `git init` → 첫 커밋 `b634e50` "볼트 초기 구조: 학습 0~4회차, 업무 기록 설계 v1" (파일 34개, `workspace.json`·`.DS_Store` 제외 확인)
- [x] `work-log-schema.md`를 일부러 망가뜨리고(규칙 삭제, `결정`→`확정`) `git diff`로 확인 → `git restore`로 복구 ✅ (복구 후 변경 없음 확인)
- [x] `git check-ignore -v`: `test.env` → `.gitignore:3:*.env`, `.DS_Store` → `.gitignore:18:.DS_Store`

## 4. 막힌 점과 질문
- 

## 5. 회차 사이 과제
- [ ] Git과 별개의 백업 방법 하나를 정해 적용
- [ ] 첨부파일 관리 기준을 볼트 `README.md`에 기록

## 6. 완료 기준 확인
- [x] 잘못 수정한 노트를 Git으로 복구했다
- [x] `git check-ignore -v`로 `.env` 테스트 파일과 `.DS_Store`가 제외되는 것을 확인했다
- [ ] Git 외 백업 1개를 갖췄다

## 7. 팀장 코멘트
- 

## 8. 다음 회차
- 6회차: 터미널과 파일 경로
