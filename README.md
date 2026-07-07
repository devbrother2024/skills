# 개발동생 Skills

대량 생성한 스킬 모음이 아닙니다. 개발동생이 매일 쓰는 워크플로에서 검증한 에이전트 스킬만 골라 담았고, Claude Code, Codex, Cursor에서 동일하게 동작합니다. 필요한 스킬만 개별적으로 설치할 수 있습니다.

## Skills

| Skill | 설명 |
| --- | --- |
| [`deep-interview`](deep-interview/SKILL.md) | 요구사항이 아직 흐릿할 때 씁니다. AI가 한 번에 하나씩 질문하면서 목표와 범위, 완료 기준을 대신 정리해 줍니다 |
| [`agents-md`](agents-md/SKILL.md) | 프로젝트에 에이전트 규칙이 없을 때 씁니다. 코드베이스를 분석해 `AGENTS.md` 규칙 체계를 만들고 `CLAUDE.md`까지 연결합니다 |
| [`autofix`](autofix/SKILL.md) | PR에 리뷰 코멘트가 쌓였을 때 씁니다. 지적을 그대로 반영하지 않고 실제 코드와 대조해서, 맞는 것만 골라 고칩니다 |
| [`advisor-strategy`](advisor-strategy/SKILL.md) | 접근을 확정하기 전이나 막혔을 때 씁니다. 지정한 상위 모델이 작업을 검토하고 조언만 돌려줍니다 (`/advisor-strategy`로만 호출) |
| [`artifact-design`](artifact-design/SKILL.md) | HTML 시안이나 데모를 만들 때 씁니다. 팔레트와 타이포그래피를 먼저 설계해서 어디서 본 듯한 AI 디자인을 피합니다 |

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

**Claude Code**: 별도 등록 없이 위 설치만으로 동작합니다. 채팅에서 `/`를 입력했을 때 스킬 이름이 자동완성에 뜨면 설치된 것입니다. 스킬은 전역 `~/.claude/skills` 또는 프로젝트 `.claude/skills`에 들어갑니다.

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
