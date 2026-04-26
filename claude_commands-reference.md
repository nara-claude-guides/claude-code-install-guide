# Claude Code 명령어 정리 ⌨️

Claude Code 명령어를 한눈에 보기 좋게 정리한 레퍼런스입니다.

---

## 📑 목차

- [명령어 종류](#-명령어-종류)
- [1. 터미널 명령 (Shell에서 실행)](#1️⃣-터미널-명령-shell에서-실행)
- [2. CLI 플래그 (실행 시 옵션)](#2️⃣-cli-플래그-실행-시-옵션)
- [3. 슬래시 명령 (세션 내부)](#3️⃣-슬래시-명령-세션-내부)
- [🎯 입력창 특수 기호](#-입력창-특수-기호-세션-내부)
- [⌨️ 키보드 단축키](#️-키보드-단축키-세션-내부)
- [💡 자주 쓰는 조합 패턴](#-자주-쓰는-조합-패턴)
- [🌍 환경 변수](#-환경-변수-자주-쓰는-것)
- [📚 공식 문서](#-공식-문서)

---

## 🎯 명령어 종류

| 종류 | 사용 위치 | 예시 |
|------|-----------|------|
| **① 터미널 명령** | 셸에서 직접 실행 | `claude --version` |
| **② CLI 플래그** | `claude` 실행 시 옵션 | `claude --model opus` |
| **③ 슬래시 명령** | 세션 내부에서 입력 | `/help`, `/init` |

---

## 1️⃣ 터미널 명령 (Shell에서 실행)

### 🚀 실행 & 세션 관리

```bash
claude                            # 새 대화형 세션 시작
claude "질문 내용"                # 즉석 질문 (대화형 모드)
claude -c                         # 마지막 세션 이어가기 (continue)
claude --resume                   # 세션 선택해서 재개 (인터랙티브 피커)
claude --resume <session-id>      # 특정 세션 ID로 재개
```

### 📋 정보 확인 & 진단

```bash
claude --version                  # 버전 확인
claude -v                         # 위와 동일 (단축형)
claude --help                     # 도움말 (전체 플래그는 일부만 표시됨)
claude doctor                     # 설치·인증·환경 진단
```

### 🔐 인증 관리

```bash
claude auth login                 # 로그인 / 계정 전환
claude auth status                # 현재 인증 상태
claude auth logout                # 자격증명 삭제
claude setup-token                # CI/CD용 장기 OAuth 토큰 발급
```

### 📦 설치·업데이트

```bash
# 설치 (3가지 방법)
curl -fsSL https://claude.ai/install.sh | bash    # 네이티브 바이너리 (권장)
brew install --cask claude-code                   # macOS Homebrew
npm install -g @anthropic-ai/claude-code          # npm

# 업데이트
npm update -g @anthropic-ai/claude-code
claude install                                    # npm → 네이티브 마이그레이션
```

### 🔌 MCP 서버 관리

```bash
claude mcp add <name> <command>   # MCP 서버 추가
claude mcp list                   # 등록된 MCP 서버 목록
claude mcp remove <name>          # MCP 서버 제거
```

---

## 2️⃣ CLI 플래그 (실행 시 옵션)

### 🤖 모델 선택

```bash
claude --model opus               # Opus 모델로 시작
claude --model sonnet             # Sonnet 모델
claude --model haiku              # Haiku 모델 (빠름, 저렴)
claude --model claude-opus-4-7    # 모델 ID 직접 지정
```

### 🔓 권한 모드

```bash
claude --permission-mode plan          # Plan 모드 (계획 후 승인)
claude --permission-mode acceptEdits   # 편집 자동 수락
claude --permission-mode auto          # 완전 자동 모드 ⚠️
claude --permission-mode default       # 매 작업마다 확인 (기본값)
```

### 📤 출력 & 비대화 모드

```bash
claude -p "한 줄 질문"            # 1회 응답 후 종료 (print 모드)
claude --print "질문"             # -p 와 동일
claude -p --output-format json "질문"        # JSON 출력 (스크립트용)
claude -p --output-format stream-json "질문" # 스트리밍 JSON
```

### 🧠 시스템 프롬프트

```bash
claude --system-prompt "TypeScript 전문가야"           # 기본 프롬프트 교체
claude --system-prompt-file ./prompt.txt              # 파일에서 로드 (교체)
claude --append-system-prompt "한국어로 답변"          # 기본 프롬프트에 추가 (권장)
claude --append-system-prompt-file ./extra.txt        # 파일 추가
```

> 💡 **`--append-` 권장**: 기본 기능을 유지하면서 커스터마이징 가능

### 🌳 Git Worktree

```bash
claude --worktree feature-auth    # 격리된 git worktree에서 시작
claude -w feature-auth            # 단축형
```

### 🐛 디버깅

```bash
claude --debug                    # 디버그 정보 켜기
claude -d "api,hooks"             # 특정 카테고리만 디버그
claude --verbose                  # 상세 로깅
```

### 🔧 기타

```bash
claude --max-turns 5              # 최대 턴 수 제한
claude --max-budget-usd 5         # 비용 한도 (USD)
claude --add-dir ~/another-proj   # 추가 디렉토리 컨텍스트 포함
```

---

## 3️⃣ 슬래시 명령 (세션 내부)

### 📚 도움말 & 정보

```
/help                  # 모든 슬래시 명령어 목록
/status                # 인증·연결·모델 상태
/usage                 # 플랜 사용량 확인
/cost                  # 현재 토큰·비용 확인
/doctor                # 환경 진단
```

### 🗂️ 세션 & 컨텍스트 관리

```
/clear                 # 대화 히스토리 완전 초기화
/compact               # 히스토리 압축 (요약하여 컨텍스트 확보)
/compact <지시>        # 압축 시 보존할 내용 지정
/rewind                # 이전 시점으로 롤백 (Esc 두 번도 가능)
/checkpoint            # /rewind 와 동일
/exit                  # 세션 종료 (Ctrl+D 도 가능)
```

### 📁 프로젝트 관리

```
/init                  # CLAUDE.md 자동 생성 (프로젝트 컨텍스트)
/add-dir <경로>        # 추가 디렉토리를 컨텍스트에 포함
```

### ⚙️ 설정 & 모드 변경

```
/config                # 런타임 설정 변경 (diff 도구 등)
/model                 # 모델 변경 (목록 표시 후 선택)
/permissions           # 권한 모드 변경
/plan                  # Plan 모드 토글 (Shift+Tab 도 가능)
/effort high           # 다음 응답에 높은 추론 노력 적용
/keybindings           # 단축키 커스터마이징
```

### 🔐 인증

```
/login                 # 로그인 / 계정 전환
/logout                # 로그아웃
```

### 🔌 IDE & 통합

```
/ide                   # 외부 터미널 → 현재 IDE에 연결
/mcp                   # MCP 서버 관리
/agents                # 서브에이전트 설정
```

### 🤖 고급 기능 (2026 추가)

```
/simplify              # PR 전 품질 검증 (3-에이전트 리뷰)
/batch                 # 여러 worktree에서 병렬 작업 + PR 자동 생성
/remote-control        # 원격 제어 세션 시작
```

---

## 🎯 입력창 특수 기호 (세션 내부)

### `@` — 파일·터미널 참조

```
@src/utils/helpers.js                # 파일 전체 첨부
@src/utils/helpers.js#L10-50         # 특정 라인 범위
@./README.md                         # 상대경로
@terminal:build                      # 터미널 출력 참조 (이름)
```

### `!` — 셸 명령 직접 실행

```
!npm test                            # 테스트 실행 후 결과를 컨텍스트에 추가
!ls -la                              # 파일 목록 보기
!git status                          # git 상태 확인
```

### `/` — 슬래시 명령 자동완성

프롬프트 시작에 `/` 입력 시 사용 가능한 명령어 메뉴 표시

---

## ⌨️ 키보드 단축키 (세션 내부)

| 키 | 기능 |
|-----|------|
| `Ctrl+C` | 현재 응답 인터럽트 (세션은 유지) |
| `Ctrl+D` | 세션 완전 종료 |
| `Esc` | 입력 취소 / 진행 중 작업 중지 |
| `Esc` (두 번) | `/rewind` 메뉴 (롤백) |
| `Shift+Tab` | Plan 모드 토글 |
| `Option+Enter` (Mac) | 여러 줄 입력 (개행) |
| `↑` / `↓` | 이전 프롬프트 히스토리 |

---

## 💡 자주 쓰는 조합 패턴

```bash
# 코드 리뷰 자동화
git diff | claude -p "이 변경사항 리뷰해줘"

# 에러 메시지 빠른 분석
npm test 2>&1 | claude -p "이 에러 원인 알려줘"

# README 자동 업데이트
claude -p "package.json 보고 README의 설치 섹션 업데이트해줘"

# 강의용: Plan 모드로 안전하게 시작
claude --permission-mode plan --model sonnet

# CI 환경에서 JSON 출력
claude -p --output-format json "테스트 커버리지 분석" > result.json

# 격리된 환경에서 실험
claude --worktree experiment-refactor

# 한국어 응답 강제 + 한국어 코멘트
claude --append-system-prompt "모든 응답과 코드 주석은 한국어로 작성"
```

---

## 🌍 환경 변수 (자주 쓰는 것)

```bash
ANTHROPIC_API_KEY              # API 키 (직접 인증)
ANTHROPIC_AUTH_TOKEN           # 게이트웨이용 Bearer 토큰
ANTHROPIC_BASE_URL             # API 엔드포인트 변경 (프록시·게이트웨이용)
CLAUDE_CODE_OAUTH_TOKEN        # CI용 장기 OAuth 토큰
CLAUDE_CODE_MODEL              # 기본 모델 지정
CLAUDE_CODE_USE_BEDROCK        # AWS Bedrock 라우팅
CLAUDE_CODE_USE_VERTEX         # Google Vertex AI 라우팅
HTTPS_PROXY / HTTP_PROXY       # 기업 프록시 환경
NODE_EXTRA_CA_CERTS            # 사내 CA 인증서
```

---

## 🎓 강의 실습용 핵심 명령어 TOP 10

학습자가 가장 먼저 익혀야 할 10개:

| 순위 | 명령어 | 용도 |
|------|--------|------|
| 1 | `claude` | 세션 시작 |
| 2 | `claude --version` | 설치 확인 |
| 3 | `claude doctor` | 환경 진단 |
| 4 | `/help` | 도움말 |
| 5 | `/init` | 프로젝트 컨텍스트 자동 생성 |
| 6 | `/clear` | 대화 초기화 |
| 7 | `/compact` | 컨텍스트 정리 |
| 8 | `@파일경로` | 파일 첨부 |
| 9 | `Shift+Tab` | Plan 모드 토글 |
| 10 | `Esc Esc` | 롤백 메뉴 |

---

## 📚 공식 문서

- [CLI Reference (전체 플래그)](https://code.claude.com/docs/en/cli-reference)
- [Slash Commands](https://docs.claude.com/en/docs/claude-code/overview)
- [Commands Overview](https://code.claude.com/docs/en/commands)
- [Claude Code 설치](https://code.claude.com/docs/en/setup)

---

> 💡 세션 안에서 **`/help`** 만 기억하셔도 됩니다. 현재 세션에서 사용 가능한 모든 명령어(커스텀·플러그인·MCP 포함)를 보여줍니다.

---

📅 작성일: 2026.04.27  
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
