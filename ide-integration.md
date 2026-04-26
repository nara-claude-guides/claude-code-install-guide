# Claude Code IDE 연동 가이드 🧩

VS Code, Cursor, JetBrains에서 Claude Code를 사용하는 방법을 한 번에 정리했습니다.

---

## 📑 목차

- [왜 IDE 연동이 필요할까?](#-왜-ide-연동이-필요할까)
- [공통 사전 준비](#-공통-사전-준비)
- [1. VS Code 연동](#1️⃣-vs-code-연동)
- [2. Cursor 연동](#2️⃣-cursor-연동)
- [3. JetBrains 연동 (IntelliJ / PyCharm / WebStorm 등)](#3️⃣-jetbrains-연동-intellij--pycharm--webstorm-등)
- [⌨️ 핵심 단축키 모음](#️-핵심-단축키-모음)
- [💪 강력한 IDE 연동 기능](#-강력한-ide-연동-기능)
- [🪟 Windows WSL 사용자 추가 설정](#-windows-wsl-사용자-추가-설정)
- [🆘 자주 발생하는 문제](#-자주-발생하는-문제)
- [📚 공식 문서](#-공식-문서)

---

## 🎯 왜 IDE 연동이 필요할까?

터미널만으로도 Claude Code는 완벽하게 동작하지만, IDE와 연동하면 다음과 같은 장점이 생깁니다.

| 항목 | 터미널만 사용 | IDE 연동 |
|------|---------------|----------|
| 코드 변경 검토 | 터미널 텍스트 diff | **IDE 네이티브 diff 뷰어** |
| 파일 컨텍스트 | 수동으로 경로 입력 | **선택 영역 자동 공유** |
| 에러/린트 정보 | 복사·붙여넣기 필요 | **자동 진단 정보 공유** |
| 파일 참조 | `@파일경로` 직접 입력 | **단축키로 `@File#L1-99` 삽입** |
| 작업 흐름 | 창 전환 잦음 | **에디터 내에서 완결** |

> 💡 IDE 연동은 **선택사항**입니다. SSH 환경이나 서버 작업에서는 터미널만으로도 충분합니다.

---

## 📋 공통 사전 준비

```bash
# 1. Claude Code 설치 확인
claude --version

# 설치되어 있지 않다면
npm install -g @anthropic-ai/claude-code

# 2. 인증 확인
claude
# 처음이라면 OAuth 로그인 또는 API 키 입력 진행
```

> 📌 인증 방식은 [API 키 설정 가이드](./api-key-setup.md)를 참고하세요.

---

## 1️⃣ VS Code 연동

### 📥 설치 방법 (3가지 중 택1)

**방법 A. Extensions 마켓플레이스에서 설치 (가장 권장)**

1. VS Code 실행
2. `Cmd+Shift+X` (Mac) 또는 `Ctrl+Shift+X` (Windows/Linux)로 Extensions 패널 열기
3. **"Claude Code"** 검색 → Anthropic 공식 확장 선택
4. **Install** 클릭

**방법 B. 통합 터미널에서 자동 설치**

```bash
# VS Code 통합 터미널 (Ctrl+`) 열고 실행
claude
# → Claude Code가 VS Code를 감지하고 자동으로 확장 설치를 제안
```

**방법 C. 외부 터미널에서 연결**

```bash
# VS Code를 이미 열어둔 상태에서 외부 터미널에서 claude 실행 후
/ide
# → 실행 중인 VS Code 인스턴스에 자동 연결
```

### ✅ 설치 확인

1. VS Code 좌측 사이드바에 Claude Code 아이콘 확인
2. `Cmd+Shift+P` (Mac) / `Ctrl+Shift+P` (Win/Linux) → `"Claude Code"` 입력 시 명령어 노출
3. 클릭하면 사이드 패널에 채팅 UI 표시

### 🔧 권장 설정

```bash
# VS Code 명령 팔레트에서:
# "Shell Command: Install 'code' command in PATH" 실행
# → 어디서든 `code .`로 VS Code 열기 가능
```

VS Code 설정(`settings.json`)에 추가:

```json
{
  "claudeCode.initialPermissionMode": "plan"
}
```

> 💡 **Plan 모드**: Claude가 작업 계획을 먼저 보여주고, 승인 후 실행합니다. **강의 시연·학습용으로 추천!**

---

## 2️⃣ Cursor 연동

> Cursor는 VS Code 기반이므로 **같은 확장**을 사용합니다.

### 📥 설치 방법

1. Cursor 실행
2. `Cmd+Shift+X` / `Ctrl+Shift+X`로 Extensions 열기
3. **"Claude Code"** 검색 → Install
4. (권장) 명령 팔레트에서 **"Install 'cursor' command in PATH"** 실행

### ⚠️ Cursor 사용 시 주의점

- Cursor 내장 AI(Tab 자동완성, Composer)와 **별개**로 동작합니다
- Cursor의 모델 사용량과 Claude Code 사용량은 **각각 따로 과금**
- 강의 시연 시에는 충돌 방지를 위해 Cursor의 자동 제안 일시 끄기를 권장

```
Cursor Settings → Features → Cursor Tab → Disable (강의 중에만)
```

---

## 3️⃣ JetBrains 연동 (IntelliJ / PyCharm / WebStorm 등)

### 🎯 지원 IDE

| IDE | 주 사용 분야 |
|-----|--------------|
| IntelliJ IDEA | Java / Kotlin / Spring |
| PyCharm | Python / Django / FastAPI |
| WebStorm | JavaScript / TypeScript / React |
| GoLand | Go |
| PhpStorm | PHP / Laravel |
| Android Studio | Android / Kotlin |
| RubyMine | Ruby / Rails |
| Rider | .NET / C# |
| CLion | C / C++ |

> ⚠️ JetBrains 플러그인은 현재 **Beta 단계**입니다. 일부 UI/기능이 변경될 수 있습니다.

### 📥 설치 방법

**Step 1. 플러그인 설치**

1. JetBrains IDE 실행
2. `Settings` (Mac: `Cmd+,` / Win/Linux: `Ctrl+Alt+S`)
3. **Plugins** → **Marketplace** 탭
4. **"Claude Code"** 검색 → Anthropic 공식 플러그인 선택
5. **Install** 클릭
6. **IDE 완전 재시작** (중요!)

**Step 2. CLI 연결 확인**

```bash
# IDE 하단 통합 터미널 열기 (Alt+F12)
# 프로젝트 루트에서 실행
claude
```

**Step 3. 플러그인 설정**

`Settings → Tools → Claude Code [Beta]` 에서:

| 설정 항목 | 권장 값 | 설명 |
|-----------|---------|------|
| **Claude command** | `claude` (자동 감지) | CLI 경로. 못 찾으면 절대경로 입력 (예: `/usr/local/bin/claude`) |
| **Suppress notification** | OFF | 처음에는 켜두고 문제 파악 후 끄기 |
| **Option+Enter for multi-line** (Mac) | ON | 여러 줄 프롬프트 입력 시 편리 |
| **Enable automatic updates** | ON | 플러그인 자동 업데이트 |

### ✅ 설치 확인

1. IDE 우측 툴 윈도우에 **Claude** 패널 표시
2. 코드 선택 후 `Cmd+Esc` / `Ctrl+Esc` → Claude 패널이 선택 영역 인식
3. Claude가 코드 수정 시 **JetBrains 네이티브 Diff 뷰어**로 표시

### 🔧 CLI를 못 찾을 때 (PATH 문제)

특히 `nvm`, `mise`, `asdf` 같은 Node 버전 관리자 사용 시 자주 발생합니다.

```bash
# 1. claude 절대 경로 확인
which claude        # Mac/Linux
where claude        # Windows

# 결과 예시: /Users/sinnara/.nvm/versions/node/v20.10.0/bin/claude
```

→ `Settings → Tools → Claude Code → Claude command`에 위 절대경로 입력

---

## ⌨️ 핵심 단축키 모음

### VS Code / Cursor

| 단축키 (Mac / Win·Linux) | 기능 |
|--------------------------|------|
| `Cmd+Esc` / `Ctrl+Esc` | **Claude 패널 ↔ 에디터 토글** |
| `Cmd+Shift+P` / `Ctrl+Shift+P` | 명령 팔레트 (Claude Code 명령어 검색) |
| `Ctrl+`` ` (백틱) | 통합 터미널 열기 |
| `/` (Claude 입력창) | 명령 메뉴 (파일 첨부, 모델 변경 등) |

### JetBrains

| 단축키 (Mac / Win·Linux) | 기능 |
|--------------------------|------|
| `Cmd+Esc` / `Ctrl+Esc` | **Claude 빠른 실행** |
| `Cmd+Option+K` / `Alt+Ctrl+K` | **파일 참조 삽입** (`@File#L1-99`) |
| `Alt+F12` | 통합 터미널 열기 |

### Claude Code 내부 슬래시 명령어

```
/ide              # 외부 터미널에서 IDE에 연결
/status           # 현재 인증·연결 상태 확인
/config           # 설정 변경 (diff 도구, 모델 등)
/init             # 프로젝트에 CLAUDE.md 자동 생성
/add-dir <경로>   # 작업 컨텍스트에 디렉토리 추가
/compact          # 대화 히스토리 압축
/clear            # 컨텍스트 초기화
/login  /logout   # 인증 전환
/usage            # 플랜 사용량 확인
```

---

## 💪 강력한 IDE 연동 기능

### 1. 인라인 Diff 검토

Claude가 파일을 수정하면 IDE의 네이티브 diff 뷰어로 좌우 비교를 볼 수 있고, **Hunk 단위로 수락/거부**가 가능합니다.

### 2. @-멘션으로 파일 참조

```
@src/utils/helpers.js         # 파일 전체
@src/utils/helpers.js#L10-50  # 특정 라인 범위
@terminal:build               # 터미널 출력 참조
```

### 3. 선택 영역 자동 컨텍스트

코드를 드래그로 선택한 뒤 `Cmd+Esc` / `Ctrl+Esc`를 누르면, 선택 영역이 자동으로 Claude의 컨텍스트에 포함됩니다.

### 4. Plan 모드

복잡한 작업은 Plan 모드로:

```bash
# Claude Code 실행 후 권한 모드 전환
# 프롬프트 박스 하단의 모드 인디케이터 클릭 → Plan 모드 선택
```

- Claude가 **마크다운 계획서** 작성
- 사용자가 **인라인 코멘트로 피드백** 가능
- 승인 후에만 실제 코드 수정

> 🎓 **강의 시연용으로 최고**: 학습자가 AI의 사고 과정을 단계별로 볼 수 있습니다.

### 5. 진단 정보 자동 공유

ESLint 경고, TypeScript 에러, Linter 메시지 등이 **자동으로** Claude에게 공유됩니다. 별도로 복사·붙여넣기할 필요 없음.

---

## 🪟 Windows WSL 사용자 추가 설정

WSL(Windows Subsystem for Linux)을 통해 Claude Code를 사용하는 경우 추가 설정이 필요합니다.

### VS Code (WSL Extension 사용 시)

```bash
# WSL 안에서 Claude Code 설치
wsl -d Ubuntu
npm install -g @anthropic-ai/claude-code

# VS Code에서:
# 좌측 하단 [><] 버튼 → "Connect to WSL" 선택
# WSL 환경에서 VS Code가 다시 열리면 Claude Code 확장도 WSL에 자동 설치됨
```

### JetBrains

`Settings → Tools → Claude Code → Claude command` 에 다음 입력:

```bash
wsl -d Ubuntu -- bash -lic "claude"
```

> 💡 `Ubuntu` 부분은 본인 WSL 배포판 이름으로 교체. 확인 명령어:
> ```powershell
> wsl --list
> ```

> 🔑 **`-lic` 플래그가 핵심**: bash가 프로필을 로드해 PATH·Node.js 설정을 인식합니다. 빠뜨리면 CLI를 찾지 못합니다.

---

## 🆘 자주 발생하는 문제

### Q1. VS Code에서 확장은 설치됐는데 패널이 안 보여요

```bash
# 명령 팔레트(Cmd+Shift+P)에서 실행
> Developer: Reload Window
```

다중 프로필 사용 시 → 현재 프로필에 확장이 설치됐는지 확인

### Q2. JetBrains에서 통합 터미널의 ESC 키가 작동 안 해요

`Settings → Tools → Terminal → Override IDE shortcuts` 항목을 조정하거나, Claude Code에서 `Ctrl+C`로 인터럽트 사용.

### Q3. `/ide` 명령어가 IDE에 연결 안 돼요

```bash
# 1. Claude Code 최신 버전 확인
claude --version
npm update -g @anthropic-ai/claude-code

# 2. IDE 완전 재시작 (캐시 무효화)
# JetBrains: File → Invalidate Caches → Invalidate and Restart
# VS Code: Developer: Reload Window

# 3. 프로젝트 루트에서 실행하는지 확인 (서브폴더 X)
```

### Q4. JetBrains 플러그인이 CLI를 못 찾아요

Node 버전 관리자(`nvm`, `mise`, `asdf`) 사용 시 IDE가 셸 PATH를 상속받지 못해서 발생합니다.

```bash
# 절대경로 확인 후 플러그인 설정에 입력
which claude

# 또는 PATH가 적용된 터미널에서 IDE 실행
# Mac: open -a "IntelliJ IDEA"
# Linux: idea ~/myproject
```

### Q5. JetBrains AI Assistant의 Claude Agent와 뭐가 달라요?

- **JetBrains AI Assistant의 Claude Agent**: JetBrains AI 구독 포함, IDE 채팅으로만 사용
- **Claude Code Plugin (Beta)**: Anthropic CLI 연동, 터미널·전체 프로젝트·자동화 가능

→ **둘 다 설치해서 상황에 맞게** 사용하는 것을 추천합니다.

### Q6. 인증은 됐는데 첫 응답이 너무 느려요

```bash
# Claude Code 진단 도구 실행
claude doctor
```

네트워크·프록시·인증 상태를 한 번에 점검합니다.

---

## 📚 공식 문서

- [Claude Code IDE 연동 (전체)](https://docs.claude.com/en/docs/claude-code/overview)
- [VS Code 확장 공식 문서](https://code.claude.com/docs/en/vs-code)
- [JetBrains 플러그인 공식 문서](https://code.claude.com/docs/en/jetbrains)
- [JetBrains Marketplace - Claude Code [Beta]](https://plugins.jetbrains.com/plugin/27310-claude-code-beta-)
- [Claude Code 인증 가이드](https://code.claude.com/docs/en/authentication)

---

## 🎓 강의 실습용 환경 체크리스트

학습자에게 배포하기 전, 다음 항목을 확인하세요.

- [ ] Node.js 18+ 설치
- [ ] `npm install -g @anthropic-ai/claude-code` 완료
- [ ] `claude --version` 정상 출력
- [ ] Anthropic 계정 로그인 (`/login`) 또는 API 키 설정
- [ ] 사용 IDE에 Claude Code 확장/플러그인 설치
- [ ] IDE 통합 터미널에서 `claude` 실행 시 IDE 자동 인식
- [ ] 테스트 프롬프트 1회 실행 (예: "이 프로젝트의 폴더 구조를 설명해줘")
- [ ] Plan 모드 동작 확인 (강의용)

---

📅 작성일: 2026.04.27  
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
