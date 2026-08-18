---
name: create-til
description: Write a TIL (Today I Learned) entry in Korean and save it as a topic-named markdown file (til-{topic}.md). Use this skill whenever the user says TIL, 오늘 배운 것, 오늘 배운 거, 오늘 정리, 데일리 기록, or asks to jot down something they just figured out — a flag they discovered, an error they finally understood, a concept that clicked. Trigger it even when they just say "이거 til로 남겨줘" or "오늘 거 정리해줘" right after solving something together, and even when the request looks small enough to answer inline.
---

# TIL

Capture one thing learned today into `til-{topic}.md`, in Korean, 한다체.

A TIL is not a small blog post. Blog posts explain something to a stranger; a TIL is a note to yourself six months from now, when you've forgotten the whole thing and are searching your own repo for the answer. That difference drives most of the rules here — no 서론, no 인사, no "이번 글에서는", and no explaining background you already know.

If the material is actually a full 트러블슈팅 story with a debugging arc worth 2,000자, say so and offer the blog post skill instead. Don't silently compress it into a TIL.

## Workflow

1. **Ask what material they have — before writing anything.** See 재료 확인 below.
2. **Decide the topic slug and check whether that file already exists.** 주제마다 한 파일이라, 같은 주제 파일이 있으면 새로 만들지 말고 아래에 덧붙인다. See 파일 다루기 below — 이걸 건너뛰면 전에 쓴 항목이 날아간다.
3. **Write the entry** (500~800자, 아래 형식).
4. **점검 후 저장**하고 파일을 보여준다.

### 재료 확인

Ask before writing, every time. A TIL assembled from general knowledge is just a worse version of the docs — the value is entirely in the specifics: the actual error string, the actual flag, what they believed before they were corrected.

무엇을 물어볼지는 상황에 따라 다르지만 대체로 이 셋이다:

- 뭘 하다가 만났나 (맥락)
- 처음엔 뭐라고 알고 있었나 (오해)
- 코드나 에러 메시지 원문이 있나

**대화에 이미 재료가 있으면 백지에서 묻지 않는다.** 방금 같이 디버깅하고 나서 "til로 남겨줘"라고 하면 재료는 눈앞에 있다. 이럴 땐 무엇을 가지고 쓸 생각인지 한 줄로 말하고 더 넣거나 고칠 게 있는지만 확인한 다음 쓴다. 스레드에 뻔히 있는 걸 다시 물으면 안 읽은 것처럼 보인다.

없다고 하면 있는 것만으로 쓴다. 두 번 묻지 않는다.

## 항목 형식

````markdown
## 2026-08-18 — 배운 것을 한 줄로 (질문형 말고 서술형)

본문 — 한다체, 500~800자

```js
// 필요할 때만
```

참고: https://...
````

제목은 `useEffect 정리`처럼 주제만 적지 말고, 알게 된 내용을 담는다 — `useEffect 의존성 배열에 객체를 넣으면 매 렌더마다 새로 실행된다`처럼. 나중에 파일 목록만 훑을 때 제목만 보고 찾을 수 있어야 한다.

본문에는 세 가지가 들어간다. 라벨을 붙일 필요는 없고 자연스럽게 이어 쓰면 된다.

- **어쩌다 만났나** — 한두 문장. 맥락이 없으면 반년 뒤에 이게 왜 중요했는지 기억이 안 난다.
- **뭘 알게 됐나** — 핵심. 여기가 제일 길다.
- **뭘 잘못 알고 있었나** — TIL에서 제일 값어치 있는 부분이다. 배웠다는 건 보통 전에 알던 게 틀렸다는 뜻이니까. 오해가 없었으면 굳이 안 써도 되지만, 있었으면 반드시 남긴다.

### 직접 해결한 문제라면: 왜 → 어떻게 → 무엇을

내가 겪고 고친 문제를 남기는 거라면 본문을 이 순서로 쓴다. 500~800자 안이니까 각각 한 문단씩이면 충분하다.

- **왜** — 뭐가 문제였고 원인이 뭐였나
- **어떻게** — 어떻게 고쳤나 (코드나 명령어)
- **무엇을** — 뭐가 달라졌고 뭘 배웠나

해결책부터 쓰지 않는다. 반년 뒤에 같은 증상으로 이 파일을 뒤질 때, 증상이 먼저 나와야 찾는다.

코드는 있으면 좋지만 억지로 넣지 않는다. 넣을 땐 언어 태그를 붙이고, 파일 전체 말고 문제가 되는 몇 줄만 남긴다.

참고 링크는 실제로 읽은 것만. 없으면 줄 자체를 뺀다.

재료가 얇으면 — 한두 줄짜리 메모만 있으면 — 주제에 맞는 공식 문서나 이슈를 찾아 사실을 확인하고 그 링크를 `참고`에 남긴다. 다만 TIL은 짧아도 되는 형식이라 억지로 늘리지 않는다. 300자짜리 항목은 그대로 두는 게 맞다. 검색해서 알게 된 건 문장 안에서 출처를 밝히고, 내가 직접 겪은 것처럼 쓰지 않는다.

## 말투

블로그와 같은 **한다체**다. 격식 차린 논문투가 아니라 편하게 쓰는 한다체이고, 한 항목 안에서 일관되게 유지한다.

- 종결어미: `-다`, `-이다`, `-했다`, `-한다`, `-된다`
- 딱딱해지지 않게 가끔 구어체를 섞는다: `-더라`, `-거든`, `-지`
- 1인칭은 `나`다. 그런데 TIL은 어차피 전부 내 얘기라 주어를 빼는 게 자연스럽다.
- `-습니다`나 `-해요`로 새지 않게 한다.

기계 번역투는 TIL에서도 똑같이 티가 난다. 자주 나오는 것들:

| 이렇게 쓰기 쉬운데 | 이렇게 고친다 |
|---|---|
| ~에 대해 알아보았습니다 | ~를 알게 됐다 |
| ~를 통해 해결했다 | ~로 해결했다 |
| 장점을 가지고 있다 | 장점이 있다 |
| 사용하는 것이 가능하다 | 쓸 수 있다 |
| 그것은 캐시 문제였다 | 캐시 문제였다 |

## 파일 다루기

파일명은 `til-{topic}.md`다. 저장 위치는 `/mnt/user-data/outputs/`.

topic은 영문 소문자와 하이픈으로 만든다 — `til-git-reflog.md`, `til-docker-multistage.md`, `til-css-grid.md`. 한글 파일명은 배포 환경에 따라 깨진다.

**주제 크기가 이 구조의 전부다.** 너무 좁게 잡으면 (`til-useeffect-dependency-array-object.md`) 파일이 한 번 쓰고 버려지는 조각으로 흩어지고, 너무 넓게 잡으면 (`til-react.md`) 나중에 그 안에서 다시 찾아야 한다. 도구 하나, 개념 하나 정도가 맞다. 이미 쓰던 슬러그가 있으면 새로 만들지 말고 그대로 쓴다.

**같은 주제 파일이 이미 있으면 덧붙인다.** 덮어쓰지 않는다. 찾는 순서:

1. 이번 대화에서 방금 만든 같은 주제 파일이 있나
2. 사용자가 올린 파일 중에 있나 (`/mnt/user-data/uploads/`)
3. 둘 다 없으면 새로 만든다

여기서 솔직해야 하는 부분이 있다. 이 환경은 대화가 끝나면 파일이 사라져서, 전에 쓴 `til-git-reflog.md`를 알아서 찾아올 수 없다. 그러니까 같은 주제로 전에 쓴 게 있을 법하면, 넘겨주면 이어서 쓰겠다고 한 줄로 말한다. 안 준다고 하면 새 항목만 담긴 파일을 만들어서 붙여 넣을 수 있게 한다.

새로 만드는 파일은 이렇게 연다:

````markdown
# git reflog

## 2026-08-18 — reflog는 rebase로 사라진 커밋도 들고 있다

...
````

주제 제목(`#`)은 파일당 하나다. 항목을 덧붙일 때 또 만들지 않는다. 항목 제목(`##`)에는 날짜를 붙인다 — 파일이 주제로 묶이니까 시간 순서는 항목 제목이 들고 있어야 한다. 새 항목은 맨 아래에 붙인다.

`##` 항목 사이에는 빈 줄을 넣는다. 코드 블록과 표 앞뒤도 마찬가지다.

## 마지막 점검

- [ ] 제목만 보고 내용을 알 수 있나
- [ ] 맥락(어쩌다 만났나)이 한두 문장 들어갔나
- [ ] 오해했던 지점이 있었다면 적었나
- [ ] 해결한 문제라면 왜 → 어떻게 → 무엇을 순서인가
- [ ] 한다체가 끝까지 유지됐나 (`-해요`, `-습니다` 확인)
- [ ] 번역투 표의 패턴이 남아 있나
- [ ] 500~800자 안인가 — 넘치면 블로그 글감이다
- [ ] 검색으로 확인한 내용이면 출처를 밝히고 참고 링크를 남겼나
- [ ] 주제 슬러그가 도구/개념 단위로 적당한가 — 너무 좁거나 넓지 않나
- [ ] 같은 주제 파일이 있었다면 덮어쓰지 않고 아래에 덧붙였나
- [ ] `#` 주제 제목이 파일에 하나만 있고, `##` 항목에 날짜가 붙었나
- [ ] 서론이나 인사말로 시작하지 않았나

## 예시

**Input:** "git rebase -i 하다가 실수로 커밋 날린 거 reflog로 살렸어. til 남겨줘"

**Output:**

````markdown
## 2026-08-18 — reflog는 rebase로 사라진 커밋도 들고 있다

인터랙티브 rebase 중에 `drop`을 잘못 눌러서 커밋 두 개를 날렸다. 원격에 안 올린 커밋이라 복구가 안 되는 줄 알고 한참 헤맸다.

`git reflog`를 찍어보니 rebase 전 HEAD가 그대로 남아 있었다. reflog는 브랜치 히스토리가 아니라 HEAD가 거쳐 간 자리를 전부 기록하거든. rebase나 reset처럼 히스토리를 바꾸는 명령을 써도 이전 위치가 남는다.

```bash
git reflog
# 7a3f1c2 HEAD@{3}: rebase -i (start): checkout main
git reset --hard HEAD@{3}
```

커밋은 브랜치에서 떨어져 나갔을 뿐이지 지워진 게 아니었다. gc가 돌기 전까지는 며칠 여유가 있고. "커밋을 날렸다"는 표현 자체가 사실은 틀린 말이었다.

참고: https://git-scm.com/docs/git-reflog
````

맥락 한 문단, 핵심 한 문단, 오해 한 줄. 서론 없이 바로 시작한다.
