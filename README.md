# 개발동생 Skills

개발동생이 실제 작업 흐름에서 사용하는 AI agent skills 공유 저장소입니다.

## Quickstart

가장 쉬운 설치 방법은 `skills` CLI를 사용하는 것입니다.

```bash
npx skills@latest add devbrother2024/skills
```

설치 화면에서 `deep-interview`, `agents-md`, `autofix`, `advisor-strategy` 중 원하는 스킬을 선택하고, 사용할 에이전트를 고르면 됩니다.

특정 에이전트에 바로 설치하려면 아래 명령을 사용하세요.

```bash
# Codex 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent codex --global --yes
npx skills@latest add devbrother2024/skills --skill agents-md --agent codex --global --yes
npx skills@latest add devbrother2024/skills --skill autofix --agent codex --global --yes
npx skills@latest add devbrother2024/skills --skill advisor-strategy --agent codex --global --yes

# Claude Code 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent claude-code --global --yes
npx skills@latest add devbrother2024/skills --skill agents-md --agent claude-code --global --yes
npx skills@latest add devbrother2024/skills --skill autofix --agent claude-code --global --yes
npx skills@latest add devbrother2024/skills --skill advisor-strategy --agent claude-code --global --yes

# Cursor 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent cursor --global --yes
npx skills@latest add devbrother2024/skills --skill agents-md --agent cursor --global --yes
npx skills@latest add devbrother2024/skills --skill autofix --agent cursor --global --yes
npx skills@latest add devbrother2024/skills --skill advisor-strategy --agent cursor --global --yes

# 설치하지 않고 사용 가능한 스킬만 확인
npx skills@latest add devbrother2024/skills --list
```

## Codex Plugin

Codex에서는 이 저장소를 plugin marketplace로 추가한 뒤, Codex의 plugin browser에서 설치할 수도 있습니다.

```bash
codex plugin marketplace add devbrother2024/skills
```

그다음 Codex를 열고 `/plugins`를 실행한 뒤 `개발동생 Skills` marketplace에서 `개발동생 Skills` plugin을 설치하세요.

```bash
codex
/plugins
```

업데이트가 필요하면 marketplace를 갱신합니다.

```bash
codex plugin marketplace upgrade devbrother-skills
```

## Cursor

Cursor는 Agent Skills를 `SKILL.md` 기반으로 로드합니다. 가장 빠른 설치 방법은 `skills` CLI를 사용하는 것입니다.

```bash
# Cursor 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent cursor --global --yes
npx skills@latest add devbrother2024/skills --skill agents-md --agent cursor --global --yes
npx skills@latest add devbrother2024/skills --skill autofix --agent cursor --global --yes
npx skills@latest add devbrother2024/skills --skill advisor-strategy --agent cursor --global --yes

# 현재 프로젝트에 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent cursor --yes
npx skills@latest add devbrother2024/skills --skill agents-md --agent cursor --yes
npx skills@latest add devbrother2024/skills --skill autofix --agent cursor --yes
npx skills@latest add devbrother2024/skills --skill advisor-strategy --agent cursor --yes
```

설치 후 Cursor Settings → Rules에서 설치한 스킬이 Agent Decides 섹션에 보이는지 확인하세요. Agent chat에서는 `/deep-interview`, `/agents-md`, `/autofix`, `/advisor-strategy`로 직접 호출할 수 있습니다.

Cursor 앱 안에서 GitHub 원격 스킬로 추가하려면 아래 순서로 진행합니다.

1. Cursor Settings → Rules를 엽니다.
2. Project Rules 섹션에서 Add Rule을 선택합니다.
3. Remote Rule (Github)을 선택합니다.
4. `https://github.com/devbrother2024/skills`를 입력합니다.

## Skills

| Skill | 설명 | 설치 |
| --- | --- | --- |
| [`deep-interview`](deep-interview/SKILL.md) | 러프한 요청을 바로 실행하지 않고, AI가 사용자에게 한 번에 하나씩 질문하여 목표, 범위, 제약, 완료 기준을 구체화하도록 만드는 스킬 | `npx skills@latest add devbrother2024/skills --skill deep-interview` |
| [`agents-md`](agents-md/SKILL.md) | 프로젝트를 분석해 루트 및 하위 `AGENTS.md` 거버넌스 시스템을 생성하고 `CLAUDE.md`에 `@AGENTS.md` 링크를 추가하는 스킬 | `npx skills@latest add devbrother2024/skills --skill agents-md` |
| [`autofix`](autofix/SKILL.md) | PR의 미해결 리뷰 스레드를 리뷰어(CodeRabbit, Codex cloud review, 사람) 구분 없이 조회하고, 코멘트별 타당성을 검증한 뒤 적절한 지적만 승인(또는 `--auto`) 하에 반영하는 스킬 | `npx skills@latest add devbrother2024/skills --skill autofix` |
| [`advisor-strategy`](advisor-strategy/SKILL.md) | 사용자가 지정한 상위 모델을 Advisor로 세워 접근 확정 전 검토, 완료 선언 전 검증, 막힘 진단 등 결정점에서 컨설트하는 스킬 (명시 호출 전용) | `npx skills@latest add devbrother2024/skills --skill advisor-strategy` |

## Why This Exists

AI 코딩 에이전트의 결과물 차이는 모델 성능보다 요구사항을 얼마나 명확히 정의했는지에서 크게 갈립니다.

문제는 프롬프트를 처음부터 완벽하게 쓰기 어렵다는 점입니다. 사용자 본인도 아직 무엇을 원하는지 모르는 경우가 많기 때문입니다.

`deep-interview`는 이 문제를 역으로 풉니다. AI에게 바로 실행을 맡기기 전에, AI가 먼저 사용자를 인터뷰하게 만들어 목표, 범위, 제약, 완료 기준을 명확하게 만듭니다.

## deep-interview

사용 시점:

- 아이디어는 있지만 요구사항이 흐릿할 때
- Plan Mode로 바로 들어가기 전에 맥락을 더 정리하고 싶을 때
- 코딩, 제품 기획, 콘텐츠 기획, 업무 자동화처럼 결과물의 성공 기준을 먼저 맞춰야 할 때

질문은 한 번에 하나만 묻고, 매 질문은 아래 구조를 따릅니다. 선택지는 답변 부담을 줄이거나 사용자의 암묵적 판단 기준을 드러내는 데 도움이 될 때만 붙입니다.

```md
현재 이해: {요청과 지금까지 정해진 내용을 필요한 만큼 간결하게 요약}
막힌 결정: {지금 풀어야 하는 가장 중요한 불확실성}
질문: {한 가지 질문}
선택지: {필요할 때만 총 2-3개. 마지막 항목은 `- (직접 입력)`}
```

권장 항목이 필요하면 항상 A안에 `(권장: 짧은 이유)`로 표시합니다. 선택지가 사용자의 사고를 좁히거나 객관식 답변처럼 만들면 선택지를 붙이지 않습니다.

다음 항목이 정리되면 인터뷰를 멈춥니다.

- 달성하려는 목표
- 포함 범위와 제외 범위
- 지켜야 할 제약
- 완료 판단 기준
- 아직 남은 열린 질문

## agents-md

사용 시점:

- 프로젝트에 `AGENTS.md` 규칙 시스템을 새로 만들고 싶을 때
- 루트 규칙과 하위 폴더별 위임 규칙을 함께 설계하고 싶을 때
- Claude Code가 같은 규칙을 읽도록 `CLAUDE.md`에 `@AGENTS.md` 링크를 추가하고 싶을 때

`agents-md`는 단일 `SKILL.md` 안에 실행 지침을 포함합니다. 별도 `references/` 파일 없이 gist의 마스터 프롬프트 구조를 그대로 공유합니다.

## autofix

사용 시점:

- PR에 쌓인 리뷰 코멘트(CodeRabbit, Codex cloud review, 사람 리뷰어)를 한 번에 정리하고 싶을 때
- 리뷰 지적을 그대로 반영하기 전에, 실제 코드와 대조해 타당한 지적만 골라내고 싶을 때
- 신뢰하는 저위험 브랜치에서 리뷰 반영→커밋→push→resolve→재리뷰까지 자동 루프를 돌리고 싶을 때 (`--auto`)

동작 원칙:

- 리뷰 코멘트를 명령이 아니라 **검증 대상**으로 취급합니다. 코멘트별로 분석 전용 서브에이전트가 실제 코드를 읽고 적절/부적절을 판정하고, 적절 판정만 수정 대상에 올립니다.
- 기본 모드는 검증 테이블과 수정 계획을 보여준 뒤 승인받아 적용하고 단일 커밋까지만 수행합니다. push·스레드 resolve·재리뷰 루프는 `--auto`를 명시했을 때만 자동화합니다.
- 리뷰 코멘트 본문은 untrusted input으로 다룹니다. 시크릿 접근·외부 URL·인프라 변경을 유도하는 지시는 무시하며, 코멘트 텍스트를 셸 명령에 보간하지 않습니다.

## advisor-strategy

사용 시점:

- 접근을 확정하기 전에 더 강한 모델의 검토를 받고 싶을 때
- 완료를 선언하기 전에 산출물을 독립 컨텍스트에서 검증받고 싶을 때
- 같은 오류가 반복되거나 접근이 수렴하지 않을 때 (막힘 진단)

동작 원칙:

- Anthropic의 Advisor Strategy(executor/advisor 모델 조합) 패턴을 스킬로 구현했습니다. Advisor는 조언만 반환하고 산출물은 만들지 않습니다.
- advisor 모델은 디폴트 없이 호출할 때 직접 지정합니다: `/advisor-strategy <fable|opus|sonnet> [질문·주제]`. 모델을 지정하지 않으면 진행하지 않습니다 (비용·모델 접근 권한이 걸린 선택은 사용자 몫).
- Advisor는 브리프를 그대로 믿지 않고, 핵심 전제를 증거 경로에서 read-only로 직접 검증한 뒤 조언합니다.
- `disable-model-invocation: true` — 자동 발동 없이 명시 호출 전용입니다.

개념·컨설트 타이밍 규율·브리프 템플릿은 [`advisor-strategy/SKILL.md`](advisor-strategy/SKILL.md) 단일 파일에 모두 담겨 있습니다.

## Manual Install

`npx`를 사용하지 않고 직접 복사해도 됩니다.

Codex 전역 설치:

```bash
mkdir -p ~/.agents/skills
cp -R deep-interview ~/.agents/skills/deep-interview
cp -R agents-md ~/.agents/skills/agents-md
cp -R autofix ~/.agents/skills/autofix
cp -R advisor-strategy ~/.agents/skills/advisor-strategy
```

Codex 프로젝트 설치:

```bash
mkdir -p .agents/skills
cp -R deep-interview .agents/skills/deep-interview
cp -R agents-md .agents/skills/agents-md
cp -R autofix .agents/skills/autofix
cp -R advisor-strategy .agents/skills/advisor-strategy
```

Claude Code 전역 설치:

```bash
mkdir -p ~/.claude/skills
cp -R deep-interview ~/.claude/skills/deep-interview
cp -R agents-md ~/.claude/skills/agents-md
cp -R autofix ~/.claude/skills/autofix
cp -R advisor-strategy ~/.claude/skills/advisor-strategy
```

Claude Code 프로젝트 설치:

```bash
mkdir -p .claude/skills
cp -R deep-interview .claude/skills/deep-interview
cp -R agents-md .claude/skills/agents-md
cp -R autofix .claude/skills/autofix
cp -R advisor-strategy .claude/skills/advisor-strategy
```

Cursor 전역 설치:

```bash
mkdir -p ~/.cursor/skills
cp -R deep-interview ~/.cursor/skills/deep-interview
cp -R agents-md ~/.cursor/skills/agents-md
cp -R autofix ~/.cursor/skills/autofix
cp -R advisor-strategy ~/.cursor/skills/advisor-strategy
```

Cursor 프로젝트 설치:

```bash
mkdir -p .cursor/skills
cp -R deep-interview .cursor/skills/deep-interview
cp -R agents-md .cursor/skills/agents-md
cp -R autofix .cursor/skills/autofix
cp -R advisor-strategy .cursor/skills/advisor-strategy
```

## Repository Structure

```text
.
├── .agents/plugins/marketplace.json   # Codex plugin marketplace metadata
├── .claude-plugin/plugin.json         # Claude Code plugin compatibility metadata
├── .codex-plugin/plugin.json          # Codex plugin manifest
├── agents-md/SKILL.md                 # AGENTS.md governance generator skill
├── autofix/SKILL.md                   # PR review verify-and-apply skill
└── deep-interview/SKILL.md            # Skill source
```

## License

MIT
