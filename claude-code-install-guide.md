# Claude 로그인 및 Claude Code 설치 가이드

> 본 가이드는 **터미널을 처음 사용하는 학습자**도 따라 할 수 있도록 절차순으로 구성되어 있습니다.
> 한 단계씩 ✅ 표시하면서 진행하세요.
> _기준일: 2026년 4월 / 자료 출처: Anthropic 공식 문서(code.claude.com)_

---

## 📌 학습 목표

- [ ] Claude 계정을 만들고 로그인할 수 있다.
- [ ] 자신의 OS에 맞게 Claude Code를 설치할 수 있다.
- [ ] 터미널에서 `claude` 명령으로 첫 세션을 실행할 수 있다.
- [ ] 설치 중 발생하는 일반적인 오류를 스스로 해결할 수 있다.

---

## 0단계 · 사전 준비물 체크리스트

### 0-1. 시스템 요구사항

| 항목 | 요구 사양 |
|------|-----------|
| **운영체제** | macOS 10.15 이상 / Windows 10·11 / Ubuntu 20.04+ / Debian 10+ |
| **메모리(RAM)** | 최소 4GB (8GB 이상 권장) |
| **셸(Shell)** | Bash, Zsh, PowerShell, CMD 중 하나 |
| **인터넷** | OAuth 로그인 및 모델 호출에 필요 |
| **Windows 추가 요건** | **Git for Windows** 또는 **WSL** 중 택1 |

### 0-2. 결제 플랜 확인 — ⚠️ 매우 중요

**무료 Claude.ai 플랜으로는 Claude Code를 사용할 수 없습니다.** 아래 중 하나가 필요합니다.

| 플랜 | 월 요금(개인) | 비고 |
|------|--------------|------|
| **Claude Pro** | $20 | 개인 학습/소규모 프로젝트 |
| **Claude Max** | $100 ~ $200 | 헤비 사용자, Opus 우선 사용 |
| **Claude Team** | 시트당 $25 | 5인 이상 팀 |
| **Claude Console (API 키)** | 사용량 과금 | 자동화·CI/CD용 |

> 💡 **강의 실습용 추천**: Pro($20) 플랜 한 달 결제 → 학습 후 필요 시 해지

---

## 1단계 · Claude 계정 가입 및 로그인

### 1-1. 계정 가입

1. 웹 브라우저에서 **`https://claude.ai`** 접속
2. 우측 상단 **`Sign up`** 클릭
3. 다음 중 **하나의 방법**으로 가입
   - Google 계정 연동(가장 빠름)
   - Apple 계정 연동
   - 이메일 + 비밀번호 직접 입력
4. 이메일 인증 메일 확인 후 인증 링크 클릭
5. 휴대폰 번호 인증(국가 코드 +82, 국제 형식)

### 1-2. Pro 플랜 결제

1. 로그인 후 좌측 하단 **프로필 아이콘** 클릭
2. **`Settings`** → **`Plans & Billing`** 이동
3. **`Upgrade to Pro`** 버튼 클릭
4. 신용카드 정보 입력 후 결제 완료
5. 우측 상단 모델 선택기에 **`Claude Opus 4.7`** 또는 **`Sonnet 4.6`** 이 보이면 정상

> ✅ 체크포인트: 이 단계까지 마치면 웹 브라우저에서 Claude.ai를 자유롭게 쓸 수 있는 상태입니다.

---

## 2단계 · 운영체제별 Claude Code 설치

> 자신의 OS 섹션만 따라가면 됩니다. 잘못된 OS 명령을 실행하지 않도록 주의하세요.

### 🍎 2-A. macOS

#### 옵션 1: 네이티브 설치 (권장)

1. **Spotlight(`⌘ + Space`)** 에서 `터미널` 입력 → 실행
2. 아래 명령을 복사해서 붙여넣고 **Enter**

   ```bash
   curl -fsSL https://claude.ai/install.sh | bash
   ```

3. 설치 진행률이 표시되며 약 1~2분 소요
4. 설치 완료 후 **터미널 창을 닫았다가 다시 열기**(PATH 갱신용)

#### 옵션 2: Homebrew 사용

> Homebrew가 이미 설치되어 있는 경우만 해당

```bash
brew install claude-code
```

업데이트가 필요할 때:

```bash
brew upgrade claude-code
```

---

### 🪟 2-B. Windows

> ⚠️ **사전 작업**: [https://git-scm.com/download/win](https://git-scm.com/download/win) 에서 **Git for Windows**를 먼저 설치하세요.

#### 옵션 1: PowerShell 네이티브 설치 (권장)

1. **시작 버튼 우클릭** → **`Windows PowerShell`** 또는 **`터미널`** 선택
2. 다음 명령을 붙여넣고 **Enter**

   ```powershell
   irm https://claude.ai/install.ps1 | iex
   ```

3. 설치 완료 후 **PowerShell 창을 완전히 닫고 새로 열기**

#### 옵션 2: WinGet 사용 (Windows 10/11 기본 패키지 매니저)

```powershell
winget install Anthropic.ClaudeCode
```

업데이트가 필요할 때:

```powershell
winget upgrade Anthropic.ClaudeCode
```

> 💡 **PowerShell vs CMD 구분법**
> 프롬프트가 `PS C:\Users\...>` → PowerShell
> 프롬프트가 `C:\Users\...>` → CMD

---

### 🐧 2-C. Linux (Ubuntu / Debian / Fedora / Arch)

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

배포판별 패키지 매니저로도 설치 가능합니다.

| 배포판 | 명령 |
|--------|------|
| **Debian / Ubuntu** | `sudo apt install claude-code` |
| **Fedora / RHEL** | `sudo dnf install claude-code` |
| **Alpine** | `sudo apk add claude-code` |

> ⚠️ Alpine 등 musl 기반 배포판은 추가로 `libgcc`, `libstdc++`, `ripgrep`을 설치하고 환경 변수 `USE_BUILTIN_RIPGREP=0`을 설정해야 합니다.

---

### 🐧🪟 2-D. Windows 사용자 중 WSL 환경 선호 시

1. PowerShell에서 WSL 설치
   ```powershell
   wsl --install
   ```
2. 재부팅 후 Ubuntu 터미널 실행
3. WSL 터미널 안에서 Linux 설치 명령 실행
   ```bash
   curl -fsSL https://claude.ai/install.sh | bash
   ```

---

## 3단계 · 설치 확인

운영체제와 무관하게 **새 터미널 창**을 열고 다음을 실행하세요.

```bash
claude --version
```

✅ 정상 출력 예시:

```
claude-code 2.1.x
```

❌ `command not found` 또는 `명령을 인식할 수 없습니다` 오류 → **6단계 트러블슈팅**으로 이동

---

## 4단계 · 첫 실행 및 인증 (로그인)

### 4-1. 작업 폴더 만들기

```bash
mkdir my-first-claude-project
cd my-first-claude-project
```

### 4-2. Claude Code 실행

```bash
claude
```

### 4-3. 브라우저 로그인 흐름

1. 터미널에 **`Press Enter to authenticate in browser`** 메시지가 뜸
2. **Enter** 키를 누르면 기본 웹 브라우저가 자동으로 열림
3. **1단계에서 만든 Claude 계정**으로 로그인
4. 권한 요청 페이지에서 **`Authorize`** 클릭
5. **"You can now close this browser tab"** 메시지 확인
6. 터미널로 돌아오면 인증 완료, Claude Code 프롬프트(`>`)가 뜸

> 💡 **CI/CD 환경 등 브라우저가 없는 경우**: Anthropic Console에서 API 키를 발급받아 환경 변수로 설정합니다.
> ```bash
> export ANTHROPIC_API_KEY="sk-ant-..."
> ```

---

## 5단계 · 동작 확인 — 첫 명령 실행하기

Claude Code 프롬프트가 뜨면 자연어로 명령을 입력해 봅니다.

### 5-1. 인사 테스트

```
> Hello, Claude. 현재 폴더에 어떤 파일이 있는지 알려줘.
```

### 5-2. 간단한 파일 만들기

```
> README.md 파일을 만들고 "내 첫 Claude Code 프로젝트"라고 적어줘.
```

→ Claude Code가 변경 사항을 보여주고 **`Do you want to make this edit? (y/n)`** 확인을 요청합니다.
→ `y` 입력 → 파일 생성 완료

### 5-3. 종료하기

```
> /exit
```

또는 `Ctrl + C` 두 번

> ✅ 여기까지 성공하면 **설치와 로그인이 모두 정상**입니다.

---

## 6단계 · 트러블슈팅 (자주 발생하는 오류)

### 6-1. `claude: command not found`

| 원인 | 해결 방법 |
|------|----------|
| **PATH 미반영** | 터미널을 완전히 닫고 새로 열기 |
| **macOS Zsh** | `source ~/.zshrc` 실행 |
| **Linux Bash** | `source ~/.bashrc` 실행 |
| **Windows** | 시스템 환경 변수 → PATH에 `%USERPROFILE%\.local\bin` 추가 |

### 6-2. Windows 네이티브 설치 시 진행 표시가 멈춤

→ **WinGet으로 재시도**

```powershell
winget install Anthropic.ClaudeCode
```

### 6-3. 401 Unauthorized 또는 로그인 루프

```bash
claude logout
claude
```

→ 다시 브라우저 인증 시도

### 6-4. 진단 도구로 자동 점검

```bash
claude doctor
```

→ 시스템 설정, 인증 상태, 감지된 문제를 한 번에 보고합니다.

### 6-5. ⚠️ 보안 경고 — 가짜 설치 페이지 주의

2026년 들어 검색 광고를 통해 **가짜 Claude Code 설치 페이지**가 유포된 사례가 보고되었습니다.
**반드시 공식 도메인 두 곳만** 사용하세요.

- ✅ `https://claude.ai/install.sh`
- ✅ `https://claude.ai/install.ps1`
- ❌ 검색 광고 상단의 의심스러운 도메인은 클릭 금지

---

## 7단계 · (선택) VS Code 확장 설치

터미널이 익숙하지 않다면 VS Code 확장으로도 동일한 기능을 쓸 수 있습니다.

1. VS Code 실행
2. `Cmd + Shift + X` (Mac) 또는 `Ctrl + Shift + X` (Windows/Linux)로 확장 패널 열기
3. 검색창에 **`Claude Code`** 입력
4. **Anthropic 공식 배포본**의 **`Install`** 클릭
5. 설치 후 좌측 사이드바의 ✱ 스파크 아이콘 클릭
6. 동일한 OAuth 로그인 절차 진행

> 💡 확장과 CLI는 설정을 공유합니다. 설정 파일 경로는 모든 OS에서 `~/.claude/settings.json` 입니다.

---

## 8단계 · 다음 학습 단계

| 주제 | 학습 키워드 |
|------|------------|
| 프로젝트 컨텍스트 기억시키기 | `CLAUDE.md` 파일 작성법 |
| 권한 제어 | `/permissions` 명령 |
| 외부 도구 연결 | MCP (Model Context Protocol) |
| 자동화 워크플로 | Hooks, Sub-agents |
| 비용 관리 | `/cost` 명령, 모델 티어 선택 |

---

## 📋 최종 체크리스트

수강생이 모든 항목에 체크할 수 있어야 실습 완료입니다.

- [ ] Claude.ai 계정을 만들고 Pro 이상 플랜을 결제했다.
- [ ] 내 OS에 맞는 방법으로 Claude Code를 설치했다.
- [ ] `claude --version`이 정상적으로 버전을 출력한다.
- [ ] 새 폴더에서 `claude` 명령으로 첫 세션을 시작했다.
- [ ] 브라우저 OAuth로 로그인을 완료했다.
- [ ] Claude에게 자연어로 첫 명령을 내려 응답을 받았다.
- [ ] `/exit`로 정상 종료할 수 있다.

---

## 📚 공식 참고 자료

- Claude Code 공식 문서: <https://code.claude.com/docs>
- 설치 가이드(영문): <https://code.claude.com/docs/en/setup>
- 설치 가이드(한글): <https://code.claude.com/docs/ko/setup>
- 인증 방법: <https://code.claude.com/docs/en/authentication>
- 트러블슈팅: <https://code.claude.com/docs/en/troubleshooting>

---

> _본 자료는 강의·실습용으로 자유롭게 배포 및 수정 가능합니다.
> 단, Anthropic 공식 정책 및 가격은 수시로 변동되므로 결제 직전 공식 페이지에서 재확인하시기 바랍니다._
