# /status 명령어 결과 읽는 법 🔍

Claude Code 세션 안에서 **`/status`** 를 입력하면 현재 환경 정보가 한꺼번에 표시돼요. 이 화면을 읽을 줄 알면 문제 해결 속도가 10배 빨라져요!

---

## 📑 목차

- [/status가 뭐예요?](#-status가-뭐예요)
- [전체 출력 예시](#-전체-출력-예시)
- [항목별 자세히 읽기](#-항목별-자세히-읽기)
  - [1. Working Directory](#1️⃣-working-directory)
  - [2. Account](#2️⃣-account)
  - [3. Model](#3️⃣-model)
  - [4. Permissions](#4️⃣-permissions)
  - [5. IDE](#5️⃣-ide)
  - [6. MCP servers](#6️⃣-mcp-servers)
  - [7. Setting sources](#7️⃣-setting-sources)
  - [8. Memory files](#8️⃣-memory-files)
- [🚦 신호등 진단법](#-신호등-진단법)
- [🆘 자주 마주치는 시나리오](#-자주-마주치는-시나리오)
- [🎓 강의 활용 팁](#-강의-활용-팁)

---

## 🤔 /status가 뭐예요?

**한마디로:** Claude Code의 **건강검진 보고서**예요.

> 💡 **언제 쓰나요?**
> - 🚀 세션 시작할 때 (첫 점검)
> - 🐛 뭔가 이상하게 동작할 때
> - 🤝 다른 사람한테 도와달라고 할 때 (스크린샷 찍어 보내기)
> - 🎓 강의 시연 시작 전 환경 확인

### 비슷한 비교

| 익숙한 도구 | Claude Code |
|-------------|-------------|
| 🩺 건강검진 결과지 | `/status` |
| 🚗 자동차 계기판 | `/status` |
| 📱 핸드폰 설정 화면 | `/status` |

---

## 📋 전체 출력 예시

```
Working Directory:  /Users/nara/claude-code-guide
Account:            sinnara@example.com (Pro plan)
Model:              Claude Sonnet 4.6 (auto)
Permissions:        Plan mode
Plugins:            3 installed, 3 enabled
IDE:                Installed VS Code extension
MCP servers:        2 connected, 3 need auth · /mcp
Setting sources:    User settings
Memory files:       ~/.claude/CLAUDE.md, ./CLAUDE.md
```

> ⚠️ 버전에 따라 항목이 조금씩 다를 수 있어요. 핵심 항목은 비슷해요.

---

## 🔎 항목별 자세히 읽기

### 1️⃣ Working Directory

```
Working Directory:  /Users/nara/claude-code-guide
```

**의미:** Claude가 **"내 작업장"** 으로 인식하는 폴더

| 체크 포인트 | 확인 방법 |
|-------------|-----------|
| ✅ 의도한 폴더가 맞는지 | 경로 직접 확인 |
| ✅ 프로젝트 루트인지 | `package.json`, `.git` 등이 있는 폴더? |
| ❌ 서브폴더에서 시작했나? | 한 단계 위로 이동 후 재시작 |

> 💡 **중요**: Claude는 이 폴더와 그 하위 파일만 봐요. 다른 폴더는 모름!

**바꾸고 싶다면:**

```bash
# Claude를 종료하고
exit

# 원하는 폴더로 이동 후
cd /원하는/경로
claude
```

---

### 2️⃣ Account

```
Account:  sinnara@example.com (Pro plan)
```

**의미:** 현재 로그인된 계정과 플랜 정보

**플랜별 표시:**

| 표시 | 플랜 | 특징 |
|------|------|------|
| `(Free)` | 무료 | 제한적 사용 |
| `(Pro plan)` | $20/월 | 일반 개발자용 |
| `(Max plan)` | $100~$200/월 | Claude Code 무제한 가까이 |
| `(Team)` | 팀 플랜 | 팀 단위 사용 |
| `(API)` | API 키 사용 | 종량제 |

**계정 전환:**

```
/login    # 다른 계정으로 로그인
/logout   # 로그아웃
```

---

### 3️⃣ Model

```
Model:  Claude Sonnet 4.6 (auto)
```

**의미:** 현재 대화에 사용되는 Claude 모델

**모델 종류:**

| 모델 | 특징 | 추천 작업 |
|------|------|-----------|
| **Opus** | 가장 똑똑함, 느리고 비쌈 | 복잡한 리팩토링, 설계 |
| **Sonnet** | 균형 잡힘 (기본값) | 일반 코딩 |
| **Haiku** | 빠르고 저렴 | 간단한 질문, 자동화 |

**`(auto)` 표시 의미:**

> 자동으로 적절한 모델 선택 모드. 보통 Opus로 시작하고, 사용량 50% 넘으면 Sonnet으로 자동 전환해서 비용 절약.

**바꾸고 싶다면:**

```
/model    # 모델 선택 메뉴 열기
```

---

### 4️⃣ Permissions

```
Permissions:  Plan mode
```

**의미:** 현재 권한 모드 (Claude가 작업할 때 어떻게 동작할지)

| 표시 | 모드 | 동작 |
|------|------|------|
| `Default` | 기본 | 매 작업마다 허락받기 |
| `Plan mode` | 계획 모드 | 계획만 짜고 승인 대기 |
| `Accept Edits` | 편집 자동 수락 | 파일 편집은 알아서 |
| `Auto` | 완전 자동 | 모든 작업 자동 ⚠️ |

**전환 방법:**

- `Shift+Tab` 누르기 (모드 순환)
- 또는 `/permissions` 명령어

> 🎓 **강의 시연용 추천**: `Plan mode`

---

### 5️⃣ IDE

```
IDE:  Installed VS Code extension
```

**의미:** 현재 연결된 IDE 정보

**가능한 표시:**

| 표시 | 의미 | 상태 |
|------|------|------|
| `Installed VS Code extension` | VS Code 확장 정상 작동 | ✅ |
| `Installed Cursor extension` | Cursor에서 사용 중 | ✅ |
| `Installed JetBrains plugin` | JetBrains에서 사용 중 | ✅ |
| `No IDE detected` | 일반 터미널에서 실행 | ⚪ (정상) |
| `IDE not found` | 외부 터미널 → IDE 연결 필요 | ⚠️ |

**연결 안 된 경우:**

```
/ide    # 현재 열린 IDE에 연결 시도
```

---

### 6️⃣ MCP servers

```
MCP servers:  2 connected, 3 need auth · /mcp
```

**의미:** 외부 서비스(GitHub, Slack, Notion 등)와의 연결 상태

> 💡 **MCP가 뭐예요?**  
> Model Context Protocol의 줄임말. Claude가 **외부 도구·서비스와 대화할 수 있게 해주는 다리** 예요.

### 상태별 의미

| 표시 | 의미 | 액션 필요? |
|------|------|-----------|
| `connected` | ✅ 정상 작동 | 없음 |
| `need auth` | 🔐 인증 필요 (로그인 안 됨) | `/mcp` 로 로그인 |
| `failed` | ❌ 연결 실패 | 설정 확인 |
| `pending` | ⏳ 연결 시도 중 | 기다리기 |

### 인증이 필요한 서버 처리하기

```
/mcp
```

→ 메뉴가 열리면 인증 안 된 서버 옆에 **"Authenticate"** 버튼 클릭

→ 보통 브라우저 창이 열리고 OAuth 로그인 진행

→ 완료되면 다시 `/status` 로 확인

### 자주 만나는 케이스

**✅ 모두 connected:**
```
MCP servers:  5 connected
```
→ 모든 외부 도구 사용 준비 완료!

**⚠️ 일부 need auth:**
```
MCP servers:  2 connected, 3 need auth · /mcp
```
→ 3개 서버 로그인 필요. `/mcp` 실행해서 마무리.

**❌ 전부 failed:**
```
MCP servers:  0 connected, 5 failed
```
→ 인터넷 연결 또는 설정 확인. `claude mcp list` 로 상세 진단.

---

### 7️⃣ Setting sources

```
Setting sources:  User settings
```

**의미:** 현재 적용 중인 설정의 출처

### 설정 파일의 4단계 우선순위

```
🏢 Enterprise (회사 강제 설정)        ← 최우선
   ↓
🔒 Project Local (이 프로젝트 + 로컬만)
   ↓
📁 Project (이 프로젝트, 팀 공유)
   ↓
👤 User (내 모든 프로젝트)              ← 기본
```

| 표시 | 파일 위치 | 적용 범위 |
|------|-----------|-----------|
| `User settings` | `~/.claude/settings.json` | 내 모든 프로젝트 |
| `Project settings` | `.claude/settings.json` | 이 프로젝트만 (팀 공유) |
| `Local settings` | `.claude/settings.local.json` | 이 프로젝트만 (git 제외) |
| `Enterprise settings` | OS별 시스템 경로 | 회사 강제 설정 |

### 자주 만나는 케이스

**개인 작업:**
```
Setting sources:  User settings
```
→ 내 글로벌 설정만 적용 중

**팀 프로젝트:**
```
Setting sources:  User settings, Project settings
```
→ 내 설정 + 팀 공통 설정 같이 적용

**회사 환경:**
```
Setting sources:  User settings, Project settings, Enterprise settings
```
→ 회사 정책이 추가로 적용 중

> 💡 **팀과 설정 공유하고 싶다면**: 프로젝트 루트에 `.claude/settings.json` 만들어서 git에 커밋

---

### 8️⃣ Memory files

```
Memory files:  ~/.claude/CLAUDE.md, ./CLAUDE.md
```

**의미:** Claude가 자동으로 읽어들이는 컨텍스트 파일들

> 💡 **CLAUDE.md가 뭐예요?**  
> 프로젝트 안내서예요. Claude가 매 세션 시작할 때 자동으로 읽고, 코딩 스타일/아키텍처/주의사항을 알게 돼요.

### 우선순위

```
1. ~/.claude/CLAUDE.md      ← 글로벌 (모든 프로젝트)
2. ./CLAUDE.md              ← 현재 프로젝트
3. ./하위폴더/CLAUDE.md     ← 특정 영역
```

### 비유로 이해하기

마치 **회사 입사할 때 받는 안내문** 같아요:

| 안내문 | CLAUDE.md |
|--------|-----------|
| 회사 전체 규칙 | `~/.claude/CLAUDE.md` (글로벌) |
| 우리 팀 규칙 | `./CLAUDE.md` (프로젝트) |
| 우리 부서 규칙 | `./src/components/CLAUDE.md` (영역별) |

**없으면 어떻게 만들어요?**

```
/init
```

→ Claude가 프로젝트를 분석해서 자동으로 `CLAUDE.md` 생성!

---

## 🚦 신호등 진단법

`/status` 출력을 빠르게 진단하는 방법이에요.

### 🟢 모두 정상 (Go!)

```
Working Directory:  ✅ 의도한 폴더
Account:            ✅ 로그인됨
Model:              ✅ 적절한 모델
Permissions:        ✅ 작업에 맞는 모드
IDE:                ✅ 연결됨 (또는 N/A)
MCP servers:        ✅ 모두 connected
Setting sources:    ✅ 의도한 설정
Memory files:       ✅ CLAUDE.md 인식
```

→ **자유롭게 작업 시작!** 🚀

### 🟡 점검 필요 (Caution)

```
MCP servers:  2 connected, 3 need auth · /mcp     ← 인증 필요
Memory files: (none)                              ← CLAUDE.md 없음
```

→ **기본 작업은 가능**하지만 일부 기능 제한. 필요시 `/mcp` 또는 `/init`

### 🔴 문제 있음 (Stop!)

```
Working Directory:  /Users/wrong/folder           ← 잘못된 폴더!
Account:            (not logged in)               ← 로그인 안 됨
MCP servers:        0 connected, 5 failed         ← 모두 실패
```

→ **작업 중단**, 환경부터 정리

---

## 🆘 자주 마주치는 시나리오

### 시나리오 1: "MCP servers 3 need auth"

```
MCP servers: 2 connected, 3 need auth · /mcp
```

**해결:**

```
/mcp
```

→ 메뉴에서 인증 안 된 서버마다 **"Authenticate"** 클릭  
→ 브라우저에서 로그인 → 완료

### 시나리오 2: "No IDE detected"인데 IDE에서 작업 중

```
IDE: No IDE detected
```

**원인:** 외부 터미널에서 실행하거나 IDE 확장 설치 안 됨

**해결:**

```bash
# 옵션 1: IDE 통합 터미널에서 실행
# (VS Code: Ctrl+`, JetBrains: Alt+F12)

# 옵션 2: 외부 터미널에서 강제 연결
/ide
```

### 시나리오 3: Working Directory가 잘못됐어요

```
Working Directory: /Users/nara/wrong-folder
```

**해결:**

```bash
# 1. Claude 종료
/exit       # 또는 Ctrl+D

# 2. 올바른 폴더로 이동
cd /Users/nara/correct-project

# 3. 다시 실행
claude
```

### 시나리오 4: 모델이 자꾸 바뀌어요

```
Model: Claude Haiku 4.5    ← 어? Opus 쓰고 있었는데?
```

**원인:** Auto 모드에서 사용량에 따라 자동 전환됨 (정상 동작!)

**해결:**

```
/model
# Opus 4.7 직접 선택
```

### 시나리오 5: 권한 모드가 자꾸 Default로 돌아가요

```
Permissions: Default
```

**원인:** 세션마다 초기화됨

**해결:** 시작 시 옵션으로 지정

```bash
claude --permission-mode plan
```

또는 설정 파일(`~/.claude/settings.json`)에 영구 저장:

```json
{
  "initialPermissionMode": "plan"
}
```

### 시나리오 6: CLAUDE.md가 인식 안 돼요

```
Memory files: (none)
```

**점검:**

```bash
# 1. 파일 존재 확인
!ls -la CLAUDE.md

# 2. 파일이 없다면 자동 생성
/init

# 3. 위치 확인 (반드시 Working Directory 루트에)
!pwd
```

---

## 🎓 강의 활용 팁

### 강의 시작 전 환경 점검 체크리스트

학습자에게 **`/status`** 실행하고 스크린샷 보내달라고 요청해보세요:

```
✅ Working Directory: 강의용 실습 폴더가 맞나?
✅ Account: 로그인 완료?
✅ Model: Sonnet 또는 Opus 적절히 설정?
✅ Permissions: Plan mode (시연용)
✅ IDE: VS Code/JetBrains 연결 확인
✅ MCP servers: 강의에 필요한 서버 연결?
```

### 학습자 디버깅 1단계: "/status부터 보여주세요"

문제가 생겼을 때 학습자에게 항상 먼저 요청:

> 💬 "/status 결과를 캡처해서 보내주세요"

90%의 환경 문제는 이 한 화면으로 진단 가능해요!

### 강의 슬라이드용 정리

```
🩺 /status는 Claude Code의 건강검진
📋 8가지 핵심 정보 한눈에 확인
🚦 신호등 색깔처럼 빠르게 진단
🆘 문제 생기면 /status부터!
```

---

## 📚 관련 명령어

`/status`와 함께 알아두면 좋은 명령어들:

| 명령어 | 용도 |
|--------|------|
| `/status` | **전체 환경 점검** (이 가이드 주제) |
| `/usage` | 토큰·비용 사용량 확인 |
| `/cost` | 현재 세션 비용 |
| `/config` | 설정 변경 |
| `/mcp` | MCP 서버 관리 |
| `/model` | 모델 변경 |
| `/permissions` | 권한 모드 변경 |
| `claude doctor` | 더 자세한 환경 진단 (셸에서) |

---

## 🎓 다음 단계

`/status` 마스터했다면 다음으로:

- 📘 **[명령어 레퍼런스](./commands-reference.md)** — 더 많은 슬래시 명령어
- 🖥️ **[인터페이스 이해](./interface-overview.md)** — 화면 구성 다시 보기
- 🎬 **[Hello World 실습](./first-conversation-hello-world.md)** — 직접 시연해보기

---

📅 작성일: 2026.04.27  
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
