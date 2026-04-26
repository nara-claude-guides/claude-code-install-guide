# Claude Code API 키 설정 완벽 가이드 🔑

Claude Code 인증은 **두 가지 방식** 중 선택할 수 있습니다. 본인 상황에 맞는 방법을 고르세요.

---

## 📑 목차

- [어떤 방식을 선택해야 할까?](#-어떤-방식을-선택해야-할까)
- [사전 준비](#-사전-준비)
- [1. Anthropic Console에서 API 키 발급받기](#1️⃣-anthropic-console에서-api-키-발급받기)
- [2. 환경변수로 API 키 설정하기](#2️⃣-환경변수로-api-키-설정하기)
- [3. Claude Code 실행 & 인증 확인](#3️⃣-claude-code-실행--인증-확인)
- [4. 인증 방식 변경하고 싶을 때](#4️⃣-인증-방식-변경하고-싶을-때)
- [🔒 보안 베스트 프랙티스](#-보안-베스트-프랙티스)
- [💸 비용 관리 팁](#-비용-관리-팁)
- [🆘 자주 발생하는 문제](#-자주-발생하는-문제)
- [📚 공식 문서](#-공식-문서)

---

## 🎯 어떤 방식을 선택해야 할까?

| 방식 | 추천 대상 | 비용 |
|------|-----------|------|
| **① 구독 로그인 (OAuth)** | Claude Pro / Max 구독자 | 구독료에 포함 (추가 비용 없음) |
| **② API 키 (ANTHROPIC_API_KEY)** | 종량제로 쓰고 싶은 사용자, CI/CD, 자동화 스크립트 | 사용한 토큰만큼 과금 |

> 💡 **강의 실습용으로는 ①번 구독 로그인이 가장 간편합니다.** 본 가이드는 API 키 방식(②)을 중심으로 안내합니다.

---

## 📋 사전 준비

- ✅ Claude Code 설치 완료 (`npm install -g @anthropic-ai/claude-code`)
- ✅ Anthropic Console 계정 ([console.anthropic.com](https://console.anthropic.com))
- ✅ 결제 카드 등록 + 최소 $5 크레딧 충전

---

## 1️⃣ Anthropic Console에서 API 키 발급받기

### Step 1. 콘솔 접속

👉 [https://console.anthropic.com](https://console.anthropic.com) 접속 후 로그인

### Step 2. API Keys 메뉴 이동

좌측 사이드바에서 **API Keys** 클릭

### Step 3. 새 키 생성

1. **`Create Key`** 버튼 클릭
2. 키 이름 입력 (예: `claude-code-personal`, `lecture-demo`)
3. **`Create Key`** 클릭
4. **`sk-ant-api03-...`** 형식의 키가 표시됨

> ⚠️ **이 키는 단 한 번만 표시됩니다!** 반드시 안전한 곳(비밀번호 관리자 등)에 복사해두세요.

---

## 2️⃣ 환경변수로 API 키 설정하기

### 🍎 macOS (zsh, 기본 셸)

```bash
# 1. zshrc 파일에 환경변수 추가
echo 'export ANTHROPIC_API_KEY="sk-ant-api03-여기에_본인키_입력"' >> ~/.zshrc

# 2. 변경사항 적용
source ~/.zshrc

# 3. 정상 등록 확인
echo $ANTHROPIC_API_KEY
```

### 🐧 Linux / macOS (bash)

```bash
# 1. bashrc 파일에 환경변수 추가
echo 'export ANTHROPIC_API_KEY="sk-ant-api03-여기에_본인키_입력"' >> ~/.bashrc

# 2. 변경사항 적용
source ~/.bashrc

# 3. 정상 등록 확인
echo $ANTHROPIC_API_KEY
```

### 🪟 Windows (PowerShell)

**임시 설정 (현재 세션만)**

```powershell
$env:ANTHROPIC_API_KEY = "sk-ant-api03-여기에_본인키_입력"
```

**영구 설정 (사용자 환경변수)**

```powershell
[System.Environment]::SetEnvironmentVariable('ANTHROPIC_API_KEY', 'sk-ant-api03-여기에_본인키_입력', 'User')
```

> 💡 영구 설정 후에는 **터미널을 완전히 닫았다가 다시 열어야** 적용됩니다.

### 🪟 Windows (CMD)

```cmd
setx ANTHROPIC_API_KEY "sk-ant-api03-여기에_본인키_입력"
```

---

## 3️⃣ Claude Code 실행 & 인증 확인

```bash
# Claude Code 실행
claude

# 현재 인증 상태 확인 (Claude Code 내부에서)
/status
```

✅ 정상이라면 `Authentication: API key (ANTHROPIC_API_KEY)` 와 같은 메시지가 표시됩니다.

> 첫 실행 시 **"이 API 키를 사용하시겠습니까?"** 라는 확인 프롬프트가 한 번 뜹니다. `Yes`를 선택하면 이후 자동으로 사용됩니다.

---

## 4️⃣ 인증 방식 변경하고 싶을 때

```bash
# Claude Code 실행 후
/login        # 구독 로그인으로 전환
/logout       # 로그아웃
/config       # API 키 사용 토글 변경
/status       # 현재 인증 상태 확인
```

> ⚠️ 구독자인데 환경변수에 API 키가 있으면 **API 키가 우선 적용**됩니다. 구독으로 사용하려면:
>
> ```bash
> unset ANTHROPIC_API_KEY
> ```

---

## 🔒 보안 베스트 프랙티스

### ✅ 해야 할 것

- 🔐 환경변수로만 관리하기
- 🔐 `.gitignore`에 `.env` 파일 추가
- 🔐 Console에서 **월별 사용량 한도(Spend limit)** 설정
- 🔐 강의/데모용 키는 별도로 발급 (`lecture-demo` 등)
- 🔐 사용 후 **즉시 비활성화** 또는 한도 낮추기

### ❌ 절대 하지 말 것

- 🚫 소스코드에 API 키 하드코딩
- 🚫 GitHub, GitLab 등에 키 업로드
- 🚫 채팅, 슬라이드, 화면공유에 노출
- 🚫 README나 문서에 평문으로 기재

### 🚨 키가 유출되었다면

1. Console → API Keys → 해당 키 **즉시 비활성화(Deactivate)**
2. 새 키 발급
3. 모든 환경에 새 키 반영

---

## 💸 비용 관리 팁

```bash
# 1. Console > Settings > Limits 에서 월 한도 설정
#    예: 강의용은 $20/월로 제한

# 2. Console > Usage 에서 일별 사용량 확인

# 3. 강의 직후 Console 에서 키 즉시 비활성화
```

> 📌 Claude **Max 플랜 구독자는 Claude Code를 추가 비용 없이** 사용할 수 있습니다. 강의 환경 구축 시 참고하세요.

---

## 🆘 자주 발생하는 문제

| 증상 | 해결 방법 |
|------|-----------|
| `ANTHROPIC_API_KEY` 인식 안 됨 | 터미널 **완전히 종료 후 재시작** |
| `401 Unauthorized` | 키 오타 확인, Console에서 활성 상태 확인 |
| 구독으로 쓰고 싶은데 API 키가 먹힘 | `unset ANTHROPIC_API_KEY` 실행 후 `/login` |
| `apiKeyHelper` 경고 (10초 이상 지연) | 자격증명 스크립트 최적화 필요 |

---

## 📚 공식 문서

- [Claude Code 인증 가이드](https://code.claude.com/docs/en/authentication)
- [환경변수 관리 (지원센터)](https://support.claude.com/en/articles/12304248-managing-api-key-environment-variables-in-claude-code)
- [Anthropic Console](https://console.anthropic.com)
- [Claude Code 문서](https://docs.claude.com/en/docs/claude-code/overview)

---

📅 작성일: 2026.04.27  
✍️ Claude Code 강의 실습용 환경 구축 가이드
