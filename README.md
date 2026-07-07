# 개발동생 Skills

대량 생성한 스킬 모음이 아닙니다. 개발동생이 매일 쓰는 워크플로에서 검증한 에이전트 스킬만 골라 담았고, Claude Code, Codex, Cursor에서 동일하게 동작합니다. 필요한 스킬만 개별적으로 설치할 수 있습니다.

## Skills

| Skill | 설명 |
| --- | --- |
| [`deep-interview`](deep-interview/SKILL.md) | 바로 실행하는 대신 AI가 먼저 한 번에 하나씩 질문해서, 흐릿한 요청을 목표와 범위, 완료 기준이 잡힌 요구사항으로 만들어 줍니다 |
| [`agents-md`](agents-md/SKILL.md) | 프로젝트를 분석해서 `AGENTS.md` 규칙 체계를 만들어 주고, Claude Code도 같은 규칙을 읽도록 `CLAUDE.md`에 연결합니다 |
| [`autofix`](autofix/SKILL.md) | 쌓인 PR 리뷰 코멘트를 실제 코드와 대조해 보고, 타당한 지적만 골라 승인받아 반영합니다 |
| [`advisor-strategy`](advisor-strategy/SKILL.md) | 막히거나 중요한 결정을 앞뒀을 때, 지정한 상위 모델에게 세컨드 오피니언을 받아 옵니다 (`/advisor-strategy`로만 호출) |
| [`artifact-design`](artifact-design/SKILL.md) | HTML 산출물을 만들 때 팔레트와 타이포그래피, 레이아웃을 먼저 설계해서 AI 티가 나는 템플릿 디자인을 피합니다 |

각 스킬의 전체 문서는 링크된 `SKILL.md`에 있습니다.

## 설치

가장 쉬운 방법은 [`skills`](https://skills.sh) CLI입니다.

```bash
# 대화식: 스킬과 에이전트를 화면에서 선택
npx skills@latest add devbrother2024/skills

# 바로 설치
npx skills@latest add devbrother2024/skills --skill <스킬> --agent <에이전트> --global --yes
```

- `<스킬>`: 위 Skills 표의 이름
- `<에이전트>`: `codex` | `claude-code` | `cursor`
- 현재 프로젝트에만 설치하려면 `--global`을 뺍니다
- 설치 가능한 목록만 확인: `npx skills@latest add devbrother2024/skills --list`

설치 후 에이전트 채팅에서 `/스킬이름`으로 직접 호출합니다.

## 에이전트별 참고

**Codex**: plugin marketplace로도 설치할 수 있습니다.

```bash
codex plugin marketplace add devbrother2024/skills
```

이후 `codex`를 열고 `/plugins`에서 `개발동생 Skills`를 설치합니다. 업데이트는 `codex plugin marketplace upgrade devbrother-skills`.

**Cursor**: 설치 후 Settings → Rules의 Agent Decides 섹션에 스킬이 보이는지 확인합니다. GitHub 원격 규칙으로 추가하려면 Settings → Rules → Add Rule → Remote Rule (Github)에서 `https://github.com/devbrother2024/skills`를 입력합니다.

## 직접 설치

`npx` 없이 스킬 폴더를 복사해도 됩니다.

```bash
cp -R <스킬> <스킬 디렉토리>/<스킬>
```

| 에이전트 | 전역 | 프로젝트 |
| --- | --- | --- |
| Codex | `~/.agents/skills` | `.agents/skills` |
| Claude Code | `~/.claude/skills` | `.claude/skills` |
| Cursor | `~/.cursor/skills` | `.cursor/skills` |

예를 들어 autofix를 Claude Code 전역에 설치하려면:

```bash
mkdir -p ~/.claude/skills && cp -R autofix ~/.claude/skills/autofix
```

## License

MIT. 플러그인 메타데이터(`.claude-plugin/`, `.codex-plugin/`, `.agents/plugins/`)는 각 에이전트 marketplace 노출용입니다.
