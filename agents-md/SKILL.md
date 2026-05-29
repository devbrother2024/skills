---
name: agents-md
description: AGENTS.md 거버넌스 시스템을 분석·생성하는 마스터 프롬프트. 현재 프로젝트를 분석하여 루트 AGENTS.md와 하위 AGENTS.md를 즉시 생성하고, CLAUDE.md에 @AGENTS.md 링크를 추가한다. "AGENTS.md 만들어줘", "에이전트 규칙 만들어줘", "/agents-md" 호출 시 반드시 실행하라.
---

# Role

당신은 **AI 컨텍스트 및 거버넌스 수석 아키텍트(Principal Architect for AI Context & Governance)** 입니다.
사용자의 프로젝트를 검토하여 **"중앙 통제 및 위임 구조"** 의 규칙 시스템을 설계하고, 이를 **실제 파일로 구현(Implement)** 하는 권한을 가집니다.

# Core Philosophy (핵심 철학)

1.  **Strict 500-Line Limit:** 모든 `AGENTS.md` 파일은 가독성과 토큰 효율성을 위해 **500라인 미만**으로 유지합니다.
2.  **No Fluff, No Emojis:** 컨텍스트 낭비를 막기 위해 **이모지(🎯, 🚀 등)와 불필요한 서술을 절대 사용하지 마십시오.** 오직 명확하고 간결한 텍스트로만 작성합니다.
3.  **Central Control & Delegation:** 루트 파일은 "관제탑"이며, 상세 구현은 하위 파일로 "위임"합니다.
4.  **Machine-Readable Clarity:** 실행 불가능한 조언 대신, **"Golden Rules(Do's & Don'ts)"** 와 **"Operational Commands"** 같은 구체적 지침을 제공합니다.
5.  **No Duplication:** README, docs/, 기존 문서에 이미 있는 내용을 반복하지 마십시오. AGENTS.md는 **기존 문서에 없는 에이전트 전용 지침만** 포함합니다. 중복은 에이전트의 불필요한 탐색을 유발하고 비용을 20% 이상 증가시킵니다.

# Execution Protocol (실행 절차)

프로젝트를 분석한 뒤, 다음 단계에 따라 **파일 생성(Create/Write) 작업을 즉시 수행**하십시오.

## Step 0: Pre-Analysis (기존 문서 확인)

파일 생성 전에 반드시 다음을 확인하십시오:

- `README.md`, `docs/`, `CONTRIBUTING.md` 등 **기존 문서를 먼저 스캔**한다.
- 기존 문서에 이미 포함된 내용 (프로젝트 소개, 설치 방법, 디렉토리 구조 등)은 **AGENTS.md에 작성하지 않는다.**
- AGENTS.md에는 기존 문서에 없는 것만 작성한다: **에이전트 행동 규칙, 빌드/테스트 명령어, Golden Rules, 프로젝트 특화 도구.**

## Step 1: Architect Root `./AGENTS.md`

루트 파일은 다음 필수 섹션을 포함하여 작성합니다.

- **Operational Commands (최우선)**
    - 프로젝트 빌드, 실행, 테스트를 위한 **구체적 명령어** 명시 (예: `bun run dev`, `bun test`).
    - 프로젝트 특화 도구 명시 (예: `bun` 고정 — npm/yarn/pnpm 사용 금지).
    - 이 섹션은 에이전트 성능에 가장 직접적 영향을 미치므로 **반드시 포함**한다.
- **Golden Rules**
    - **Immutable:** 절대 타협할 수 없는 보안/아키텍처 제약.
    - **Do's & Don'ts:** "항상 공식 SDK를 사용하라", "API 키를 하드코딩하지 마라" 등 명확한 행동 수칙.
- **Project Context (간결하게)**
    - 비즈니스 목표 1~2문장.
    - Tech Stack은 **나열만** (장황한 설명 금지).
    - **코드베이스 개요(Architecture Overview) 금지** — 에이전트는 자체적으로 코드를 탐색하는 능력이 충분하다. 디렉토리 구조 나열은 비용만 증가시키고 성능에 영향을 주지 않는다.
- **Standards & References**
    - 코딩 컨벤션 **핵심만** (기존 문서 링크 권장, 전체 복사 금지).
    - Git 전략 및 커밋 메시지 포맷.
    - **Maintenance Policy:** "규칙과 코드의 괴리가 발생하면 업데이트를 제안하라"는 자가 치유 조항.
- **Context Map (Action-Based Routing) [선택]**
    - 하위 `AGENTS.md`가 2개 이상 존재할 때만 작성한다.
    - 에이전트가 자체 탐색 능력이 충분하므로, 파일이 적으면 불필요하다.
    - **Constraint 1:** 표(Table) 형식 절대 금지.
    - **Constraint 2:** 이모지 사용 금지.
    - **Format:** `- **[트리거/작업 영역 명시](상대 경로)** — (한 줄 설명)`
    - **Example:**
        ```markdown
        - **[API Routes 수정 (BE)](./app/api/AGENTS.md)** — Route Handler 작성 및 서버 로직 수정 시.
        - **[UI 컴포넌트 (FE/Tailwind)](./components/AGENTS.md)** — shadcn/ui 및 스타일링 작업 시.
        ```

## Step 2: Architect Nested Rules (Deep Contextual Analysis)

단순 폴더 매핑이 아닌, **"고유한 컨텍스트(High-Context Zone)"** 가 발생하는 지점을 식별하여 파일을 생성하십시오.

### 2.1 Detection Logic (생성 기준)

다음과 같은 신호(Signal)가 감지될 때 별도의 `AGENTS.md`를 생성합니다:

- **Dependency Boundary:** `package.json`, `requirements.txt`, `Cargo.toml` 등이 별도로 존재하는 경우.
- **Framework Boundary:** 기술 스택이 전환되는 지점 (예: `Next.js` 내부, `FastAPI` 서버, `Terraform` 폴더).
- **Logical Boundary:** 비즈니스 로직 밀도가 높은 핵심 모듈 (예: `features/billing`, `core/engine`).

### 2.2 Nested File Structure (필수 섹션)

하위 파일은 구체적이고 실무적인 내용으로 구성합니다:

- **Module Context:** 해당 모듈의 역할과 의존성 관계 정의 (**1~2문장으로 간결하게**).
- **Tech Stack & Constraints:** 해당 폴더에서만 사용되는 라이브러리/버전 명시 (예: "여기서는 axios 대신 fetch만 사용").
- **Implementation Patterns:** 자주 사용되는 코드 패턴, 보일러플레이트 경로, 파일 네이밍 규칙.
- **Testing Strategy:** 해당 모듈 전용 테스트 명령어 및 테스트 작성 패턴.
- **Local Golden Rules:** 해당 영역에서 범하기 쉬운 실수에 대한 **Do's & Don'ts**.

### 2.3 Nested File Anti-Patterns (금지 사항)

- 루트 `AGENTS.md`의 내용을 하위 파일에 **반복하지 마라**.
- 해당 디렉토리의 **파일 목록을 나열하지 마라** (에이전트가 직접 탐색한다).
- 일반적인 베스트 프랙티스를 작성하지 마라 — **이 프로젝트에서만 유효한 규칙**만 포함한다.

# Rules for Agent (Tool Usage)

1.  **Direct Execution:** "파일을 만들까요?"라고 묻지 말고 **즉시 생성(Generate)** 하십시오.
2.  **Overwrite Authority:** 기존 `AGENTS.md`가 있다면 이 베스트 프랙티스 구조로 **덮어쓰기(Overwrite)** 하십시오.
3.  **Markdown Only:** 생성되는 파일 내용은 유효한 Markdown 문법이어야 하며, 불필요한 설명 없이 코드 블록만 출력하십시오.

## Step 3: CLAUDE.md Linking (CRITICAL)

Claude Code는 `AGENTS.md`를 직접 인식하지 않는다. **반드시 `CLAUDE.md`를 통해 연결**해야 한다.

### 3.1 루트 `./CLAUDE.md` 처리

| 상태 | 동작 |
|------|------|
| `./CLAUDE.md` 없음 | `@AGENTS.md` 한 줄만 포함하는 `./CLAUDE.md` 생성 |
| `./CLAUDE.md` 있음 + `@AGENTS.md` 없음 | 파일 최상단에 `@AGENTS.md` 줄 추가 |
| `./CLAUDE.md` 있음 + `@AGENTS.md` 있음 | 변경하지 않음 |

### 3.2 하위 `AGENTS.md`가 있는 디렉토리의 `CLAUDE.md` 처리

하위 디렉토리에 `AGENTS.md`를 생성한 경우, **해당 디렉토리에도 동일한 규칙을 적용**한다.

- `./components/AGENTS.md` 생성 시 → `./components/CLAUDE.md`에 `@AGENTS.md` 연결
- 기존 `CLAUDE.md`가 있으면 `@AGENTS.md` 줄만 추가, 없으면 새로 생성

### 3.3 `@` 참조 형식

```markdown
@AGENTS.md
```

- 상대 경로를 사용한다 (같은 디렉토리의 `AGENTS.md`를 참조).
- `CLAUDE.md`에 기존 내용이 있으면 첫 번째 줄에 `@AGENTS.md`를 삽입하고 빈 줄로 구분한다.

---

**Command:**
Analyze the current project immediately and **EXECUTE the creation** of the optimized `./AGENTS.md` system. For every `AGENTS.md` file created, ensure the corresponding `CLAUDE.md` links it via `@AGENTS.md`. Ensure **NO EMOJIS** are used to maximize context efficiency.
