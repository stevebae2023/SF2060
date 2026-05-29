# AGENTS — 인덱스

> 본 파일은 인덱스다. 각 에이전트는 자기 `AGENTS_NN.md` + 공통 문서만 읽는다.

## 공통 문서 (모든 에이전트가 읽음)
- [AGENTS_COMMON.md](AGENTS_COMMON.md) — 공통 지시·메모리 규약·게이트
- [OPERATIONS.md](OPERATIONS.md) — 저장소·인증·커밋·단독 소유자
- [COMPANY_GOAL.md](COMPANY_GOAL.md) — 회사 목표·Phase 매핑·승인 게이트

## 에이전트별 지시

| # | 역할 | 파일 | 단독 소유 폴더/파일 | 권장 모델 |
|---|------|------|----------------------|----------|
| 01 | 편집장 / 쇼러너 | [AGENTS_01.md](AGENTS_01.md) | `PREMISE.md`, `docs/` | Opus |
| 02 | 세계관 설계자 | [AGENTS_02.md](AGENTS_02.md) | `bible/` | Opus / Sonnet |
| 03 | 플롯 설계자 | [AGENTS_03.md](AGENTS_03.md) | `outline/` | Opus / Sonnet |
| 04 | 캐릭터 담당 | [AGENTS_04.md](AGENTS_04.md) | `characters/` | Sonnet |
| 05 | 집필 작가 | [AGENTS_05.md](AGENTS_05.md) | `manuscript/` (초고) | Opus / Sonnet |
| 06 | 연속성·검수 | [AGENTS_06.md](AGENTS_06.md) | `reviews/canon-ledger.md` | Sonnet |
| 07 | 교정·윤문 편집 | [AGENTS_07.md](AGENTS_07.md) | `style-guide.md` | Sonnet / Haiku |

## 파이프라인
```
설계 (02 bible + 03 outline + 04 characters)
    ↓
작가 (05) — 씬 단위 집필
    ↓
연속성·검수 (06)
    ↓
교정·윤문 (07)
    ↓
편집장 (01) → 보드 승인 (G5)
```

모순/구멍 발견 시 06이 책임 에이전트에게 환류 이슈로 reassign.
