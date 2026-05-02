# Claude HUD 설치 & 동작 확인 실습 📊

> Claude Code 화면 아래 **상태 표시줄**에 컨텍스트, 도구 활동, 에이전트, Todo 진행 상황을 띄우는 플러그인이에요.
> "지금 Claude가 뭘 하고 있는지" 한눈에 보면서 작업하고 싶다면 필수!

---

## 🎯 학습 목표

이 실습을 마치면 다음을 할 수 있어요:

- ✅ **Claude HUD 플러그인** 의 역할과 효과 이해
- ✅ Marketplace 추가 → 설치 → 리로드 → 설정의 **4단계 흐름** 체득
- ✅ `/reload-plugins` 로 설치 상태 **검증**
- ✅ `/claude-hud:setup` 으로 상태바 활성화
- ✅ 흔한 OS별 설치 함정 **회피**

---

## 📑 목차

- [시작하기 전에](#-시작하기-전에)
- [1. Claude HUD 소개](#1️⃣-claude-hud-소개)
- [2. 사전 준비 (Node.js 등)](#2️⃣-사전-준비-nodejs-등)
- [3. 4단계 설치 흐름](#3️⃣-4단계-설치-흐름)
- [4. /reload-plugins 로 동작 확인 실습](#4️⃣-reload-plugins-로-동작-확인-실습)
- [5. /claude-hud:setup 으로 상태바 활성화](#5️⃣-claude-hudsetup-으로-상태바-활성화)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [🪞 5분 회고](#-5분-회고)
- [📚 공식 문서](#-공식-문서)
- [🎓 다음 단계](#-다음-단계)

---

## 📋 시작하기 전에

- ✅ Claude Code **v1.0.80+** 설치 완료 → [설치 가이드](./claude-code-install-guide.md)
- ✅ 인증 완료 (구독 또는 API 키) → [API 키 설정 가이드](./api-key-setup.md)
- ✅ Node.js 18+ 설치
- ✅ 마음의 준비: **"한 번만 설정하면 매 세션 자동으로 떠요"** 🌱

> ⏱ **소요 시간**: 약 15~25분
> 🎯 **권장 모드**: 아무 모드 OK (설치만 하는 작업)

### 작업 폴더 준비

설치는 **어느 폴더에서 시작해도** 됩니다. 어차피 글로벌 플러그인이니까요.

```bash
claude
```

---

## 1️⃣ Claude HUD 소개

### 🤔 Claude HUD가 뭐예요?

**한마디로**: 입력창 아래에 항상 떠 있는 **계기판(HUD = Heads-Up Display)** 이에요.

### 🖼️ 어떤 정보가 보여요?

```
[Opus] │ my-project git:(main*)
Context █████░░░░░ 45% │ Usage ██░░░░░░░░ 25% (1h 30m / 5h)
◐ Edit: auth.ts | ✓ Read ×3 | ✓ Grep ×2        ← 도구 활동 (옵션)
◐ explore [haiku]: Finding auth code (2m 15s)    ← 에이전트 상태 (옵션)
▸ Fix authentication bug (2/5)                   ← Todo 진행 (옵션)
```

### 🎯 어떤 점이 좋아요?

| 보이는 정보 | 왜 유용한가? |
|------------|--------------|
| 🤖 **모델 이름** | Opus 쓰는지 Sonnet 쓰는지 즉시 확인 |
| 📁 **프로젝트 경로 + Git 브랜치** | "지금 어디 있지?" 헷갈릴 일 없음 |
| 📊 **컨텍스트 사용량** | 80% 넘기 전에 `/compact` 타이밍 잡기 |
| 📈 **Usage 한도** | 구독 한도 남은 양 실시간 확인 |
| 🛠 **도구 활동** | Claude가 지금 어떤 파일을 읽는지 보임 |
| 🤝 **서브에이전트** | 어떤 에이전트가 뭘 하는지 |
| ✅ **Todo 진행** | 작업 완료 진척률 |

### 비유로 이해하기

| 익숙한 것 | Claude HUD |
|----------|------------|
| 🚗 자동차 계기판 | 속도·연료·RPM을 항상 보여줌 |
| ✈️ 비행기 HUD | 핵심 정보를 시야에서 안 떼고 |
| ⌚ 스마트워치 | 굳이 화면 안 봐도 핵심만 |

> 💡 **`/status` 와의 차이**: `/status`는 **요청해야 보이는 일회성 보고서**, Claude HUD는 **항상 떠 있는 실시간 표시**.

---

## 2️⃣ 사전 준비 (Node.js 등)

### 📋 시스템 요구사항

| 항목 | 요구 사양 |
|------|-----------|
| **Claude Code** | v1.0.80 이상 |
| **macOS / Linux** | Node.js 18+ 또는 Bun |
| **Windows** | Node.js 18+ (Bun 미지원) |

### 🔍 현재 버전 확인

```bash
claude --version       # v1.0.80 이상이어야 함
node --version         # v18 이상이어야 함
```

### 📦 Node.js 설치 방법 (OS별)

#### 🍎 macOS

```bash
# Homebrew 사용
brew install node

# 또는 nvm 사용
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install 20
```

#### 🐧 Linux (Ubuntu/Debian)

```bash
sudo apt install nodejs npm

# 또는 NodeSource (최신 LTS)
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install nodejs
```

#### 🪟 Windows

```powershell
winget install OpenJS.NodeJS.LTS
```

설치 후 **PowerShell을 재시작** 해야 PATH가 갱신됩니다.

---

## 3️⃣ 4단계 설치 흐름

### 🗺️ 전체 그림

```
①  Marketplace 등록     → 어느 저장소에서 받을지 알려주기
       ↓
②  플러그인 설치         → 실제 다운로드 + 적용
       ↓
③  /reload-plugins       → Claude가 새 플러그인을 인식하게 리로드
       ↓
④  /claude-hud:setup     → 상태바 자동 구성
```

### 🎬 Step 1. Marketplace 등록

Claude Code 세션 안에서:

```
/plugin marketplace add sinnarasam/claude-hud
```

> 💡 `sinnarasam/claude-hud` 는 본 가이드 작성자의 fork 저장소예요. 원본은 `jarrodwatts/claude-hud` 입니다. 둘 다 같은 방식으로 동작해요.

✅ 정상 응답 예시:

```
Added marketplace: sinnarasam/claude-hud
```

### 🎬 Step 2. 플러그인 설치

```
/plugin install claude-hud
```

> ⚠️ **Linux 사용자 주의**: `/tmp` 가 별도 파일시스템(tmpfs)이면 `EXDEV: cross-device link not permitted` 에러가 날 수 있어요. 이 경우 Claude Code를 종료하고 다음으로 시작하세요:
>
> ```bash
> mkdir -p ~/.cache/tmp && TMPDIR=~/.cache/tmp claude
> ```

✅ 정상 응답 예시:

```
Installed plugin: claude-hud
Run /reload-plugins to activate.
```

### 🎬 Step 3. `/reload-plugins`

```
/reload-plugins
```

✅ 정상 응답 예시:

```
Plugins reloaded.
```

### 🎬 Step 4. 상태바 자동 구성

```
/claude-hud:setup
```

→ 가이드 흐름이 시작돼요. 프리셋 선택 → 언어 선택 → 옵션 토글.

> 🪟 **Windows 사용자 주의**: setup이 `no JavaScript runtime was found` 라고 나오면 Node.js LTS 설치 후 셸 재시작:
>
> ```powershell
> winget install OpenJS.NodeJS.LTS
> ```

설정 완료 후 **Claude Code를 완전히 재시작** 해야 새 statusLine 구성이 적용돼요.

---

## 4️⃣ /reload-plugins 로 동작 확인 실습

### 🎯 왜 동작 확인이 중요해요?

플러그인 설치는 **3가지 단계** 가 모두 성공해야 진짜 동작해요:

```
다운로드 OK ✅ → Claude가 인식 OK ✅ → 슬래시 명령 등록 OK ✅
```

`/reload-plugins` 는 **두 번째와 세 번째** 를 한 번에 갱신하는 명령이에요.

### 🧪 검증 시나리오

#### Step 1. 리로드 실행

```
/reload-plugins
```

#### Step 2. 슬래시 메뉴에서 확인

입력창에 `/` 만 치고 멈춰보세요. 자동완성 메뉴에서 다음 두 명령이 보여야 정상:

```
/claude-hud:setup
/claude-hud:configure
```

#### Step 3. `/help` 로 전체 목록 확인

```
/help
```

→ Claude HUD 관련 명령이 목록에 있는지 스크롤하며 확인.

#### Step 4. 플러그인 목록 직접 확인

```
/plugin
```

→ 설치된 플러그인 목록에 **`claude-hud`** 가 떠 있어야 해요.

### 🚦 신호등 진단

| 결과 | 상태 | 다음 행동 |
|------|------|-----------|
| 🟢 `/claude-hud:*` 명령이 자동완성에 보임 | 정상 | Step 5로 진행 |
| 🟡 명령은 보이는데 실행 시 에러 | 부분 설치 | Node.js 버전 확인 |
| 🔴 `/help` 에 명령이 없음 | 미설치 | Step 1~3 다시 실행 |

### 🏋️ 실습 미션

```
1. /plugin marketplace list 로 등록된 marketplace 확인
2. /plugin 으로 claude-hud 가 설치된 상태인지 확인
3. /reload-plugins 한 번 더 실행
4. /help 에서 claude-hud 명령어 갯수 세기 (2개여야 정상)
```

---

## 5️⃣ /claude-hud:setup 으로 상태바 활성화

### 🎬 setup 가이드 흐름

```
/claude-hud:setup
```

대화형 마법사가 진행돼요. 차례대로:

#### ① 프리셋 선택

| 프리셋 | 표시 내용 | 추천 대상 |
|--------|-----------|----------|
| **Full** | 전부 — 도구·에이전트·Todo·Git·Usage·시간 | 🎓 강의 시연·관찰 학습 |
| **Essential** | 활동 라인 + Git 상태 (군더더기 X) | 일반 개발자 |
| **Minimal** | 모델 이름 + 컨텍스트 바만 | 깔끔 선호 |

> 💡 **처음이면 Essential 추천**. 익숙해지면 항목 켜고 끄면 돼요.

#### ② 언어 선택

```
en  (English, 기본)
zh  (中文)
```

> ℹ️ 한국어 라벨은 아직 미지원. 영문이 가장 호환성 좋아요.

#### ③ 개별 토글 (선택)

도구 활동, 에이전트, Todo 라인 등을 켜고 끄기.

### 🔄 Claude Code 재시작

설정 저장 후 **반드시 재시작**:

```
/exit
```

```bash
claude
```

> 🪟 **Windows**: `/exit` 만으론 부족할 수 있어요. **PowerShell 자체를 닫았다 다시 열어** `claude` 실행하세요.

### ✅ 최종 확인

새 세션이 뜨면 입력창 아래 다음과 비슷한 줄이 보여야 해요:

```
[Sonnet] │ my-project git:(main*)
Context █████░░░░░ 45% │ Usage ██░░░░░░░░ 25% (1h 30m / 5h)
```

🎉 **성공!** 이제 매 세션마다 자동으로 뜹니다.

### ⚙️ 나중에 설정 바꾸고 싶다면

```
/claude-hud:configure
```

→ 같은 마법사가 다시 열려서 옵션을 바꿀 수 있어요.

---

## 🆘 자주 막히는 지점

### Q1. `/plugin: command not found` 같은 에러

**A.** Claude Code 버전이 너무 낮을 수 있어요.

```bash
claude --version
# v1.0.80 미만이면 업데이트
```

업데이트:

```bash
# Homebrew
brew upgrade claude-code

# npm
npm update -g @anthropic-ai/claude-code

# 또는 재설치
curl -fsSL https://claude.ai/install.sh | bash
```

### Q2. Linux에서 `EXDEV: cross-device link not permitted`

**A.** `/tmp` 와 홈 디렉토리가 다른 파일시스템이라 발생.

```bash
# Claude Code 종료 후
mkdir -p ~/.cache/tmp
TMPDIR=~/.cache/tmp claude
```

이 세션에서 다시 `/plugin install claude-hud` 시도.

### Q3. Windows에서 `no JavaScript runtime was found`

**A.** Node.js 미설치 또는 PATH 미반영.

```powershell
# 설치
winget install OpenJS.NodeJS.LTS

# 설치 후 PowerShell 완전히 닫고 새로 열기
node --version    # v18 이상이어야 함

# 다시 시도
claude
/claude-hud:setup
```

### Q4. `/reload-plugins` 했는데도 명령이 안 보여요

**A.** 점검 순서:

```
/plugin marketplace list      # marketplace 등록됐나?
/plugin                       # claude-hud가 installed 상태인가?
/reload-plugins               # 다시 한 번
/help                         # claude-hud:setup 검색
```

그래도 안 되면 Claude Code 자체를 재시작:

```
/exit
claude
```

### Q5. setup 끝났는데 상태바가 안 보여요

**A.** 가장 흔한 원인은 **재시작 미실시**.

- macOS: 터미널 앱 자체를 완전히 종료(`Cmd+Q`) 후 재실행
- Windows: PowerShell 창을 완전히 닫고 새로 열기
- Linux: 터미널 닫고 다시 열기

또는 statusLine 설정이 제대로 쓰였는지 직접 확인:

```bash
!cat ~/.claude/settings.json | grep statusLine
```

`statusLine` 항목에 claude-hud 관련 명령이 있어야 정상.

### Q6. 한국어 설정이 없어요

**A.** 현재(2026-05 기준) `en` / `zh` 만 공식 지원이에요. 한국어는 아직 미지원이지만 GitHub Issue로 요청하면 추가될 수 있어요.

### Q7. 이미 설치되어 있다고 나와요

**A.** 좋은 소식! 이미 설치된 거예요. 곧바로:

```
/claude-hud:setup       # 처음 설정
/claude-hud:configure   # 기존 설정 변경
```

---

## 🪞 5분 회고

여기까지 따라왔다면 정말 대단해요! 잠시 멈추고 돌아봐요.

### 📝 스스로에게 던질 질문

**1. 설치 4단계 중 가장 헷갈렸던 단계는?**
- Marketplace 등록?
- 플러그인 설치?
- `/reload-plugins`?
- `/claude-hud:setup`?

**2. 어떤 정보를 항상 보고 싶나요?**
- 컨텍스트 사용량만으로 충분?
- 도구 활동까지 보고 싶은지?
- Todo 진행을 보면 동기 부여될지?

**3. `/status` (요청형) 와 HUD (상시) 의 차이를 본인 워크플로에 어떻게 녹일 수 있을까요?**

### 💭 토론거리

> "정보가 더 많이 보인다 = 항상 좋은가? 노이즈가 되는 순간은 언제일까?"
> "AI 도구의 **'시야 정보'** 가 우리 사고에 어떻게 영향을 줄까?"

---

## 🎯 오늘 배운 핵심 정리

| 단계 | 핵심 |
|------|------|
| 1️⃣ Marketplace 등록 | `/plugin marketplace add <user>/<repo>` |
| 2️⃣ 플러그인 설치 | `/plugin install claude-hud` |
| 3️⃣ 리로드·검증 | `/reload-plugins` 후 `/help`에서 `claude-hud:` 검색 |
| 4️⃣ 상태바 활성화 | `/claude-hud:setup` → 재시작 |
| 🎨 설정 변경 | `/claude-hud:configure` |

### 💎 가장 중요한 교훈

> **"설치(install)와 인식(reload)은 별개의 단계예요."**
> **"눈에 보이는 정보가 사고의 속도를 바꿔요."**

---

## 📚 공식 문서

- [Claude HUD GitHub (sinnarasam fork)](https://github.com/sinnarasam/claude-hud)
- [Claude HUD GitHub (jarrodwatts 원본)](https://github.com/jarrodwatts/claude-hud)
- [Claude Code 플러그인 시스템 공식 문서](https://docs.claude.com/en/docs/claude-code/overview)
- [statusLine 설정 레퍼런스](https://code.claude.com/docs/en/terminal-config)

---

## 🎓 다음 단계

축하해요! 🎉 이제 Claude Code 작업이 **훨씬 더 시각적**으로 변했어요.

**바로 시도해볼 만한 것:**

1. 🎨 `/claude-hud:configure` 로 도구·에이전트·Todo 라인 켜보기
2. 🌈 `~/.claude/plugins/claude-hud/config.json` 직접 편집해서 색상 커스터마이징
3. 🧪 컨텍스트 80% 도달 시 색상 변화 관찰 → `/compact` 타이밍 익히기
4. 📦 다른 유용한 플러그인도 같은 방식으로 설치 시도

**더 깊이 배우고 싶다면:**

- 🛠 **[Skills & Remote Control 가이드](./skills-and-remote-control.md)** — 플러그인이 제공하는 Skill 활용
- 📘 **[명령어 레퍼런스](./claude_commands-reference.md)** — `/plugin`, `/help` 자세히
- 🩺 **[/status 가이드](./status-reading-guide.md)** — HUD와 함께 쓰면 시너지
- 🖥️ **[인터페이스 가이드](./claude_interface-overview.md)** — 상태 표시줄 위치 다시 확인

---

## 🌱 마무리: Fail Forward

이 실습에서:

> 🟢 **4단계가 술술 끝났다면** — 다른 플러그인도 도전을!
> 🟡 **OS별 함정에 한 번 빠졌다 빠져나왔다면** — 진짜 학습이 일어난 거예요
> 🔴 **아직 어딘가 막혔다면** — `/plugin` 으로 현재 상태 먼저 확인하면 길이 보여요

학습 노트에 적어보세요:

```
✏️ 가장 헷갈렸던 단계: ___
🔥 OS별로 만난 함정: ___
💡 켜놓고 싶은 HUD 라인: ___
🎨 다음에 시도할 플러그인: ___
```

📅 작성일: 2026.05.02
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
