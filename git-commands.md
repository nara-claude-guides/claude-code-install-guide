# Git 명령어 정리 🛠️

터미널에서 자주 쓰는 Git 명령어를 한눈에 보기 좋게 정리했습니다.

---

## 📑 목차

- [1. 초기 설정 & 저장소](#1-초기-설정--저장소)
- [2. 상태 확인](#2-상태-확인)
- [3. 커밋하기](#3-커밋하기)
- [4. 브랜치 관리](#4-브랜치-관리)
- [5. 원격 저장소 동기화](#5-원격-저장소-동기화)
- [6. 되돌리기 / 취소](#6-되돌리기--취소)
- [7. 스태시 (임시 저장)](#7-스태시-임시-저장)
- [8. 자주 쓰는 조합 패턴](#8-자주-쓰는-조합-패턴)
- [⚠️ 주의해야 할 명령어](#️-주의해야-할-명령어)
- [💡 꿀팁](#-꿀팁)

---

## 1. 초기 설정 & 저장소

```bash
git init                          # 새 저장소 만들기
git clone <URL>                   # 원격 저장소 복제
git config --global user.name "이름"
git config --global user.email "이메일"
git remote -v                     # 연결된 원격 저장소 확인
git remote add origin <URL>       # 원격 저장소 연결
```

## 2. 상태 확인

```bash
git status                        # 변경된 파일 확인
git diff                          # 변경 내용 비교 (스테이지 전)
git diff --staged                 # 스테이지된 변경 내용 비교
git log                           # 커밋 로그
git log --oneline --graph --all   # 그래프로 보기 (가장 많이 씀)
```

## 3. 커밋하기

```bash
git add <파일>                    # 특정 파일 스테이징
git add .                         # 전체 변경사항 스테이징
git commit -m "메시지"            # 커밋
git commit -am "메시지"           # add + commit 한번에 (추적중인 파일만)
git commit --amend                # 마지막 커밋 수정
```

## 4. 브랜치 관리

```bash
git branch                        # 브랜치 목록
git branch <이름>                 # 브랜치 생성
git checkout <브랜치>             # 브랜치 이동
git switch <브랜치>               # 이동 (최신 명령어)
git checkout -b <이름>            # 생성 + 이동
git switch -c <이름>              # 생성 + 이동 (최신)
git branch -d <이름>              # 브랜치 삭제 (병합된 것만)
git branch -D <이름>              # 강제 삭제
git merge <브랜치>                # 현재 브랜치에 병합
git rebase <브랜치>               # 리베이스
```

## 5. 원격 저장소 동기화

```bash
git push origin main              # 푸시
git push -u origin main           # 업스트림 설정 + 푸시 (처음 한 번)
git push -f origin main           # ⚠️ 강제 푸시 (히스토리 덮어쓰기)
git push --force-with-lease       # 더 안전한 강제 푸시 (협업 권장)
git pull                          # 원격에서 가져와 병합
git pull --rebase                 # 리베이스로 가져오기 (히스토리 깔끔)
git fetch                         # 원격 정보만 가져오기 (병합 X)
```

## 6. 되돌리기 / 취소

```bash
git restore <파일>                # 변경 취소 (스테이지 전)
git restore --staged <파일>       # 스테이징 취소
git reset HEAD~1                  # 마지막 커밋 취소 (변경은 유지)
git reset --soft HEAD~1           # 커밋만 취소, 스테이지 유지
git reset --hard HEAD~1           # ⚠️ 커밋 + 변경 모두 삭제
git revert <커밋해시>             # 해당 커밋을 취소하는 새 커밋 생성 (안전)
```

## 7. 스태시 (임시 저장)

```bash
git stash                         # 작업중 변경사항 임시 저장
git stash list                    # 저장된 목록
git stash pop                     # 최근 스태시 복원 + 삭제
git stash apply                   # 복원만 (스태시 유지)
git stash drop                    # 스태시 삭제
git stash clear                   # 전체 삭제
```

## 8. 자주 쓰는 조합 패턴

```bash
# 새 작업 시작
git switch main && git pull && git switch -c feature/새기능

# 커밋 후 푸시
git add . && git commit -m "메시지" && git push

# 마지막 커밋 메시지만 수정 후 강제 푸시
git commit --amend -m "새 메시지" && git push -f

# 원격 main에 맞게 강제로 동기화
git fetch origin && git reset --hard origin/main
```

---

## ⚠️ 주의해야 할 명령어

| 명령어 | 위험성 |
|--------|--------|
| `git push -f` | 다른 사람의 커밋을 날릴 수 있음 → `--force-with-lease` 권장 |
| `git reset --hard` | 작업 내용 복구 불가 |
| `git clean -fd` | 추적되지 않은 파일/폴더 삭제 |
| `git rebase` (공유 브랜치에서) | 협업자 히스토리 꼬임 |

---

## 💡 꿀팁

```bash
git log --oneline -10             # 최근 10개 커밋만
git reflog                        # 모든 HEAD 이동 기록 (실수 복구용 ⭐)
git blame <파일>                  # 줄별 작성자 확인
git show <커밋해시>               # 특정 커밋 내용 보기
git cherry-pick <커밋해시>        # 특정 커밋만 가져오기
```

> **`git reflog`** 는 실수로 `reset --hard` 했을 때 살아남을 수 있는 마지막 동아줄입니다. 꼭 기억해두세요!

---

📅 작성일: 2026.04.27  
✍️ Git 명령어 빠른 참조용 치트시트
