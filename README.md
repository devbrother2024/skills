# 개발동생 Skills

개발동생이 실제 작업 흐름에서 사용하는 AI agent skills 공유 저장소입니다.

<p>
  <a href="#cursor">
    <img alt="Cursor 연동" src="https://img.shields.io/badge/Cursor-Install%20Skill-111827?style=for-the-badge" />
  </a>
</p>

## Quickstart

가장 쉬운 설치 방법은 `skills` CLI를 사용하는 것입니다.

```bash
npx skills@latest add devbrother2024/skills
```

설치 화면에서 `deep-interview`를 선택하고, 사용할 에이전트를 고르면 됩니다.

특정 에이전트에 바로 설치하려면 아래 명령을 사용하세요.

```bash
# Codex 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent codex --global --yes

# Claude Code 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent claude-code --global --yes

# Cursor 전역 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent cursor --global --yes

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

# 현재 프로젝트에 설치
npx skills@latest add devbrother2024/skills --skill deep-interview --agent cursor --yes
```

설치 후 Cursor Settings → Rules에서 `deep-interview`가 Agent Decides 섹션에 보이는지 확인하세요. Agent chat에서는 `/deep-interview`로 직접 호출할 수 있습니다.

Cursor 앱 안에서 GitHub 원격 스킬로 추가하려면 아래 순서로 진행합니다.

1. Cursor Settings → Rules를 엽니다.
2. Project Rules 섹션에서 Add Rule을 선택합니다.
3. Remote Rule (Github)을 선택합니다.
4. `https://github.com/devbrother2024/skills`를 입력합니다.

## Skills

| Skill | 설명 | 설치 |
| --- | --- | --- |
| [`deep-interview`](deep-interview/SKILL.md) | 러프한 요청을 바로 실행하지 않고, AI가 사용자에게 한 번에 하나씩 질문하여 목표, 범위, 제약, 완료 기준을 구체화하도록 만드는 스킬 | `npx skills@latest add devbrother2024/skills --skill deep-interview` |

## Why This Exists

AI 코딩 에이전트의 결과물 차이는 모델 성능보다 요구사항을 얼마나 명확히 정의했는지에서 크게 갈립니다.

문제는 프롬프트를 처음부터 완벽하게 쓰기 어렵다는 점입니다. 사용자 본인도 아직 무엇을 원하는지 모르는 경우가 많기 때문입니다.

`deep-interview`는 이 문제를 역으로 풉니다. AI에게 바로 실행을 맡기기 전에, AI가 먼저 사용자를 인터뷰하게 만들어 목표, 범위, 제약, 완료 기준을 명확하게 만듭니다.

## deep-interview

사용 시점:

- 아이디어는 있지만 요구사항이 흐릿할 때
- Plan Mode로 바로 들어가기 전에 맥락을 더 정리하고 싶을 때
- 코딩, 제품 기획, 콘텐츠 기획, 업무 자동화처럼 결과물의 성공 기준을 먼저 맞춰야 할 때

질문은 한 번에 하나만 묻고, 매 질문은 아래 구조를 따릅니다.

```md
현재 이해: {요청을 한 문장으로 요약}
막힌 결정: {가장 중요한 불확실성}
추천 답안: {있으면 제시}
질문: {한 가지 질문}
```

다음 항목이 정리되면 인터뷰를 멈춥니다.

- 달성하려는 목표
- 포함 범위와 제외 범위
- 지켜야 할 제약
- 완료 판단 기준
- 아직 남은 열린 질문

## Manual Install

`npx`를 사용하지 않고 직접 복사해도 됩니다.

Codex 전역 설치:

```bash
mkdir -p ~/.agents/skills
cp -R deep-interview ~/.agents/skills/deep-interview
```

Codex 프로젝트 설치:

```bash
mkdir -p .agents/skills
cp -R deep-interview .agents/skills/deep-interview
```

Claude Code 전역 설치:

```bash
mkdir -p ~/.claude/skills
cp -R deep-interview ~/.claude/skills/deep-interview
```

Claude Code 프로젝트 설치:

```bash
mkdir -p .claude/skills
cp -R deep-interview .claude/skills/deep-interview
```

Cursor 전역 설치:

```bash
mkdir -p ~/.cursor/skills
cp -R deep-interview ~/.cursor/skills/deep-interview
```

Cursor 프로젝트 설치:

```bash
mkdir -p .cursor/skills
cp -R deep-interview .cursor/skills/deep-interview
```

## Repository Structure

```text
.
├── .agents/plugins/marketplace.json   # Codex plugin marketplace metadata
├── .claude-plugin/plugin.json         # Claude Code plugin compatibility metadata
├── .codex-plugin/plugin.json          # Codex plugin manifest
└── deep-interview/SKILL.md            # Skill source
```

## License

MIT
