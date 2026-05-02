# Claude Code를 활용한 데이터 분석 - Spotify 🎵📊

> Claude Code와 함께 **진짜 데이터**를 만져봐요.
> "코드 한 줄 안 쓰고 분석부터 시각화까지" — Vibe Coding의 세계로!

---

## 🎯 학습 목표

이 실습을 마치면 다음을 할 수 있어요:

- ✅ **Vibe Coding** 감각 익히기 (AI와 흐름 타며 작업)
- ✅ Claude Code로 **데이터 탐색·전처리** 수행
- ✅ **시각화 코드를 점진적으로 개선** 하기
- ✅ 데이터에서 **인사이트 도출 + 해석**
- ✅ Pandas, Matplotlib, Seaborn 실전 흐름 체득

---

## 📑 목차

- [시작하기 전에](#-시작하기-전에)
- [🎵 Vibe Coding이란?](#-vibe-coding이란)
- [1. 실습 주제 소개: Spotify 데이터 분석](#1️⃣-실습-주제-소개-spotify-데이터-분석)
- [2. 데이터 탐색 및 전처리](#2️⃣-데이터-탐색-및-전처리-claude-code-활용)
- [3. 시각화 코드 생성 및 개선](#3️⃣-시각화-코드-생성-및-개선)
- [4. 분석 결과 도출 및 해석](#4️⃣-분석-결과-도출-및-해석)
- [🪞 5분 회고](#-5분-회고)
- [🆘 자주 막히는 지점](#-자주-막히는-지점)
- [🎓 다음 단계](#-다음-단계)

---

## 📋 시작하기 전에

- ✅ Claude Code 설치 완료 → [설치 가이드](./claude-code-install-guide.md)
- ✅ Python 3.10+ 설치 (`python --version` 또는 `python3 --version`)
- ✅ [Python 계산기 실습](./python-calculator-tutorial.md) 완료 권장
- ✅ [프롬프트 작성법 실습](./effective-prompting-and-claude-md.md) 완료 권장
- ✅ 마음의 준비: **"오타가 나도, 차트가 못나도 괜찮아"** 🌱

> ⏱ **소요 시간**: 약 90~120분
> 🎯 **권장 모드**: Plan 모드 (사고 과정 관찰용)

### 작업 폴더 준비

```bash
mkdir spotify-analysis
cd spotify-analysis
claude
```

---

## 🎵 Vibe Coding이란?

> "Coding by vibes" — **느낌으로 코딩하기**

### 🤔 무슨 뜻이에요?

전통 코딩과 Vibe Coding을 비교해볼게요:

| 항목 | 전통 코딩 | Vibe Coding |
|------|----------|-------------|
| 시작점 | 정확한 명세서 | "이런 느낌이면 좋겠어" |
| 진행 방식 | 한 줄 한 줄 직접 작성 | 자연어로 의도 전달 |
| 디버깅 | 스택 트레이스 분석 | "이 에러 고쳐줘" |
| 최종 결과 | 의도한 그대로 | **반복하며 다듬어가는 결과** |

### 🌊 핵심 마인드셋

```
1. 완벽하게 시작하지 않는다 → 일단 흐름을 탄다
2. 모든 라인을 이해할 필요 없다 → 의도와 결과만 챙긴다
3. AI가 더 잘 아는 영역은 위임한다 → 내 시간은 판단에 쓴다
4. 막히면 보여주고 물어본다 → 혼자 헤매지 않는다
```

### ⚠️ 오해 풀기

> ❌ "코드를 전혀 모르고도 돼요" — **틀려요!**
> ✅ "코드를 직접 안 짜도, 읽고 평가할 수는 있어야 해요"

Vibe Coding은 **운전과 비슷해요**. 차의 모든 부품을 만들 줄 몰라도 운전은 할 수 있죠. 다만 **신호등은 읽을 줄 알아야** 해요.

---

## 1️⃣ 실습 주제 소개: Spotify 데이터 분석

### 🎶 왜 Spotify 데이터?

| 이유 | 설명 |
|------|------|
| 🎧 **친숙함** | 모두가 음악은 들어요 |
| 📊 **숫자 + 카테고리 혼재** | 다양한 분석 기법 연습 |
| 🤔 **직관적 가설 생성** | "신나는 노래는 인기가 많을까?" |
| 📈 **시각화 효과 좋음** | 결과가 한눈에 들어옴 |

### 📦 사용할 데이터셋

**Kaggle의 Spotify Tracks Dataset** (또는 유사 데이터셋)을 권장해요.

> 💡 **데이터 받는 법**:
> 1. [kaggle.com](https://kaggle.com) 접속
> 2. 검색창에 "spotify tracks dataset" 검색
> 3. 인기 데이터셋 다운로드 → `tracks.csv` (또는 비슷한 이름)
> 4. 작업 폴더로 이동

### 🗂️ 일반적인 컬럼 구조

| 컬럼 | 의미 | 범위/타입 |
|------|------|----------|
| `track_name` | 곡 제목 | 문자열 |
| `artist_name` | 아티스트 | 문자열 |
| `popularity` | 인기도 | 0~100 |
| `danceability` | 춤추기 좋은 정도 | 0.0~1.0 |
| `energy` | 에너지/강렬함 | 0.0~1.0 |
| `valence` | 긍정성(=행복도) | 0.0~1.0 |
| `tempo` | BPM | 50~200 정도 |
| `acousticness` | 어쿠스틱 정도 | 0.0~1.0 |
| `duration_ms` | 길이 (밀리초) | 정수 |
| `genre` | 장르 | 문자열 |

### 🎯 우리가 던질 질문들

```
1. 가장 인기 있는 장르는?
2. 신나는(높은 valence) 노래가 정말 인기가 많을까?
3. 에너지와 춤추기 좋은 정도는 상관관계가 있을까?
4. 노래 길이는 시대에 따라 어떻게 변했을까?
5. 우리 팀(또는 본인)이 좋아할 만한 곡 추천은?
```

> 🎓 **강의 팁**: 학습자가 **자기 가설**을 1개 더 추가하게 해보세요. 주인의식이 확 살아요!

### 🛠 사전 준비: 필요한 라이브러리

```
프로젝트 시작에 필요한 라이브러리를 알려줘. 
나는 pandas로 데이터 다루고, matplotlib과 seaborn으로 시각화할 예정이야.
설치 명령어도 같이.
```

→ Claude가 알아서:

```bash
pip install pandas matplotlib seaborn jupyter
```

> 💡 **가상환경 권장**: 큰 프로젝트라면 `python -m venv venv` 먼저 만들고 시작.

---

## 2️⃣ 데이터 탐색 및 전처리 (Claude Code 활용)

### 🎬 Step 1. 데이터 첫 만남

#### 💬 프롬프트

```
tracks.csv 파일을 읽어서 다음을 알려줘:
1. 행과 열의 개수
2. 각 컬럼의 데이터 타입
3. 첫 5행 미리보기
4. 결측치(null)가 있는 컬럼

이걸 explore_data.py 라는 파일로 만들어줘.
```

#### 🎁 Claude의 응답 예시

```python
# explore_data.py
import pandas as pd

df = pd.read_csv("tracks.csv")

print("=" * 50)
print(f"📦 데이터 크기: {df.shape[0]:,}행 × {df.shape[1]}열")
print("=" * 50)

print("\n📋 컬럼 정보:")
print(df.dtypes)

print("\n👀 미리보기:")
print(df.head())

print("\n❓ 결측치 현황:")
missing = df.isnull().sum()
print(missing[missing > 0] if missing.any() else "결측치 없음 ✅")
```

#### ▶ 실행

```
!python explore_data.py
```

### 👀 결과 읽는 법

| 출력 | 무엇을 보고 있나? |
|------|------------------|
| `📦 데이터 크기: 114,000행 × 21열` | 약 11만 곡, 21개 정보 |
| `dtypes` | 숫자/문자열 구분 — 숫자가 문자열로 잘못 들어왔나? |
| `head()` | 실제 값들이 상상과 일치? |
| 결측치 | 어떤 컬럼이 빈칸 많은지 |

### 🎬 Step 2. 데이터 정제

#### 💬 프롬프트

```
지금 데이터를 정제해줘:
1. 중복된 행 제거
2. duration_ms를 분(min) 단위 컬럼으로 추가
3. 결측치가 있는 행은 제거 (또는 적절히 채우기)
4. popularity가 0인 행은 제외

clean_data.py 라는 파일로 만들고, 정제된 데이터를 tracks_clean.csv로 저장해줘.
```

#### 🎁 Claude의 응답 예시

```python
# clean_data.py
import pandas as pd

df = pd.read_csv("tracks.csv")
print(f"정제 전: {len(df):,}행")

# 1. 중복 제거
df = df.drop_duplicates()

# 2. duration_min 컬럼 추가
df["duration_min"] = df["duration_ms"] / 60_000

# 3. 결측치 행 제거
df = df.dropna()

# 4. popularity 0 제외
df = df[df["popularity"] > 0]

print(f"정제 후: {len(df):,}행")
df.to_csv("tracks_clean.csv", index=False)
print("✅ tracks_clean.csv 저장 완료")
```

### 🤔 학습자에게 던질 질문

> "결측치는 무조건 삭제하는 게 맞을까요? 어떨 때 채우는 게 더 나을까요?"

#### 💬 추가 프롬프트로 깊게 들어가기

```
결측치 처리 방법 3가지를 비교해줘 (삭제 / 평균값 채우기 / 0 채우기). 
각각 어떤 상황에 적절한지 설명도.
```

→ Claude가 트레이드오프 표로 정리해줘요. **이게 진짜 학습!**

### 🎬 Step 3. 통계 요약

```
tracks_clean.csv의 숫자형 컬럼들에 대해 통계 요약을 보여줘.
특히 popularity, danceability, energy, valence를 자세히.
```

→ `df[cols].describe()` 와 함께 **해석도 같이** 요청하면 더 좋아요:

```
위 통계에서 눈에 띄는 패턴을 3가지만 짚어줘.
```

---

## 3️⃣ 시각화 코드 생성 및 개선

### 🎨 Vibe Coding의 정수: 점진적 개선

처음부터 완벽한 차트를 만들려 하지 마세요. **3단계로** 발전시켜요.

### 🎬 1차: "일단 그려봐"

#### 💬 프롬프트

```
tracks_clean.csv를 읽어서 popularity 분포를 히스토그램으로 그려줘.
plot_popularity.py 파일로 만들어줘.
```

#### 🎁 Claude의 1차 결과

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("tracks_clean.csv")
df["popularity"].hist(bins=50)
plt.show()
```

▶ 실행:

```
!python plot_popularity.py
```

→ **차트가 떴어요!** 근데... 좀 못생겼죠?

### 🎬 2차: "이쁘게 만들어"

#### 💬 프롬프트

```
방금 차트를 다음처럼 개선해줘:
- 제목 추가: "Spotify 곡 인기도 분포"
- x축 라벨: "Popularity (0-100)"
- y축 라벨: "곡 개수"
- 색상: 좀 더 매력적인 색
- 한국어 깨지지 않게 폰트 설정
- 그리드 추가
- 평균값을 빨간 점선으로 표시
```

#### 🎁 Claude의 2차 결과

```python
import pandas as pd
import matplotlib.pyplot as plt
import platform

# 한글 폰트 설정
if platform.system() == "Darwin":
    plt.rc("font", family="AppleGothic")
elif platform.system() == "Windows":
    plt.rc("font", family="Malgun Gothic")
plt.rcParams["axes.unicode_minus"] = False

df = pd.read_csv("tracks_clean.csv")

fig, ax = plt.subplots(figsize=(10, 6))
ax.hist(df["popularity"], bins=50, color="#1DB954", edgecolor="white", alpha=0.8)

mean_pop = df["popularity"].mean()
ax.axvline(mean_pop, color="red", linestyle="--", linewidth=2, label=f"평균: {mean_pop:.1f}")

ax.set_title("Spotify 곡 인기도 분포", fontsize=16, fontweight="bold")
ax.set_xlabel("Popularity (0-100)", fontsize=12)
ax.set_ylabel("곡 개수", fontsize=12)
ax.grid(True, alpha=0.3)
ax.legend()

plt.tight_layout()
plt.savefig("popularity_distribution.png", dpi=150)
plt.show()
```

> 🎵 색상 `#1DB954` 는 Spotify 공식 그린 컬러예요!

### 🎬 3차: "분석에 진짜 도움 되게"

#### 💬 프롬프트

```
이번엔 valence(긍정성)와 popularity의 관계를 보고 싶어.
산점도(scatter plot)로 그려주고:
- 점이 너무 많으니 투명도 조절
- 추세선 추가
- 상관계수도 차트에 표시
- "신나는 노래가 정말 인기가 많을까?" 라는 질문에 답할 수 있게
```

#### 🎁 Claude의 3차 결과

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

df = pd.read_csv("tracks_clean.csv")

# 상관계수 계산
corr, p_value = stats.pearsonr(df["valence"], df["popularity"])

fig, ax = plt.subplots(figsize=(10, 7))

sns.regplot(
    data=df.sample(5000, random_state=42),  # 5천 곡 샘플 (속도 + 가독성)
    x="valence",
    y="popularity",
    scatter_kws={"alpha": 0.3, "s": 15, "color": "#1DB954"},
    line_kws={"color": "red", "linewidth": 2},
    ax=ax,
)

ax.set_title(
    f"신나는 노래가 정말 인기가 많을까?\n상관계수 r = {corr:.3f} (p = {p_value:.3g})",
    fontsize=14,
)
ax.set_xlabel("Valence (긍정성, 0=슬픔 ~ 1=신남)")
ax.set_ylabel("Popularity (0-100)")
ax.grid(True, alpha=0.3)

plt.tight_layout()
plt.savefig("valence_vs_popularity.png", dpi=150)
plt.show()

print(f"\n📊 상관계수: {corr:.3f}")
if abs(corr) < 0.1:
    print("→ 거의 관계 없음 😮")
elif abs(corr) < 0.3:
    print("→ 약한 상관관계")
else:
    print("→ 뚜렷한 상관관계")
```

### 🎯 차트 개선 사이클의 본질

```
"일단 그려" (작동) 
    ↓
"이쁘게" (가독성)
    ↓
"질문에 답하게" (인사이트)
```

> 💎 **Vibe Coding 핵심**: **세 번 시도**하는 게 한 번 완벽보다 빠르고 좋아요.

### 🎨 더 만들어볼 시각화

학습자에게 직접 요청하게 해보세요:

```
1. 장르별 평균 popularity 막대그래프 (Top 10)
2. danceability vs energy 히트맵
3. 곡 길이 분포 (분 단위)
4. 연도별 평균 valence 추이 (있다면)
```

---

## 4️⃣ 분석 결과 도출 및 해석

### 🧠 데이터에서 "이야기"를 찾아내기

차트만 그리고 끝나면 **반쪽짜리** 분석이에요. **숫자를 말로 풀어내야** 진짜 분석!

### 🎬 분석 → 해석 → 액션 흐름

#### 💬 종합 분석 프롬프트

```
지금까지 만든 차트와 통계를 종합해서 다음 형식의 리포트를 만들어줘:

## 📊 핵심 발견
1. [발견 1] - 근거 데이터
2. [발견 2] - 근거 데이터
3. [발견 3] - 근거 데이터

## 🤔 해석
- 왜 이런 패턴이 나타날까?
- 우리 직관과 일치하는가?

## 💡 액션 아이템
- 이 인사이트로 무엇을 할 수 있을까?

리포트 파일로 저장해줘 (analysis_report.md).
```

### 🎁 예시 결과 (가상)

```markdown
## 📊 핵심 발견
1. **장르 다양성**: 분석한 11만 곡 중 상위 10개 장르가 전체의 42% 차지 → 롱테일 분포
2. **valence ↔ popularity 약한 상관**: r = 0.08 → "신나는 노래가 인기 많다"는 직관은 약하게만 성립
3. **에너지-춤 강한 상관**: r = 0.71 → 에너지 높은 곡은 거의 항상 댄서블

## 🤔 해석
- 인기는 valence(긍정성) 보다 다른 요인(아티스트 인지도, 마케팅)에 더 영향받는 듯
- 에너지와 댄서빌리티는 거의 같은 차원을 측정하는 것일 수도

## 💡 액션 아이템
- 추천 시스템 만들 때 valence는 약한 신호로 취급
- 에너지·댄서빌리티는 둘 중 하나만 써도 됨
- 다음 분석: 아티스트 유명도 같은 외부 요인 추가
```

### 🎯 좋은 해석의 5가지 특징

| 특징 | ❌ 나쁜 예 | ✅ 좋은 예 |
|------|----------|----------|
| **수치 인용** | "차이가 있다" | "평균이 23% 높다" |
| **불확실성 인정** | "이게 원인이다" | "이게 한 가지 가능한 원인이다" |
| **반례 언급** | 좋은 결과만 강조 | "단, 이런 경우는 예외" |
| **다음 질문 제시** | 결론으로 끝 | "다음엔 ___을 봐야" |
| **액션 연결** | 분석만 | "그래서 우리는 ___" |

### 🏋️ 최종 미션: 자기만의 가설 검증

```
나는 "BPM(tempo)이 빠를수록 인기가 많을 것이다" 라는 가설을 세웠어.
이걸 검증하는 분석을 처음부터 끝까지 해줘:
1. 가설 명확화
2. 필요한 차트 (1~2개)
3. 통계 검증
4. 해석 + 결론

hypothesis_check.py + hypothesis_report.md 두 개 파일로.
```

→ **AI는 도구, 가설은 내가 세운다**. 이게 Vibe Coding의 균형점이에요.

---

## 🪞 5분 회고

여기까지 따라왔다면 정말 대단해요! 🎉 잠시 멈추고 돌아봐요.

### 📝 스스로에게 던질 질문

**1. 가장 인상 깊었던 순간은?**
- 첫 차트가 떴을 때?
- 차트를 3차까지 다듬으며 좋아졌을 때?
- 예상과 다른 결과가 나왔을 때?

**2. Claude의 도움 없이 혼자 했다면 얼마나 걸렸을까요?**

**3. 다음에 분석해보고 싶은 데이터셋은?**
- 본인 Spotify 청취 기록?
- 영화 평점 데이터?
- 부동산 시세?

### 💭 토론거리

> "Vibe Coding으로 분석한 결과를 **얼마나 신뢰**할 수 있을까요?"
> "AI 시대의 **'데이터 리터러시'** 는 어떻게 달라져야 할까요?"

---

## 🆘 자주 막히는 지점

### Q1. CSV 파일 인코딩 에러 (`UnicodeDecodeError`)

**A.** 한국어/특수문자 데이터에서 자주 발생.

```
파일 인코딩 에러가 났어. 다음 인코딩들로 차례로 시도해줘:
utf-8 → utf-8-sig → cp949 → latin-1
```

또는 직접:

```python
df = pd.read_csv("tracks.csv", encoding="utf-8-sig")
```

### Q2. 차트에서 한글이 □□□ 로 깨져요

**A.** 폰트 설정 문제.

```python
import platform
import matplotlib.pyplot as plt

if platform.system() == "Darwin":      # Mac
    plt.rc("font", family="AppleGothic")
elif platform.system() == "Windows":   # Windows
    plt.rc("font", family="Malgun Gothic")
else:                                  # Linux
    plt.rc("font", family="NanumGothic")  # 사전 설치 필요

plt.rcParams["axes.unicode_minus"] = False  # 마이너스 깨짐 방지
```

### Q3. 메모리 부족 에러 (`MemoryError`)

**A.** 11만 행이라도 차트에 다 그리면 느려요.

```
점이 너무 많아서 무거워. df.sample(5000) 으로 샘플링해서 그려줘.
```

### Q4. 결과 차트 창이 바로 닫혀요

**A.** Claude Code가 셸 명령으로 실행하면 GUI 창 유지가 안 될 수 있어요.

```python
plt.savefig("output.png", dpi=150)   # 파일로 저장
plt.show()                            # 화면 표시
```

→ PNG 파일로 저장 후 직접 열어 확인.

### Q5. `pip install` 했는데 `ModuleNotFoundError`

**A.** Python 버전 불일치 가능성.

```bash
python -m pip install pandas matplotlib seaborn
# 또는
python3 -m pip install pandas matplotlib seaborn
```

`python` vs `python3` 일치시키기.

### Q6. Claude가 자꾸 다른 컬럼명을 써요

**A.** 실제 컬럼명을 명시적으로 알려주세요:

```
!python -c "import pandas as pd; print(pd.read_csv('tracks.csv').columns.tolist())"
```

→ 출력된 컬럼명을 그대로 보여주며 요청.

---

## 🎯 오늘 배운 핵심 정리

| 단계 | 핵심 학습 |
|------|-----------|
| 🎵 Vibe Coding | 흐름·반복·위임의 마인드셋 |
| 📥 탐색 | shape, dtypes, head, describe, isnull |
| 🧹 전처리 | drop_duplicates, dropna, 파생 컬럼 |
| 📊 시각화 | 일단 → 이쁘게 → 질문에 답하게 (3단계) |
| 🧠 해석 | 수치·불확실성·반례·다음·액션 |

### 💎 가장 중요한 교훈

> **"AI는 코드를 짜고, 나는 질문을 짠다."**
> **"좋은 분석 = 좋은 가설 + 좋은 데이터 + 좋은 해석"**

---

## 🎓 다음 단계

축하해요! 🎉 이제 데이터 한 줌 받으면 **분석 가능한 사람**이 됐어요.

**바로 도전해볼 만한 다음 프로젝트:**

1. 🎬 **IMDb 영화 데이터** — 평점·장르·연도 트렌드
2. 🏠 **Kaggle House Prices** — 회귀 모델 입문
3. 📈 **본인 Spotify 청취 기록** — privacy.spotify.com에서 데이터 요청
4. 🌡️ **공공 데이터 포털 기상 데이터** — 한국어 데이터 실전
5. 🐦 **본인 SNS 데이터** — 게시 시간대 분석

**더 깊이 배우고 싶다면:**

- 📘 **[프롬프트 작성법](./effective-prompting-and-claude-md.md)** — 더 좋은 분석 요청
- 🛠 **[Skills & Remote Control](./skills-and-remote-control.md)** — 자주 쓰는 분석을 Skill로
- 🧮 **[Python 계산기 실습](./python-calculator-tutorial.md)** — 점진적 개발 복습
- 📚 **[명령어 레퍼런스](./claude_commands-reference.md)** — `/compact`로 긴 분석 세션 관리

---

## 🌱 마무리: Fail Forward

이 실습에서:

> 🟢 **차트 4개 다 만들고 해석까지 술술 끝났다면** — 자기 데이터셋에 도전을!
> 🟡 **막히는 지점이 몇 번 있었다면** — 진짜 학습이 일어난 거예요
> 🔴 **아직 첫 차트도 못 그렸다면** — 한 번에 다 하려 하지 마세요. **딱 1개**만 끝까지 해보세요

학습 노트에 적어보세요:

```
✏️ 가장 의외였던 발견: ___
🔥 가장 헷갈렸던 단계: ___
💡 분석해보고 싶은 나만의 데이터: ___
🎵 Vibe Coding으로 시도해볼 다음 프로젝트: ___
```

📅 작성일: 2026.05.02
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
