---
session: 12
title: 첫 자동화 — 검토 흐름과 데일리 요약
status: 진행 중
date_start: 2026-10-06
date_end: 
criteria_met: false
---

# 12 — 첫 자동화: 검토 흐름과 데일리 요약

> 커리큘럼: [[curriculum]] · 현황판: [[progress]] · 이전 회차: [[11-hermes-obsidian-permissions]] · 설계: [[work-log-schema]]

## 1. 오늘 한 것
- 주제 1: 검토(승인) 흐름 만들기

## 2. 배운 것
- 우리 시스템의 자동화 흐름 = **입력 → 처리 → 승인 → 반영**

  | 단계 | 누가 | 어디서 |
  |---|---|---|
  | 입력 | 나 | 슬랙 메시지 |
  | 처리 | 헤르메스 | `work-log` 스킬 → `90-Hermes/`에 노트 (`reviewed: false`) |
  | 승인 | 나 | 원문과 대조 → 고칠 것 고치기 → `reviewed` 체크 |
  | 반영 | 나 | `10-Notes/`로 이동 + Git 커밋 |

  - 승인된 노트를 `10-Notes`로 옮기면 헤르메스는 더 이상 고칠 수 없음 (1겹 권한 밖) → **확정된 기록 보호**
- 일일 노트 템플릿에 "검토 대기" 검색 블록 추가: `path:90-Hermes [reviewed:false]`

## 3. 수업 중 실습 결과
- [x] 검토 대기 목록 확인
- [x] 기록 검토 → 승인 → `10-Notes`로 이동: 1건 안내했으나 **4건 모두** 처리, `permission-test.md` 삭제
  - `customer-meeting-prep`: `project: [[고객미팅]]` 보완, `reviewed: true` ✅
  - ⚠️ 발견: `b-feature-launch-date`(B 기능 출시일)와 `inbox-cleanup-proposal`(인박스 비우기 제안)에도 `project: [[고객미팅]]`이 들어감 → 원문과 무관한 값 (복사해 붙인 것으로 보임)
  - 학습자가 수정: `b-feature-launch-date` → `[[B기능]]`, `inbox-cleanup-proposal` → 비움 ✅
  - 링크를 클릭하면서 `00-Inbox/고객미팅.md`(프로젝트 허브 노트)가 생김
  - 교훈: **사람의 검토도 틀릴 수 있다.** 승인 단계에서 오히려 틀린 값이 들어가면 "확인된 기록"이라 더 믿게 되어 위험

## 4. 막힌 점과 질문
- 

## 5. 회차 사이 과제
- [ ] 실제 업무 메모로 5~7일 사용하고, 이상한 결과를 모두 기록

## 6. 완료 기준 확인
- [ ] 테스트 기록을 검토·승인·반영(diff 확인 후 커밋)했다
- [ ] 데일리 요약 스케줄을 정각 기준으로 등록했다

## 7. 팀장 코멘트
- 

## 8. 다음 회차
- 13회차: 장애 훈련
