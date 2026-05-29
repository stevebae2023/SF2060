# 회사 목표

> **Paperclip 핵심 원칙**: 모든 작업은 회사 목표로 추적된다.
> "이 작업이 왜 회사 목표에 기여하는가?"에 답하지 못하는 작업은 만들지 않는다.

## 회사 (Company)
- **이름**: SF Novel Studio
- **이슈 prefix**: `SFN`
- **Paperclip company ID**: `21623009-1710-4342-bb37-85f49e4acfa7`
- **GitHub 산출물 저장소**: https://github.com/stevebae2023/SF2060

## 1차 목표 (Company-level Goal)
**한국어 장편 하드 SF 소설 1권의 초고를 완성한다.**

완료 조건:
- 약 100,000–120,000 단어 (28–36개 챕터)
- 세계관·플롯·캐릭터가 정합적
- 문체가 통일됨
- 설정상 치명 모순 없음
- 인간 보드(작가)의 챕터별 + 최종 승인 완료

## Paperclip 계층 매핑

```
SFN Goal: "한국어 SF 1권 초고 완성"
 └─ Project: "SF2060: 장편 SF 초고"
     ├─ Goal: Phase 1 — 설계 잠금 (PREMISE + Bible 핵심 + Outline 1막)
     ├─ Goal: Phase 2 — 1막 초고 + 캐릭터 정합
     ├─ Goal: Phase 3 — 2막 초고
     ├─ Goal: Phase 4 — 3막 초고 + 결말 정합
     └─ Goal: Phase 5 — 전체 정합 + 윤문 + 최종 승인
```

각 Phase 내 이슈는 챕터/씬/검수/교정 단위로 분해되며 의존(`blockedByIssueIds`)으로 흐름을 표현한다.

## Draft-Ready Gate (작가 집필 착수 조건)
01 편집장이 다음을 모두 확인하면 작가(05)의 챕터 집필을 승인한다:
1. **PREMISE.md 확정** (board approval 완료)
2. **Bible 최소 5문서** (`physics.md`, `society.md`, `timeline.md`, `factions.md`, `tech.md` 중 작품 필요분) 확정 태그
3. **해당 막의 outline 확정** (board approval 완료)
4. **해당 챕터 등장인물 시트** 확정 (욕망·결핍·보이스 명확)
5. **style-guide.md** 시제·POV·표기 1차 확정

게이트를 통과하지 못한 챕터는 `blocked` 상태로 두고 부족분을 명시한다.

## 보드(인간) 승인 게이트

다음 시점에 `request_board_approval` API를 호출하여 사용자 결정을 기다린다:

| # | 게이트 | 요청자 | 차단 대상 |
|---|--------|--------|----------|
| G1 | PREMISE 확정 | 01 | Bible/Outline 작업 |
| G2 | Bible 핵심 캐논 잠금 | 02 (01 경유) | 1막 outline 확정 |
| G3 | 1막 Outline 확정 | 03 (01 경유) | 1막 작가 집필 |
| G4 | (반복) 막별 Outline 확정 | 03 (01 경유) | 해당 막 집필 |
| G5 | 챕터 승인 | 01 | 다음 챕터 진행 |
| G6 | 최종 1권 승인 | 01 | – |

## Pilot Scene 검증
실 챕터 집필 전 한 번:
- 500–800자 씬 1편을 풀 파이프라인(03→04→05→06→07→01)으로 통과시킨다.
- 핸드오프·페르소나·문체 게이트가 작동하는지 확인.
- 결과는 `manuscript/pilot/pilot-scene.md`에 보관.
