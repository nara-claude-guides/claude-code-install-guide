# 간단한 Python 프로그램 구현 - 계산기 🧮

> Hello World를 끝냈다면, 다음 도전!  
> 자연어로 **진짜 동작하는 프로그램** 을 단계별로 만들어봐요.

---

## 📑 목차

- [학습 목표](#-학습-목표)
- [시작하기 전에](#-시작하기-전에)
- [🎬 단계 1: 가장 단순한 계산기](#-단계-1-가장-단순한-계산기)
- [🎬 단계 2: 사용자 입력 받기](#-단계-2-사용자-입력-받기)
- [🎬 단계 3: 함수로 정리 + 에러 처리](#-단계-3-함수로-정리--에러-처리)
- [🎬 단계 4: 반복 사용 가능하게](#-단계-4-반복-사용-가능하게)
- [🎬 단계 5: 기능 확장 (히스토리)](#-단계-5-기능-확장-히스토리)
- [🎬 단계 6: 테스트 코드 작성](#-단계-6-테스트-코드-작성)
- [🪞 5분 회고](#-5분-회고)
- [🌱 Fail Forward 시나리오](#-fail-forward-시나리오)
- [🎓 도전 과제](#-도전-과제)
- [📚 다음 단계](#-다음-단계)

---

## 🎯 학습 목표

이 실습을 마치면 다음을 할 수 있어요:

- ✅ 자연어로 **여러 단계에 걸쳐** 프로그램 발전시키기
- ✅ Claude의 코드를 **이해하고 수정 요청**하기
- ✅ 에러를 **두려워하지 않고** 디버깅하기
- ✅ **점진적 개선 (Iterative Development)** 의 흐름 익히기
- ✅ Python 기본 문법(if, while, 함수, 예외처리) **체득**

> 💡 **핵심 메시지**: "한 번에 완벽하게" 가 아니라 **"조금씩 발전시키며"** 가 진짜 코딩이에요!

---

## 📋 시작하기 전에

- ✅ [Hello World 실습](./first-conversation-hello-world.md) 완료
- ✅ Python 3 설치 확인 (`python3 --version` 또는 `python --version`)
- ✅ 마음의 준비: **"틀린 답이 나와도 괜찮아"** 🌱

> ⏱ **소요 시간**: 약 40~60분  
> 🎯 **권장 모드**: Plan 모드 (사고 과정 관찰)

### 작업 폴더 준비

```bash
mkdir python-calculator
cd python-calculator
claude
```

---

## 🎬 단계 1: 가장 단순한 계산기

### 💬 첫 번째 프롬프트

```
calculator.py 파일을 만들어줘. 
3 + 5, 10 - 2, 4 * 6, 20 / 4 의 결과를 출력하는 가장 단순한 계산기야.
```

### 🎁 Claude의 응답 예시

```
⏺ Write(calculator.py)
  ⎿ 파일을 생성했습니다 (4줄)

calculator.py 파일을 만들었어요:

print("3 + 5 =", 3 + 5)
print("10 - 2 =", 10 - 2)
print("4 * 6 =", 4 * 6)
print("20 / 4 =", 20 / 4)

실행하려면: python calculator.py
```

### ▶ 실행해보기

```
!python calculator.py
```

**결과:**

```
3 + 5 = 8
10 - 2 = 8
4 * 6 = 24
20 / 4 = 5.0
```

### 👀 여기서 짚을 포인트

| 발견 | 의미 |
|------|------|
| `print("3 + 5 =", ...)` | 따옴표 안은 그대로 출력, 밖은 계산 |
| `20 / 4 = 5.0` | 나누기는 **항상 소수점** 결과 (`/` 연산자) |
| `,` 로 연결 | print 안에서 여러 값 출력하는 방법 |

### 🤔 학습자에게 던질 질문

> "5.0과 5는 다를까요? Claude에게 물어보세요!"

```
20을 4로 나누면 왜 5가 아니라 5.0이 나와?
```

→ Claude가 자동으로 **정수 나눗셈(`//`)** 도 설명해줄 거예요. 추가 학습 기회!

---

## 🎬 단계 2: 사용자 입력 받기

이제 매번 코드를 고치는 게 아니라, **실행할 때마다 다른 숫자**로 계산하게 만들어봐요.

### 💬 다음 프롬프트

```
calculator.py를 수정해줘.
사용자에게 두 숫자와 연산자(+, -, *, /)를 입력받아서 계산 결과를 출력하게 만들어줘.
```

### 🎁 Claude의 응답 예시

```python
num1 = float(input("첫 번째 숫자: "))
op = input("연산자를 입력하세요 (+, -, *, /): ")
num2 = float(input("두 번째 숫자: "))

if op == "+":
    result = num1 + num2
elif op == "-":
    result = num1 - num2
elif op == "*":
    result = num1 * num2
elif op == "/":
    result = num1 / num2

print(f"{num1} {op} {num2} = {result}")
```

### ▶ 실행해보기

```
!python calculator.py
```

```
첫 번째 숫자: 15
연산자를 입력하세요 (+, -, *, /): *
두 번째 숫자: 4
15.0 * 4.0 = 60.0
```

### 👀 새로 배운 개념

| 개념 | 설명 |
|------|------|
| `input()` | 사용자가 키보드로 입력하는 값을 받음 |
| `float(...)` | 문자를 **숫자(소수)** 로 변환 |
| `if / elif / else` | 조건에 따라 다르게 동작 |
| `f"..."` | f-string. 변수를 문자열에 넣는 방법 |

### 🐛 일부러 에러 내보기 (Fail Forward!)

연산자를 `^` 같이 이상한 걸 넣어보세요:

```
!python calculator.py
첫 번째 숫자: 5
연산자를 입력하세요 (+, -, *, /): ^
두 번째 숫자: 3
```

**결과:**

```
Traceback (most recent call last):
  File "calculator.py", line 16, in <module>
    print(f"{num1} {op} {num2} = {result}")
NameError: name 'result' is not defined
```

🌱 **에러는 친구예요.** 이걸 그대로 Claude에게 보여주면 다음 단계로 자연스럽게 넘어가요!

---

## 🎬 단계 3: 함수로 정리 + 에러 처리

방금 만난 에러를 해결하면서, 코드를 **더 깔끔하게** 만들어봐요.

### 💬 프롬프트

```
방금 ^ 같은 잘못된 연산자나 0으로 나누기를 했을 때 에러가 나.
이런 경우를 처리하고, 코드를 함수로 정리해줘.
```

### 🎁 Claude의 응답 예시

```python
def calculate(num1, num2, op):
    """두 숫자와 연산자를 받아 결과를 반환"""
    if op == "+":
        return num1 + num2
    elif op == "-":
        return num1 - num2
    elif op == "*":
        return num1 * num2
    elif op == "/":
        if num2 == 0:
            return "❌ 0으로 나눌 수 없어요!"
        return num1 / num2
    else:
        return f"❌ 지원하지 않는 연산자예요: {op}"


def main():
    """프로그램 시작점"""
    print("🧮 간단한 계산기")
    print("-" * 20)
    
    try:
        num1 = float(input("첫 번째 숫자: "))
        op = input("연산자 (+, -, *, /): ")
        num2 = float(input("두 번째 숫자: "))
        
        result = calculate(num1, num2, op)
        print(f"\n결과: {num1} {op} {num2} = {result}")
    except ValueError:
        print("❌ 숫자를 정확히 입력해주세요!")


if __name__ == "__main__":
    main()
```

### 👀 새로 배운 개념

| 개념 | 비유 |
|------|------|
| `def 함수이름()` | **재사용 가능한 도구** 만들기 |
| `return` | 함수가 결과를 **돌려주기** |
| `try / except` | "**위험한 일 시도하다 실패하면 이렇게 대처**" |
| `if __name__ == "__main__":` | "이 파일이 직접 실행될 때만 main() 호출" |
| `"""..."""` | 함수 설명 (docstring) |

### 🤔 핵심 질문 던지기

> "왜 함수로 나눴을까요?"

답:
- 🔄 **재사용** 가능
- 🧪 **테스트** 쉬움 (다음 단계에서!)
- 🧹 **정리정돈** 잘됨

### ▶ 다양하게 테스트해보기

```
!python calculator.py
```

| 입력 | 결과 |
|------|------|
| `5, +, 3` | 결과: 5.0 + 3.0 = 8.0 ✅ |
| `10, /, 0` | ❌ 0으로 나눌 수 없어요! ✅ |
| `5, ^, 3` | ❌ 지원하지 않는 연산자예요: ^ ✅ |
| `abc, +, 3` | ❌ 숫자를 정확히 입력해주세요! ✅ |

🎉 **이제 망가지지 않는 튼튼한 코드!**

---

## 🎬 단계 4: 반복 사용 가능하게

매번 다시 실행하는 건 귀찮아요. **한 번 켜면 계속 쓸 수 있게** 만들어봐요.

### 💬 프롬프트

```
계산기를 반복해서 쓸 수 있게 해줘. 
'q'를 입력하면 종료하고, 그 외엔 계속 계산할 수 있게.
```

### 🎁 Claude의 응답 예시

```python
def calculate(num1, num2, op):
    """두 숫자와 연산자를 받아 결과를 반환"""
    if op == "+":
        return num1 + num2
    elif op == "-":
        return num1 - num2
    elif op == "*":
        return num1 * num2
    elif op == "/":
        if num2 == 0:
            return "❌ 0으로 나눌 수 없어요!"
        return num1 / num2
    else:
        return f"❌ 지원하지 않는 연산자예요: {op}"


def main():
    """프로그램 시작점"""
    print("🧮 간단한 계산기")
    print("종료하려면 'q'를 입력하세요")
    print("-" * 30)
    
    while True:
        first = input("\n첫 번째 숫자 (또는 q): ")
        if first.lower() == "q":
            print("👋 안녕히 가세요!")
            break
        
        try:
            num1 = float(first)
            op = input("연산자 (+, -, *, /): ")
            num2 = float(input("두 번째 숫자: "))
            
            result = calculate(num1, num2, op)
            print(f"➡ {num1} {op} {num2} = {result}")
        except ValueError:
            print("❌ 숫자를 정확히 입력해주세요!")


if __name__ == "__main__":
    main()
```

### 👀 새로 배운 개념

| 개념 | 비유 |
|------|------|
| `while True:` | "계속 반복해" 명령 (자판기처럼) |
| `break` | 반복 빠져나오기 |
| `.lower()` | 대문자 'Q'도 'q'로 처리 |

### ▶ 시연해보기

```
!python calculator.py
```

```
🧮 간단한 계산기
종료하려면 'q'를 입력하세요
------------------------------

첫 번째 숫자 (또는 q): 5
연산자 (+, -, *, /): +
두 번째 숫자: 3
➡ 5.0 + 3.0 = 8.0

첫 번째 숫자 (또는 q): 10
연산자 (+, -, *, /): *
두 번째 숫자: 4
➡ 10.0 * 4.0 = 40.0

첫 번째 숫자 (또는 q): q
👋 안녕히 가세요!
```

🎉 **진짜 계산기 같죠?**

---

## 🎬 단계 5: 기능 확장 (히스토리)

이전 계산 기록을 볼 수 있으면 좋겠어요!

### 💬 프롬프트

```
계산 기록을 저장해서 'h'를 입력하면 지금까지의 계산 내역을 다 볼 수 있게 해줘.
```

### 🎁 Claude의 응답 예시 (핵심 부분)

```python
def main():
    print("🧮 간단한 계산기")
    print("'q' = 종료, 'h' = 히스토리")
    print("-" * 30)
    
    history = []  # 계산 기록 저장
    
    while True:
        first = input("\n첫 번째 숫자 (q/h): ")
        
        if first.lower() == "q":
            print("👋 안녕히 가세요!")
            break
        
        if first.lower() == "h":
            if not history:
                print("📝 아직 계산 기록이 없어요")
            else:
                print("\n📝 계산 히스토리:")
                for i, record in enumerate(history, 1):
                    print(f"  {i}. {record}")
            continue
        
        try:
            num1 = float(first)
            op = input("연산자 (+, -, *, /): ")
            num2 = float(input("두 번째 숫자: "))
            
            result = calculate(num1, num2, op)
            record = f"{num1} {op} {num2} = {result}"
            print(f"➡ {record}")
            
            history.append(record)  # 기록에 추가
        except ValueError:
            print("❌ 숫자를 정확히 입력해주세요!")
```

### 👀 새로 배운 개념

| 개념 | 비유 |
|------|------|
| `history = []` | **빈 목록** (택배 배송 기록 노트) |
| `.append(record)` | 목록에 **추가** |
| `enumerate(...)` | 번호 매겨서 보여주기 (1, 2, 3...) |
| `continue` | 현재 반복 건너뛰고 다시 시작 |

### ▶ 시연해보기

```
첫 번째 숫자 (q/h): h

📝 계산 히스토리:
  1. 5.0 + 3.0 = 8.0
  2. 10.0 * 4.0 = 40.0
  3. 100.0 / 4.0 = 25.0
```

---

## 🎬 단계 6: 테스트 코드 작성

진짜 개발자처럼 **테스트 코드** 도 만들어봐요!

### 💬 프롬프트

```
calculate 함수가 잘 동작하는지 확인하는 테스트 코드를 test_calculator.py 파일로 만들어줘.
pytest 안 써도 되는 간단한 형태로.
```

### 🎁 Claude의 응답 예시

```python
# test_calculator.py
from calculator import calculate


def test_addition():
    assert calculate(2, 3, "+") == 5
    assert calculate(0, 0, "+") == 0
    assert calculate(-1, 1, "+") == 0
    print("✅ 덧셈 테스트 통과")


def test_subtraction():
    assert calculate(10, 3, "-") == 7
    assert calculate(0, 5, "-") == -5
    print("✅ 뺄셈 테스트 통과")


def test_multiplication():
    assert calculate(4, 5, "*") == 20
    assert calculate(0, 100, "*") == 0
    print("✅ 곱셈 테스트 통과")


def test_division():
    assert calculate(10, 2, "/") == 5
    assert calculate(7, 2, "/") == 3.5
    print("✅ 나눗셈 테스트 통과")


def test_division_by_zero():
    result = calculate(5, 0, "/")
    assert "0으로 나눌 수 없어요" in result
    print("✅ 0으로 나누기 처리 통과")


def test_invalid_operator():
    result = calculate(5, 3, "^")
    assert "지원하지 않는" in result
    print("✅ 잘못된 연산자 처리 통과")


if __name__ == "__main__":
    print("🧪 계산기 테스트 시작\n")
    test_addition()
    test_subtraction()
    test_multiplication()
    test_division()
    test_division_by_zero()
    test_invalid_operator()
    print("\n🎉 모든 테스트 통과!")
```

### ▶ 실행해보기

```
!python test_calculator.py
```

```
🧪 계산기 테스트 시작

✅ 덧셈 테스트 통과
✅ 뺄셈 테스트 통과
✅ 곱셈 테스트 통과
✅ 나눗셈 테스트 통과
✅ 0으로 나누기 처리 통과
✅ 잘못된 연산자 처리 통과

🎉 모든 테스트 통과!
```

### 👀 새로 배운 개념

| 개념 | 의미 |
|------|------|
| `assert` | "이게 참이어야 해. 아니면 에러" |
| `from X import Y` | 다른 파일의 함수 가져오기 |
| **테스트 주도 개발** | 코드보다 테스트를 먼저! (TDD) |

### 🌟 보너스: 일부러 깨뜨려보기

```
calculate 함수에서 + 동작을 일부러 *로 바꿔서, 테스트가 어떻게 실패하는지 보여줘.
```

→ 테스트가 실패하는 모습을 보면 **테스트의 가치** 를 체감할 수 있어요!

---

## 🪞 5분 회고

여기까지 왔다면 정말 대단해요! 🎉 잠시 멈추고 돌아봐요.

### 📝 스스로에게 던질 질문

**1. 가장 자랑스러운 순간은?**
- 함수로 정리했을 때 코드가 깔끔해진 느낌?
- 무한 루프 추가했을 때 진짜 프로그램 같아진 느낌?
- 테스트가 모두 통과했을 때?

**2. 가장 헷갈렸던 개념은?**
- `if __name__ == "__main__":`?
- `try / except`?
- `f-string`?

**3. Claude가 잘했던 것 / 부족했던 것은?**

### 💭 토론거리

> "이 코드를 처음부터 끝까지 **혼자** 짜라고 하면 얼마나 걸렸을까요?"  
> "Claude의 도움으로 무엇이 가능해졌고, 무엇이 그래도 어려웠나요?"

---

## 🌱 Fail Forward 시나리오

실습하면서 학습자들이 **자주 막히는 지점** 과 **회복 방법** 이에요.

### 🚧 장애 1: "ModuleNotFoundError"

```
ModuleNotFoundError: No module named 'calculator'
```

**원인:** test_calculator.py와 calculator.py가 **다른 폴더**에 있음

**해결:** Claude에게 그대로 보여주기

```
ModuleNotFoundError 에러가 났어. 두 파일이 같은 폴더에 있는데도 그래.
```

→ Claude가 작업 디렉토리, 가상환경 등을 점검해줘요.

### 🚧 장애 2: 입력값이 한국어로 깨져요

```
첫 번째 숫자: 
UnicodeDecodeError: ...
```

**해결:**

```bash
# Windows라면
set PYTHONIOENCODING=utf-8
python calculator.py

# Mac/Linux라면
export PYTHONIOENCODING=utf-8
python calculator.py
```

또는 Claude에게:

```
한국어 입출력이 깨지지 않게 코드 시작 부분에 인코딩 설정 추가해줘.
```

### 🚧 장애 3: while 루프가 안 멈춰요!

**비상 종료:**
- 터미널: `Ctrl + C`
- Claude Code 안: `Esc` (응답 중단)

> 💡 **`Ctrl+C`와 `Esc`의 차이**
> - `Ctrl+C`: 셸 명령 중단 (`!python ...` 같은 거)
> - `Esc`: Claude의 응답만 멈춤

### 🚧 장애 4: Claude가 너무 복잡한 코드를 만들어요

```
이 코드가 너무 어려워. 중학생도 이해할 수 있게 가장 단순한 버전으로 다시 만들어줘.
```

→ 학습 수준에 맞춰달라고 명확히 요청하기!

---

## 🎓 도전 과제

스스로 해볼 만한 추가 과제예요. **Claude에게 물어가며** 해보세요!

### 🥉 초급

- [ ] `**` (제곱) 연산자 추가 — 예: `2 ** 3 = 8`
- [ ] `%` (나머지) 연산자 추가 — 예: `10 % 3 = 1`
- [ ] 결과를 정수로 출력 (소수점이 .0이면)

### 🥈 중급

- [ ] 마지막 결과를 다음 계산에 자동으로 넣기 (Ans 기능)
- [ ] 히스토리를 파일로 저장 (`history.txt`)
- [ ] 컬러 출력 추가 (긍정/에러 메시지)

### 🥇 고급

- [ ] **Calculator 클래스**로 리팩토링
- [ ] `pytest` 도입해서 정식 테스트
- [ ] Tkinter로 **GUI** 버전 만들기
- [ ] Flask로 **웹 계산기** 만들기

> 💡 **각 과제를 Claude에게 요청할 때 팁:**  
> "지금 코드에 ___ 기능을 추가해줘. 이유와 어떻게 동작하는지 설명도 같이."

---

## 🎯 오늘 배운 핵심 정리

이 실습으로 익힌 개발 패턴:

| 단계 | 핵심 학습 |
|------|-----------|
| 1️⃣ 단순 출력 | print, 산술 연산자 |
| 2️⃣ 사용자 입력 | input, if/elif/else, f-string |
| 3️⃣ 함수 + 에러처리 | def, return, try/except |
| 4️⃣ 반복 | while, break, .lower() |
| 5️⃣ 자료구조 | 리스트, append, enumerate |
| 6️⃣ 테스트 | assert, import, TDD 마인드 |

### 💎 가장 중요한 교훈

> **"한 번에 완벽하게 만드는 건 불가능해요."**  
> **"조금씩, 차근차근, 망가뜨려가며 발전시키는 게 진짜 개발이에요."**

이게 바로 **Iterative Development(점진적 개발)** 이고, AI 시대 코딩의 핵심이에요!

---

## 📚 다음 단계

축하해요! 🎉 이제 Python 기본기를 Claude Code와 함께 익혔어요.

**바로 도전해볼 만한 다음 프로젝트:**

1. 🎲 **숫자 맞히기 게임** — 1~100 중 컴퓨터가 정한 숫자 맞히기
2. ✊ **가위바위보** — 사용자 vs 컴퓨터
3. 📝 **할일 관리 앱 (TODO)** — 추가/삭제/저장
4. 🌡️ **단위 변환기** — 섭씨↔화씨, km↔mile
5. 🎮 **틱택토 게임** — 2인용 OX 게임

**더 깊이 배우고 싶다면:**

- 🩺 **[/status 명령어 가이드](./status-reading-guide.md)** — 환경 점검 마스터
- 📘 **[명령어 레퍼런스](./commands-reference.md)** — 슬래시 명령어 다 보기
- 🔧 **CLAUDE.md 작성하기** — 프로젝트 컨텍스트로 Claude를 더 똑똑하게

---

## 🌱 마무리: Fail Forward

이 실습에서:

> 🟢 **모든 단계가 술술 풀렸다면** — 다음에는 더 어려운 도전을!  
> 🟡 **몇 번 막혔다 풀어냈다면** — 진짜 학습이 일어난 거예요  
> 🔴 **아직 몇 단계 남았다면** — 내일의 멋진 실습이 기다리고 있어요

학습 노트에 적어보세요:

```
✏️ 가장 인상 깊었던 단계: ___
🔥 가장 어려웠던 부분: ___
💡 다음에 만들어보고 싶은 프로그램: ___
```

📅 작성일: 2026.04.27  
✍️ Claude Code 강의 실습용 환경 구축 가이드 시리즈
