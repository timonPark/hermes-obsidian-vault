# hermes-obsidian 학습 폴더 안내

헤르메스 & 옵시디언 학습 자료를 모아두는 폴더입니다.

## 다시 시작할 때 읽는 순서

1. [[project-context]] — 왜 배우는지, 지금 어디까지 왔는지, 다음에 할 일
2. [[progress]] — 회차별 진행 현황과 시간순 기록
3. [[curriculum]] — 전체 커리큘럼 (최신)
4. [[team-lead-role-rule]] — 팀장 역할과 진행 규칙

## 폴더 구조

```
hermes-obsidian/                  ← 옵시디언 볼트
├── README.md                     ← 지금 보고 있는 안내 문서
├── 00-Inbox/                     ← 정리 전 노트 (새 노트 기본 위치)
├── 10-Notes/                     ← 정리된 노트 (허브: work-log-system)
├── 20-Daily/                     ← 일일 노트
├── 30-Raw/                       ← 원본 보관 (고치지 않음)
│   └── work-logs/
├── 90-Hermes/                    ← 헤르메스 작업 공간 (11회차부터)
├── 98-Study/                     ← 학습 자료 (헤르메스 접근 제외 예정)
│   ├── context/project-context.md   ← 학습 배경과 현재 상황 (가장 먼저 읽기)
│   ├── role/team-lead-role-rule.md  ← 팀장 역할 규칙
│   ├── curriculum/                  ← 커리큘럼 (curriculum.md = 최신, archive/ = 지난 버전)
│   ├── review/                      ← 커리큘럼 검토 문서
│   ├── reference/                   ← 외부 자료 분석
│   └── progress/                    ← 진행 현황판(progress.md), 기록 양식, 회차별 기록(sessions/)
└── 99-System/                    ← 설정용
    ├── templates/                   ← 템플릿 (work-log, daily)
    └── attachments/                 ← 첨부파일
```

**번호 순서 = 자주 쓰는 순서.** 매일 쓰는 폴더가 위, 거의 안 여는 폴더가 아래.

## 이름 규칙

1. **폴더는 문서 종류로 나눕니다.** 역할(role), 커리큘럼(curriculum), 검토(review), 학습 노트 등
2. **최신 문서는 이름을 바꾸지 않습니다.** `curriculum.md`는 항상 최신본입니다. 이름이 고정돼야 링크가 깨지지 않습니다.
3. **지난 버전은 `archive/`에 `-v번호`를 붙여 보관합니다.** 예: `curriculum-v1.md`
4. **검토 문서는 `검토대상-버전-review` 형식으로 짓습니다.** 예: `curriculum-v1-review.md`
5. **파일명은 영문 소문자와 하이픈(-)을 씁니다.** 터미널과 Git에서 다루기 편합니다.
6. **현재 버전은 문서 안에 적습니다.** 제목과 맨 아래 개정 이력을 확인하세요.
7. **진행 기록은 `98-Study/progress/`에 쌓습니다.** 회차별 기록은 `두자리회차-주제.md` 형식입니다. 예: `00-orientation.md`
8. **기록은 추가만 하고 지난 내용은 고치지 않습니다.** 정정이 필요하면 새 기록으로 남깁니다.

## 현재 상태

| 문서 | 현재 버전 | 비고 |
|---|---|---|
| 커리큘럼 | v3 | v2 검토 의견 반영 (폴더 경로만 2026-10-06 갱신) |
| 팀장 역할 규칙 | v1 | |

---
*작성: 2026-10-06*
