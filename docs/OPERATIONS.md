# Operations Guide

본 문서는 SF2060 회사의 운영 인프라(저장소, 인증, 커밋 규약, 로컬 워크스페이스)를 정리한다.
모든 에이전트는 매 하트비트 시작 시 자기 `AGENTS_NN.md`와 함께 본 문서를 참조한다.

## 1. 로컬 워크스페이스

- **경로**: `/home/softcamp/SF2060_workspace`
- **Git remote**: `https://github.com/stevebae2023/SF2060` (private)
- **default branch**: `main`

에이전트는 작업 전 항상 `cd /home/softcamp/SF2060_workspace && git pull --ff-only origin main`으로 최신화한다.

## 2. GitHub 인증

- PAT는 **로컬 파일 `/home/softcamp/.config/sf2060/git-credentials`** 에 저장 (chmod 600).
- 본 워크스페이스의 `git` 명령은 `credential.helper=store --file=…` 설정으로 자동 인증.
- **PAT를 절대 리포지토리에 커밋하지 말 것.** 코멘트·코드·문서·attachment 어디에도 노출 금지.
- PAT가 노출되거나 의심 시 즉시 보드에 보고하고 사용자가 GitHub에서 회수(revoke) 후 재발급.

## 3. 커밋 규약

### 3.1 작성자 식별
- 기본 `user.name=SF2060 Bot`, `user.email=sf2060-bot@paperclip.ing` (이미 설정됨)
- 에이전트가 자기 이름을 commit author에 반영하고 싶으면 `git -c user.name="<agent name>" -c user.email="<role>@paperclip.ing" commit ...` 형태로 사용

### 3.2 메시지 형식
```
<scope>: <한 줄 요약>

<선택: 자세한 설명>

Issue: SFN-NN
Co-Authored-By: Paperclip <noreply@paperclip.ing>
```

`scope` 예시:
- `premise`, `bible`, `outline`, `characters`, `manuscript`, `reviews`, `style`, `docs`, `ops`

이슈 참조 라인은 가능하면 항상 추가. 마지막 Co-Authored-By 라인은 **Paperclip 스킬 규칙상 필수**.

### 3.3 워크플로
- main에 직접 커밋 (1인 작가 프로젝트, board가 코멘트로 리뷰).
- 큰 변경은 한 번에 묶지 말고 의미 단위로 분리.
- 파괴적 작업 (force push, branch 삭제) 금지.

### 3.4 단독 소유자 관습
하기 폴더는 명시된 에이전트만 직접 편집한다. 다른 에이전트는 변경이 필요하면
Paperclip 이슈로 요청 (직접 수정 금지):

| 폴더/파일 | 단독 소유자 |
|----------|------------|
| `PREMISE.md` | 01 편집장 |
| `bible/` | 02 세계관 설계자 |
| `outline/` | 03 플롯 설계자 |
| `characters/` | 04 캐릭터 담당 |
| `manuscript/` (초고) | 05 집필 작가 |
| `manuscript/` (정합성 수정) | 06 |
| `manuscript/` (문체 교정) | 07 |
| `reviews/canon-ledger.md` | 06 연속성·검수 |
| `style-guide.md` | 07 교정·윤문 |
| `docs/` | 01 편집장 |

## 4. 메모리 계층 (혼동 주의)

| 계층 | 위치 | 공유 범위 | 용도 |
|------|------|----------|------|
| **개인 메모리** | 각 Claude 실행의 `para-memory-files` 스킬 저장소 | 그 에이전트만 | 작업 일지, 학습된 패턴, 결정 이력 |
| **공용 산출물** | 본 리포지토리 (PREMISE, bible/, outline/ 등) | 전 에이전트 + 보드 | 작품 캐논 자체, 진행물 |
| **이슈/코멘트** | Paperclip 서버 | 전 에이전트 + 보드 | 작업 위임·진행·합의 흔적 |

협업의 기본: **한 에이전트가 공용 폴더에 commit & push하면, 다음 하트비트에 다른 에이전트가 `git pull` 후 읽는다.**
`para-memory-files`는 **개인 메모리**일 뿐, 에이전트 간 공유 채널이 아니다.

## 5. 보드 승인 요청 (`request_board_approval`)

게이트(G1–G6, 자세한 건 [COMPANY_GOAL.md](COMPANY_GOAL.md))에서 다음과 같이 호출:

```bash
curl -s -X POST \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "request_board_approval",
    "requestedByAgentId": "'$PAPERCLIP_AGENT_ID'",
    "issueIds": ["<issue-id>"],
    "payload": {
      "title": "PREMISE 확정 승인 요청",
      "summary": "...",
      "recommendedAction": "승인하시면 02·03 작업 시작",
      "risks": ["..."]
    }
  }' \
  "$PAPERCLIP_API_URL/api/companies/$PAPERCLIP_COMPANY_ID/approvals"
```

## 6. 자기 자신을 더럽히지 않기 (No leak)
- 어떤 산출물에도 PAT, API key, paperclip 내부 토큰을 적지 않는다.
- 코멘트·문서·issue description은 공개된다고 가정한다.
- 외부 시스템(github, web search) 호출 시 회사 작품 비밀(스포일러 포함) 누출 주의.
