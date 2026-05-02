# Skills 시스템 & Remote Control 🛠️📱

> Claude Code를 **나만의 도구로 확장**하고, **어디서든 원격 제어**하는 법을 배워봐요.
> "한 번 만들어두면 평생 쓰는" 자동화의 세계로 들어가요!

---

## 🎯 학습 목표

이 실습을 마치면 다음을 할 수 있어요:

- ✅ **SKILL.md** 파일 형식과 디렉토리 구조 이해
- ✅ **Agent Skills 오픈 스탠다드** 개념 파악
- ✅ 재사용 가능한 **Skill 직접 작성·관리**
- ✅ **Remote Control** 로 외부 기기에서 세션 제어
- ✅ Skill 설치·실행 시의 **보안 위험 및 대응책** 숙지

---

## 📑 목차

- [시작하기 전에](#-시작하기-전에)
- [1. SKILL.md 파일 형식 & 디렉토리 구조](#1️⃣-skillmd-파일-형식--디렉토리-구조)
- [2. Agent Skills 오픈 스탠다드](#2️⃣-agent-skills-오픈-스탠다드)
- [3. 실전 예시 & Skill 관리](#3️⃣-실전-예시--skill-관리)
- [4. Remote Control 소개 및 사용 방법](#4️⃣-remote-control-소개-및-사용-방법)
- [5. 보안 고려사항 & 제한사항](#5️⃣-보안-고려사항--제한사항)
- [🪞 5분 회고](#-5분-회고)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [📚 공식 문서](#-공식-문서)
- [🎓 다음 단계](#-다음-단계)

---

## 📋 시작하기 전에

- ✅ Claude Code 설치 완료 → [설치 가이드](./claude-code-install-guide.md)
- ✅ [효과적인 프롬프트 & CLAUDE.md 실습](./effective-prompting-and-claude-md.md) 완료
- ✅ Claude.ai **Pro / Max / Team / Enterprise** 구독 (Remote Control 필수)
- ✅ 마음의 준비: **"한 번 만들면 평생 써먹어요"** 🌱

> ⏱ **소요 시간**: 약 60~90분
> 🎯 **권장 모드**: Plan 모드

### 작업 폴더 준비

```bash
mkdir skills-practice
cd skills-practice
claude
```

---

## 1️⃣ SKILL.md 파일 형식 & 디렉토리 구조

### 🤔 Skill이 뭐예요?

**한마디로:** Claude에게 가르치는 **재사용 가능한 작업 매뉴얼**이에요.

### 비유로 이해하기

| 익숙한 것 | Skill |
|----------|-------|
| 📖 요리 레시피 | 한 번 적어두면 매번 같은 결과 |
| 🧰 공구 세트 | 필요할 때마다 꺼내 쓰는 도구 |
| 📋 회사 SOP | 표준 절차서 (Standard Operating Procedure) |

### 📁 Skill은 단일 파일이 아니라 "디렉토리"

```
my-skill/                       ← Skill 이름 (디렉토리명)
├── SKILL.md                    ← 필수: 메인 지침서
├── examples/                   ← 선택: 예시 출력
│   ├── good.md
│   └── bad.md
├── scripts/                    ← 선택: 실행 가능한 스크립트
│   └── validate.sh
├── references/                 ← 선택: 추가 참조 문서
│   └── api-spec.md
└── template.md                 ← 선택: 템플릿
```

> 💡 **핵심 원칙**: `SKILL.md`는 **500줄 이내**로 짧게! 상세한 내용은 별도 파일로 분리해서 **필요할 때만 로드**.

### 📍 Skill이 사는 위치

| 범위 | 경로 | 적용 대상 |
|------|------|----------|
| 👤 **Personal** | `~/.claude/skills/<이름>/SKILL.md` | 내 모든 프로젝트 |
| 📁 **Project** | `.claude/skills/<이름>/SKILL.md` | 이 프로젝트만 |
| 🏢 **Enterprise** | 관리형 설정 | 회사 전체 |
| 🔌 **Plugin** | `<plugin>/skills/<이름>/SKILL.md` | 플러그인 활성화 시 |

> ⚠️ **이름 충돌 우선순위**: Enterprise > Personal > Project. 플러그인은 `플러그인이름:스킬이름` 형태로 네임스페이스 분리.

### 🧱 SKILL.md 최소 형식

```markdown
---
name: korean-readme-writer
description: Use when generating or updating README.md files in Korean. Ensures consistent tone (존댓말), markdown structure, and section ordering.
---

# 한국어 README 작성 스킬

## 사용 시점
- README.md 신규 작성
- 기존 README 한국어로 번역/리라이팅

## 절차
1. 기존 코드 구조 파악
2. 섹션 순서: 소개 → 설치 → 사용법 → 라이선스
3. 모든 명령어 예시는 코드 블록으로
4. 존댓말 사용
```

### 📐 Frontmatter 필드 (YAML 헤더)

| 필드 | 필수? | 용도 |
|------|------|------|
| `name` | 권장 | Skill 식별자 (생략 시 디렉토리명 사용) |
| `description` | 권장 | **언제 써야 하는지** 설명 (최대 1,024자) |
| `disable-model-invocation` | 선택 | `true`면 자동 호출 차단 (수동만) |
| `user-invocable` | 선택 | `false`면 `/` 메뉴에서 숨김 |
| `allowed-tools` | 선택 | 권한 프롬프트 없이 사용할 도구 목록 |
| `context: fork` | 선택 | 격리된 서브에이전트로 실행 |
| `arguments` | 선택 | 명명된 위치 인자 |
| `effort`, `model` | 선택 | 세션 설정 오버라이드 |
| `paths` | 선택 | 활성화 글롭 패턴 |

### 🎯 description 잘 쓰는 법

description은 **Claude가 언제 이 스킬을 호출할지 판단하는 근거**예요. 두 부분으로 나누어 쓰면 효과적이에요:

```yaml
description: Explains code with visual diagrams and analogies. 
  Use when explaining how code works, teaching about a codebase, 
  or when the user asks "how does this work?"
```

| 구조 | 예시 |
|------|------|
| ① **무엇을 하는가** | "Explains code with visual diagrams" |
| ② **언제 써야 하는가** | "Use when explaining how code works..." |

> 💡 **앞부분에 핵심 유스케이스를 배치**하세요. description이 길면 뒤쪽이 잘 안 읽혀요.

---

## 2️⃣ Agent Skills 오픈 스탠다드

### 🌍 Agent Skills란?

Claude Code의 Skill은 **Anthropic이 발표한 오픈 스탠다드** [agentskills.io](https://agentskills.io) 를 따릅니다.

### 핵심 아이디어

```
┌─────────────────────────────────────────────┐
│  Markdown + YAML frontmatter = Agent Skill  │
│  → 어떤 AI 에이전트도 읽고 실행 가능        │
└─────────────────────────────────────────────┘
```

### 비교: 다른 표준과의 관계

| 표준 | 무엇을 표준화? | 비유 |
|------|---------------|------|
| **Agent Skills** | Skill 작성 형식 | 📖 책의 목차 표준 |
| **MCP (Model Context Protocol)** | 외부 도구 연결 방식 | 🔌 USB-C 단자 |
| **CLAUDE.md** | 프로젝트 컨텍스트 | 🏢 회사 입사 안내문 |

### 🧬 Claude Code의 확장

Claude Code는 표준을 **확장**해서 추가 기능을 제공해요:

- 🎯 **호출 제어** (`disable-model-invocation`, `user-invocable`)
- 🔀 **서브에이전트 실행** (`context: fork`)
- 💉 **동적 컨텍스트 주입** (`paths`, `arguments`)

> ⚠️ **크로스 플랫폼 호환**: 기본 표준 부분은 다른 도구에서도 동작 가능하지만, Claude Code 확장 필드는 **Claude Code에서만** 동작해요. 공식 문서에 타 플랫폼 호환 명시는 아직 없음.

### 🔑 왜 표준이 중요한가?

| 표준이 있을 때 | 표준이 없을 때 |
|---------------|---------------|
| ✅ 한 번 만들면 여러 도구에서 활용 | ❌ 도구마다 따로 작성 |
| ✅ 커뮤니티 공유·재사용 | ❌ 폐쇄적 생태계 |
| ✅ 도구 간 마이그레이션 쉬움 | ❌ 락인(lock-in) |

---

## 3️⃣ 실전 예시 & Skill 관리

### 🎬 실습 1: 첫 Skill 직접 만들기

**시나리오**: 커밋 메시지를 일관된 형식으로 작성해주는 Skill

#### Step 1. 디렉토리 생성

```bash
!mkdir -p ~/.claude/skills/conventional-commit
```

#### Step 2. SKILL.md 작성 요청

```
~/.claude/skills/conventional-commit/SKILL.md 파일을 만들어줘.
- 이름: conventional-commit
- 설명: Conventional Commits 형식(feat:, fix:, docs: 등)으로 커밋 메시지 작성 지원
- 사용 시점: 사용자가 git commit 메시지를 작성하려 할 때
- 절차: 변경사항 분석 → 타입 선택 → 50자 이내 제목 + 본문 작성
```

#### Step 3. 동작 확인

```
/help
```

→ 새로 만든 `conventional-commit` Skill이 목록에 떠야 해요!

```
변경사항을 보고 conventional-commit Skill로 커밋 메시지 만들어줘
```

→ Claude가 자동으로 Skill을 호출해서 형식에 맞는 메시지 생성!

### 🎬 실습 2: 번들 파일이 있는 Skill 만들기

복잡한 Skill은 **하위 파일**을 활용해요.

```
~/.claude/skills/api-doc-writer/
├── SKILL.md                    ← 메인 지침
├── template.md                 ← 문서 템플릿
└── examples/
    └── user-api.md             ← 좋은 예시
```

**SKILL.md 내용:**

```markdown
---
name: api-doc-writer
description: Writes API documentation in our team's house style. Use when documenting REST/GraphQL endpoints.
---

# API 문서 작성 스킬

## 절차
1. `template.md` 의 구조를 그대로 따른다
2. 좋은 예시는 `examples/user-api.md` 를 참고
3. 모든 endpoint 마다 다음을 포함:
   - 한 줄 설명 (한국어)
   - HTTP 메서드 + 경로
   - 요청/응답 예시 (JSON)
   - 에러 코드 표
```

> 💡 Claude는 SKILL.md를 먼저 읽고, **필요할 때만** template.md나 examples를 추가로 로드해요. 토큰 효율적!

### 📋 Skill 관리 명령어

| 동작 | 방법 |
|------|------|
| **목록 보기** | `/help` 또는 파일 시스템 (`!ls ~/.claude/skills/`) |
| **수동 호출** | "X Skill 사용해서 ..." 라고 요청 |
| **자동 차단** | frontmatter에 `disable-model-invocation: true` |
| **사용자 메뉴 숨기기** | `user-invocable: false` |
| **삭제** | 디렉토리 삭제 (`!rm -rf ~/.claude/skills/<이름>`) |

### 🏗️ Skill 작성 5계명

1. 📏 **짧게**: SKILL.md는 500줄 이하, 핵심 절차만
2. 🎯 **구체적인 description**: "언제 쓰는지" 명확히
3. 📦 **번들로 분리**: 큰 참조 자료는 `references/`로
4. 🔁 **반복 패턴만 Skill로**: 일회성 작업은 그냥 프롬프트
5. 🧪 **테스트**: 실제로 Claude가 자동 호출하는지 확인

### 🌐 커뮤니티 Skill 활용

플러그인을 통해 **남이 만든 Skill** 도 쓸 수 있어요. 시스템에 이미 설치된 것들 예시:

```
superpowers:brainstorming      # 창의 작업 시작
superpowers:test-driven-development  # TDD 강제
claude-hud:setup               # 상태바 커스터마이징
update-config                  # settings.json 자동 편집
```

> 🎓 **강의 팁**: 학습자에게 본인 워크플로 중 **반복되는 작업** 1개를 Skill로 만들게 해보세요!

---

## 4️⃣ Remote Control 소개 및 사용 방법

### 🤔 Remote Control이 뭐예요?

내 컴퓨터에서 실행 중인 Claude Code 세션을 **다른 기기(폰·노트북·태블릿)** 에서 제어하는 기능이에요.

### 🌟 어떤 상황에 좋아요?

| 상황 | 활용 |
|------|------|
| 🚇 출퇴근 길 | 폰으로 빌드 진행 상황 확인 |
| ☕ 카페에서 회의 | 노트북에서 데스크탑 세션 제어 |
| 🏃 자리 비움 | 멀리서 결정 사항만 응답 |
| 👥 페어 프로그래밍 | 같은 세션에 두 명 접속 |

### 📋 사전 요구사항

- ✅ Claude.ai **Pro / Max / Team / Enterprise** 구독
- ❌ **API 키 사용 불가** — OAuth(`/login`) 필수
- 🏢 Team/Enterprise 사용자: 관리자가 Remote Control 토글 활성화 필요

### 🎬 시작하는 3가지 방법

#### 방법 1: 셸에서 서버 모드로 시작

```bash
claude remote-control
```

→ URL과 **QR 코드** 가 표시됨. 스페이스바로 QR 토글 가능.

#### 방법 2: 인터랙티브 + 이름 지정

```bash
claude --remote-control "내 사이드 프로젝트"
```

→ 세션에 이름이 붙어서 claude.ai/code에서 찾기 쉬움.

#### 방법 3: 이미 실행 중인 세션에서

```
/remote-control
```

또는 단축형:

```
/rc
```

### 🔌 다른 기기에서 접속하는 법

| 기기 | 방법 |
|------|------|
| 🌐 **데스크탑/노트북 브라우저** | URL 직접 열기 → claude.ai/code |
| 📱 **모바일 (iOS/Android)** | Claude 앱에서 QR 코드 스캔 |
| 🔍 **세션 목록에서 찾기** | claude.ai/code 접속 → 이름으로 검색 (🟢 녹색 점이면 온라인) |

### ✨ 원격에서 할 수 있는 것

```
✅ 메시지/프롬프트 전송
✅ 실시간 세션 제어
✅ 로컬 파일시스템 접근 (@경로 자동완성도 동작)
✅ MCP 서버·도구 사용
✅ 대화 기기 간 동기화
✅ 모바일 푸시 알림 (작업 완료/결정 필요 시)
```

### ⚠️ 원격에서 제한되는 것

```
❌ /mcp        (터미널 인터랙티브 필요)
❌ /plugin     
❌ /resume     
✅ /compact, /clear, /context, /exit  ← 이건 됨
```

> 💡 텍스트 출력만 하는 명령은 대부분 원격 OK. 키 입력 인터랙션이 필요한 명령은 로컬에서만!

### 🔐 연결 보안 모델

```
┌──────────────┐    HTTPS(TLS)    ┌────────────────┐
│ 내 컴퓨터     │ ────[outbound]──→ │ Anthropic API  │
│ (Claude Code) │ ←──[poll work]── │  (gateway)     │
└──────────────┘                    └────────────────┘
                                            ↑
                                            │ HTTPS(TLS)
                                            │
                                    ┌──────────────┐
                                    │ 폰/브라우저  │
                                    └──────────────┘
```

| 보안 요소 | 설명 |
|-----------|------|
| 🚫 **Inbound 포트 X** | 내 컴퓨터는 **outbound HTTPS만** |
| 🔒 **TLS 암호화** | 모든 트래픽 Anthropic API 경유 (표준 Claude Code와 동일) |
| ⏱ **Short-lived 자격증명** | 각 연결마다 단기 토큰 발급, 독립 만료 |
| ☁️ **클라우드 실행 X** | Claude는 **로컬에서만** 실행됨 (코드 유출 X) |

> 💡 **핵심**: Remote Control은 "원격 명령 전달" 일뿐, 실제 코드 실행과 파일 접근은 **모두 로컬 컴퓨터**에서 일어나요.

### 🏋️ 실습 미션

```
1. 데스크탑에서 claude remote-control 실행
2. 표시된 QR 코드를 폰의 Claude 앱으로 스캔
3. 폰에서 "현재 폴더의 README.md 내용 요약해줘" 입력
4. 데스크탑 세션이 응답하는지 확인
5. /exit 으로 원격 세션 종료
```

---

## 5️⃣ 보안 고려사항 & 제한사항

### ⚠️ Skill의 보안 위험

Skill은 **Claude의 행동을 지시**하는 문서예요. 신뢰할 수 없는 Skill을 설치하면 위험해요.

### 🚨 주요 위험 시나리오

| 위험 | 설명 | 예시 |
|------|------|------|
| 💣 **임의 코드 실행** | 명시된 용도 외 도구·코드 실행 지시 | "리뷰해줘" 라더니 비밀번호 파일 읽기 |
| 📤 **데이터 유출** | 민감 정보를 외부로 전송 | API 키를 외부 URL로 POST |
| 🌐 **외부 의존성 변조** | 외부 URL fetch 후 악성 명령 실행 | CDN 변조로 코드 삽입 |
| 🛠 **도구 오용** | 의도치 않은 네트워크 호출, 파일 접근 | 무제한 파일 시스템 스캔 |

### 🛡️ 방어 수단 (Permission Controls)

#### ① Frontmatter 통제

```yaml
---
name: my-skill
description: ...
disable-model-invocation: true   # 자동 호출 차단 (수동만)
user-invocable: false            # 사용자 / 메뉴에서 숨김
allowed-tools:                   # 권한 프롬프트 없이 쓸 도구
  - Bash(git *)
  - Read
---
```

#### ② /permissions 규칙

```
Skill(deploy *)        # deploy 로 시작하는 Skill만 허용
Skill                  # 모든 Skill 차단
```

#### ③ 관리형 정책 (조직)

```json
{
  "disableSkillShellExecution": true
}
```

→ 번들된 게 아닌 Skill의 셸 실행을 조직 차원에서 차단.

### ⚠️ 중요한 한계

| 사실 | 의미 |
|------|------|
| 🚫 **VM 샌드박싱 없음** | Skill은 Claude Code와 **같은 실행 환경**에서 동작 |
| ✅ **Permission 통제만** | 격리가 아닌 **허가/차단** 방식 |
| 👤 **신뢰가 핵심** | "Skill 설치 = 소프트웨어 설치" 와 같은 신중함 필요 |

### 🔒 Skill 설치 체크리스트

설치 전 반드시 확인:

- [ ] 출처가 신뢰할 수 있는가? (공식 / 본인 작성 / 잘 알려진 커뮤니티)
- [ ] SKILL.md 내용을 읽고 의도 파악했는가?
- [ ] `allowed-tools` 가 필요 이상으로 광범위하지 않은가?
- [ ] `references/`, `scripts/` 안에 의심스러운 파일은 없는가?
- [ ] 외부 URL을 fetch하는가? (있다면 그 URL이 안전한가?)

### 🔐 Remote Control의 보안

| 안전 | 주의 |
|------|------|
| ✅ Inbound 포트 안 열림 | ⚠️ 세션 URL이 노출되면 외부 접근 가능 |
| ✅ TLS 암호화 | ⚠️ 모바일 기기 분실 시 세션 접근 위험 |
| ✅ Short-lived 자격증명 | ⚠️ 공용 와이파이의 클라이언트 측 위험은 별도 |
| ✅ 로컬 실행 (코드 클라우드 X) | ⚠️ Claude가 실행하는 명령은 **로컬 권한 그대로** |

> 💡 **세션 URL 관리**: QR 코드·URL을 **메신저·메일에 공유 금지**. 한 번 노출되면 토큰 만료 전까지 누구나 접속 가능!

### 📜 데이터 처리

- 🏠 **코드/파일은 로컬에 머무름** — Anthropic 서버로 업로드 X
- 💬 **대화 내용**은 일반 Claude API와 동일하게 처리 (정책은 플랜에 따라 다름)
- ⏳ Remote Control 세션의 **데이터 보존 기간**은 공식 문서에 명시되지 않음 — 민감 작업 시 문의 권장

---

## 🪞 5분 회고

여기까지 따라왔다면 정말 대단해요! 잠시 멈추고 돌아봐요.

### 📝 스스로에게 던질 질문

**1. 내가 만들고 싶은 Skill 1개를 꼽는다면?**
- 자주 쓰는 코드 리뷰 체크리스트?
- 우리 팀 컨벤션 강제 Skill?
- 특정 형식의 문서 자동 생성 Skill?

**2. Remote Control이 가장 유용할 상황은?**
- 출퇴근 길의 빌드 모니터링?
- 외근 중 긴급 결정?
- 페어 프로그래밍?

**3. Skill을 설치할 때 어떤 기준으로 신뢰성을 판단할 건가요?**

### 💭 토론거리

> "Skill을 적극 공유하는 문화 vs. 보안을 위해 신중한 문화 — 어느 쪽이 맞을까요?"
> "AI 에이전트 시대의 '소프트웨어 설치'는 무엇이 달라야 할까요?"

---

## 🆘 자주 막히는 지점

### Q1. SKILL.md를 만들었는데 Claude가 인식 못 해요

**A.** 점검 포인트:

```
!ls ~/.claude/skills/                # 디렉토리 존재 확인
!cat ~/.claude/skills/<이름>/SKILL.md  # 파일 내용 확인
/help                                # 목록에서 보이는지
```

세션 재시작이 필요할 수도 있어요:

```
/exit
claude
```

### Q2. Skill이 자동으로 호출이 안 돼요

**A.** `description` 을 점검하세요. **언제 써야 하는지** 가 명확해야 Claude가 매칭해요.

```yaml
# ❌ 모호
description: 코드 리뷰 도구

# ✅ 명확
description: Reviews Python code for PEP 8 violations and security issues. 
  Use when reviewing .py files or before merging Python PRs.
```

### Q3. Remote Control에서 "Subscription required" 에러

**A.** API 키로는 사용 불가능. OAuth 로그인 필요:

```bash
# API 키 환경변수 제거
unset ANTHROPIC_API_KEY    # Mac/Linux
$env:ANTHROPIC_API_KEY=""  # Windows PowerShell

# OAuth 로그인
claude
/login
```

### Q4. 모바일에서 QR 스캔 후 연결 안 됨

**A.** 점검 순서:

1. 데스크탑 세션이 **여전히 실행 중**인지 (꺼지면 끊김)
2. 데스크탑이 **인터넷 연결**되어 있는지
3. 폰의 Claude 앱이 **데스크탑과 같은 계정**으로 로그인됐는지
4. claude.ai/code에서 세션 이름 옆 **🟢 녹색 점** 확인

### Q5. 회사 정책으로 Skill 셸 실행이 차단됐어요

**A.** Enterprise 관리형 설정 (`disableSkillShellExecution: true`) 일 가능성. 관리자에게 문의하거나, 셸을 안 쓰는 Skill로 우회.

### Q6. Skill을 GitHub에 공유하고 싶어요

**A.** 좋아요! 다만 다음을 점검:

- [ ] API 키, 토큰 등 비밀 정보가 들어있지 않은지
- [ ] 회사 내부 정보 (URL, 시스템 이름) 노출 없는지
- [ ] README에 **사용 방법 + 보안 경고** 명시
- [ ] LICENSE 파일 추가

---

## 🎯 오늘 배운 핵심 정리

| 개념 | 한 줄 요약 |
|------|-----------|
| 📁 Skill 구조 | 디렉토리 + SKILL.md + 선택적 번들 파일 |
| 📍 Skill 위치 | `~/.claude/skills/` (개인) / `.claude/skills/` (프로젝트) |
| 📐 Frontmatter | `name`, `description`이 핵심 |
| 🌍 Agent Skills | Anthropic 발표 오픈 스탠다드 |
| 🎯 description | "무엇 + 언제" 구조로 명확히 |
| 📱 Remote Control | OAuth 필수, QR로 폰 접속 |
| 🔐 보안 모델 | Outbound HTTPS, 로컬 실행, Short-lived 토큰 |
| ⚠️ Skill 위험 | VM 샌드박싱 없음 — 신뢰가 핵심 |
| 🛡️ 방어 수단 | Frontmatter 통제 + `/permissions` + 관리형 정책 |

### 💎 가장 중요한 교훈

> **"Skill을 설치하는 건 소프트웨어를 설치하는 것과 같아요."**
> **"내 손에서 멀어진 Claude는 내 컴퓨터에서 실행되는 Claude예요."**

---

## 📚 공식 문서

- [Claude Code Skills 공식 문서](https://code.claude.com/docs/en/skills)
- [Remote Control 공식 문서](https://code.claude.com/docs/en/remote-control)
- [Agent Skills 오픈 스탠다드](https://agentskills.io)
- [Agent Skills Best Practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices)
- [Agent Skills Overview (Platform)](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview)

---

## 🎓 다음 단계

축하해요! 🎉 이제 Claude Code를 **나만의 도구로 확장**하고, **어디서든 제어**할 수 있어요.

**바로 적용해볼 만한 것:**

1. 🧰 본인 워크플로 중 **반복 작업 1개**를 Skill로 만들기
2. 📦 만든 Skill을 GitHub에 **공개 저장소**로 공유 (보안 점검 후)
3. 📱 출퇴근 길에 **Remote Control**로 빌드 모니터링 시도
4. 🔍 `/permissions` 로 **Skill 차단 규칙** 미리 설정
5. 👥 팀에서 자주 쓰는 패턴을 **공통 Project Skill**로 만들기

**더 깊이 배우고 싶다면:**

- 📘 **[명령어 레퍼런스](./claude_commands-reference.md)** — 모든 슬래시 명령어
- 🔑 **[API 키 설정 가이드](./api-key-setup.md)** — OAuth vs API 키 차이
- ✍️ **[프롬프트 & CLAUDE.md 실습](./effective-prompting-and-claude-md.md)** — Skill과 함께 쓰면 강력
- 🩺 **[/status 가이드](./status-reading-guide.md)** — 환경 점검 마스터

---

## 🌱 마무리: Fail Forward

이 실습에서:

> 🟢 **첫 Skill까지 술술 만들었다면** — 더 복잡한 멀티파일 Skill에 도전을!
> 🟡 **개념은 잡혔지만 호출이 안 되는 경우가 있었다면** — description 다듬기가 진짜 학습
> 🔴 **아직 어려운 부분이 있다면** — 한 번에 다 안 익혀도 괜찮아요. 만들고 쓰면서 자연히 손에 붙어요

학습 노트에 적어보세요:

```
✏️ 만들어보고 싶은 Skill: ___
🔥 가장 헷갈렸던 개념: ___
💡 Remote Control로 시도해볼 시나리오: ___
📱 보안 측면에서 가장 인상 깊었던 것: ___
```

📅 작성일: 2026.05.02
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
