# SF2060 — 《2060》 (가제)

한국어 장편 하드 SF 소설 1권의 초고 집필 프로젝트.
**Paperclip 회사 `SF Novel Studio` (prefix `SFN`)** 가 본 리포지토리를 산출물 저장소로 사용한다.

## 작품 캐논 (단일 원천)

- **[`PREMISE.md`](PREMISE.md)** — 로그라인·톤·주제·하드 룰·미결정 사항 (01 편집장 단독 관리)
- **[`bible/SEED_세계관-2060.md`](bible/SEED_세계관-2060.md)** — 보드 직접 전달 세계관 시드 바이블 (2026-05-29). 변경 금지, 02가 추후 `bible/` 5문서로 분할.

모든 에이전트는 본 두 문서를 매 하트비트마다 숙지한다 ([docs/AGENTS_COMMON.md §1.1](docs/AGENTS_COMMON.md)).

## 디렉토리 구조

| 경로 | 소유 에이전트 | 용도 |
|------|--------------|------|
| `PREMISE.md` | 01 편집장 | 로그라인, 톤, 주제, 타깃 독자, 제약 조건 |
| `bible/` | 02 세계관 설계자 | 물리·사회·기술·연표·세력·지리 등 세계관 캐논 |
| `outline/` | 03 플롯 설계자 | 막 구조, 챕터 개요, 장면 비트, 복선 대장 |
| `characters/` | 04 캐릭터 담당 | 인물 시트, 관계도, 보이스 가이드 |
| `manuscript/` | 05 집필 작가 | 챕터별 원고 `chXX.md` (씬 단위 작성) |
| `reviews/` | 06 연속성·검수 | 정합성 리포트, `canon-ledger.md` |
| `style-guide.md` | 07 교정·윤문 | 어문 규범 준수 사항, 표기 통일 규칙 |
| `docs/` | 01 편집장 | 회사 운영 문서 (AGENTS, OPERATIONS, COMPANY_GOAL) |

## 주요 문서

- [회사 목표](docs/COMPANY_GOAL.md)
- [에이전트 공통 지시](docs/AGENTS_COMMON.md)
- [운영 가이드 (GitHub, PAT, 커밋)](docs/OPERATIONS.md)
- 에이전트별 지시: [01](docs/AGENTS_01.md) · [02](docs/AGENTS_02.md) · [03](docs/AGENTS_03.md) · [04](docs/AGENTS_04.md) · [05](docs/AGENTS_05.md) · [06](docs/AGENTS_06.md) · [07](docs/AGENTS_07.md)

## 보드(인간 작가) 인터페이스

회사와의 상호작용은 Paperclip 이슈 코멘트로 이루어진다.
보드(사용자)는 다음 게이트에서 명시적 승인을 한다:

1. **PREMISE 확정** — 시놉시스·기본 세계관 합의
2. **Bible 캐논 잠금** — 핵심 물리·사회·기술 규칙
3. **막별 outline 확정** — 막 1/2/3 각각
4. **챕터 승인** — 각 챕터별 최종 승인
