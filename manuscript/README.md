# manuscript/ — 챕터별 원고

**소유: [05 집필 작가](../docs/AGENTS_05.md)** (초고 작성)
**검수·교정 시 06·07이 수정** (정합성·문체)

## 파일 규약
- 챕터 단위: `chXX.md` (XX = 두 자리 챕터 번호, 예: `ch01.md`, `ch12.md`)
- 씬 분할 작업 중에는 `chXX/sceneNN.md` 또는 `chXX.draft.md` 사용 후 통합
- `chXX.draft.md`는 `.gitignore`로 커밋 제외

## 챕터 상단 메타 주석 (작가 작성)
```
<!--
chapter: 03
status: draft | review | revising | done
beats_covered: [b1, b2, b3]
canon_candidates:
  - "주인공이 X 행성에 처음 도착한 날짜는 2061-03-12"
  - "Y 인공지능의 정식 명칭은 ORINA-09"
open_questions:
  - "이 시점에 Z가 살아있는지 확인 필요 (06 검수 요청)"
-->
```

## 워크플로
1. 03이 챕터 비트 패킷 issue 생성, 05에게 할당
2. 05가 씬 단위로 분할 작성, 통합 후 commit
3. 06 검수 → 정합성 통과
4. 07 교정·윤문
5. 01 승인
