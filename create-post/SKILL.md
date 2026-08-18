---
name: create-post
description: Write blog posts in Korean (한다체) as a markdown file ready for velog or a GitHub blog. Use this skill whenever the user asks for a blog post, 블로그 글, 포스팅, velog 글, 개발 블로그, 회고, or asks to turn something they just did — a bug they fixed, a tool they learned, a project they shipped — into a writeup. Trigger it even when they only say "이거 글로 써줘" or "write this up as a post" without naming a platform, and even when the request looks like a simple one-shot writing task. For TIL entries, use the til skill instead.
---

# Korean Blog Post

Write publishable Korean blog posts as `.md` files. The hard part isn't the Korean — it's that machine-written Korean has a distinct texture (번역투, 과한 격식, 기계적인 3단 구조) that readers spot instantly. Most of this skill is about not sounding like that.

## Workflow

**TIL 요청이면 이 스킬을 쓰지 않는다.** TIL은 `til` 스킬이 따로 있으니 그쪽으로 넘긴다. "TIL", "오늘 배운 거", "오늘 정리", "데일리 기록" 같은 말이 나오면 TIL로 본다 — 블로그에 올린다고 해도 마찬가지다. 형식과 분량이 달라서, 이 스킬로 쓰면 TIL 자리에 짧은 블로그 글이 들어간다.

`til` 스킬이 안 보이면 조용히 이 스킬로 써버리지 말고, 그 스킬을 못 찾겠다고 말한 다음 이대로 진행할지 물어본다.

1. **Ask what material they have — before writing anything.** See below.
2. **Identify the post type** (see table below). Usually it's obvious from the request. If it genuinely isn't, fold the question into step 1.
3. **Check facts that go stale.** If the post names library versions, API signatures, CLI flags, or pricing, search before writing. A confidently wrong 버전 번호 is the fastest way to lose a reader.
4. **Write the draft** following the 말투 and structure rules below.
5. **Run the 마지막 점검 checklist** before saving. This is not optional — it's where most of the quality comes from.
6. **Save to `/mnt/user-data/outputs/`** and present the file.

### 재료 확인

Ask before drafting, always — a post built from the writer's own notes, logs, and code reads completely differently from one assembled out of general knowledge. Without the ask, the result is a competent article about the topic instead of a post about what actually happened to them.

Ask once, keep it short, and name the specific things that would help for this post type:

- 트러블슈팅 → 에러 메시지 원문, 실제로 고친 코드(before/after), 처음에 뭘 의심했는지
- 개념 정리 / 튜토리얼 → 참고한 문서 링크, 직접 돌려본 예제 코드, 특히 헷갈렸던 지점
- 회고 → 한 주 동안의 메모, 커밋 로그, PR 목록, 그때 느낀 것
- 구현기 → 최종 코드, 스크린샷, 중간에 갈아엎은 설계

Two things not to get wrong:

- **If the material is already in the conversation, don't ask from scratch.** When the user just finished debugging something with you and says "이거 글로 써줘", the 재료 is right there. Say what you're planning to build the post from and ask whether there's anything to add or correct — then write. Asking blankly for material that's visible in the thread looks like you weren't paying attention.
- **Take "없다" for an answer.** If they have nothing, or just say 알아서 써줘, write the post from what you have. Don't ask twice and don't stall — a draft they can react to is worth more than another round of questions.

Once the material is in hand, write the whole post. Don't outline first and ask for approval unless they asked for an outline — they asked for a post.

### 재료가 얇을 때

받은 게 두세 줄뿐일 때가 있다. 선택지는 둘이고, 지어내는 건 어느 쪽도 아니다.

1. **유형을 낮춘다.** 500자짜리 재료로 3,000자 튜토리얼을 쓰면 나머지 2,500자는 전부 어디서나 볼 수 있는 일반론이 된다. 짧은 팁으로 쓰는 게 낫다.
2. **검색해서 채운다.** 주제에 맞는 공식 문서, 릴리스 노트, 이슈, 믿을 만한 글을 찾아 빈 곳을 메우고, 찾은 것을 `## 참고` 섹션에 남긴다.

보통은 둘을 같이 쓴다 — 분량 기대치를 한 단계 낮추고, 남는 빈틈을 검색으로 메운다.

검색해서 채울 때 지킬 것:

- **실제로 열어본 페이지만 링크한다.** 그럴듯해 보이는 URL을 지어내지 않는다. 죽은 링크 하나가 글 전체의 신뢰를 깎는다.
- **내가 겪은 것과 문서에서 읽은 것을 섞지 않는다.** "공식 문서에는 ~라고 나와 있다"처럼 문장 안에서 출처를 밝힌다. 안 해본 걸 해본 것처럼 쓰면 독자는 금방 알아챈다. 개인 블로그에서 이건 치명적이다.
- **원문을 옮기지 않는다.** 읽고 한다체로 다시 쓴다.
- **버전이 걸린 내용은 기준 버전을 적는다.**

`## 참고` 섹션은 이렇게 쓴다:

````markdown
## 참고

- [React 공식 문서 – useEffect](https://...) — 의존성 배열을 어떻게 비교하는지 나와 있다
- [관련 이슈 #12345](https://...) — 같은 증상 보고와 메인테이너 답변
````

링크만 나열하지 않는다. 뒤에 한 줄로 뭐가 들어 있는지 적어야 반년 뒤에 어느 걸 열지 고를 수 있다.

## Post types and length

Length follows the type, not a fixed target. Pick the row that matches and stay roughly in range.

| 유형 | 분량 | 뼈대 |
|---|---|---|
| 트러블슈팅 | 1,500~2,500자 | 왜 → 어떻게 → 무엇을 (아래 참고) |
| 개념 정리 / 학습 노트 | 2,500~4,000자 | 왜 알아야 하는지 → 개념 → 예제 → 헷갈리는 지점 |
| 구현기 / 튜토리얼 | 3,000~5,000자 | 목표 → 준비물 → 단계별 구현 → 결과 → 아쉬운 점 |
| 회고 | 800~2,000자 | 한 일 → 잘된 것 / 아쉬운 것 → 다음 |
| 짧은 팁 | ~800자 | 문제 → 해결 → 주의사항 |

## 직접 해결한 문제를 쓸 때: 왜 → 어떻게 → 무엇을

사용자가 겪고 고친 문제를 다루는 글이면 이 순서를 뼈대로 쓴다.

- **왜** — 무엇이 문제였고 왜 고쳐야 했나. 증상, 영향, 원인을 찾아간 과정이 전부 여기 들어간다. 처음에 뭘 의심했다가 틀렸는지도 여기다. 삽질 과정을 지우면 공식 문서와 다를 게 없어진다.
- **어떻게** — 어떻게 고쳤나. 실제 코드와 설정, before/after. 왜 이 방법을 골랐는지 한 줄.
- **무엇을** — 무엇이 달라졌고 무엇을 배웠나. 숫자가 있으면 숫자로. 아직 못 푼 문제도 여기 적는다.

이 순서를 지키는 이유는 검색으로 들어오는 독자 때문이다. 해결책부터 쓰면 자기 증상이 같은 문제인지 확인할 방법이 없다. 증상과 원인이 먼저 나와야 "이 글이 내 문제구나" 하고 읽기 시작한다.

소제목은 `## 왜` 같은 라벨 대신 내용을 담되 순서는 지킨다 — `빌드가 11분이 된 이유` → `캐시 키를 바꾼 방법` → `4분으로 돌아오고 남은 것`.

## 말투

기본은 **한다체**다. 격식 차린 논문투가 아니라 편하게 쓰는 한다체이고, 한 편 안에서 일관되게 유지한다.

- 종결어미: `-다`, `-이다`, `-했다`, `-한다`, `-된다`
- 딱딱해지지 않게 가끔 구어체를 섞는다: `-더라`, `-거든`, `-지`
- 1인칭은 `나`다. `저는`은 쓰지 않는다. 그리고 대부분은 아예 빼는 게 자연스럽다.
- 인용문이나 에러 메시지 원문은 그대로 둔다. 말투를 맞추려고 고치지 않는다.
- `-습니다`나 `-해요`로 새지 않게 한다. 특히 글 후반부와 마무리 문단에서 잘 샌다.

### 번역투 걷어내기

기계가 쓴 한국어의 가장 큰 특징이다. 아래 패턴은 초고에서 거의 항상 나오니까 퇴고할 때 찾아서 고친다.

| 이렇게 쓰기 쉬운데 | 이렇게 고친다 |
|---|---|
| ~에 대해서 알아보겠습니다 | ~를 정리해본다 |
| 성능 향상을 통해 | 성능이 좋아져서 |
| 장점을 가지고 있다 | 장점이 있다 |
| 사용하는 것이 가능하다 | 쓸 수 있다 |
| 생각되어진다 / 구현되어져 있다 | 생각한다 / 구현돼 있다 |
| 그것은 캐시 문제였다 | 캐시 문제였다 |
| 나는 ~했고, 나는 ~했다 | 주어를 뺀다 |

한국어는 주어와 대명사를 잘 생략한다. `나는`이 문단마다 나오면 번역기 냄새가 난다.

### 피할 표현

- `여러분` — 개발 블로그에서 잘 안 쓴다. 독자를 부를 일이 있으면 그냥 안 불러도 된다.
- `~인 것 같다`를 확신 없는 곳마다 붙이기 — 모르면 "확인 못 했다"라고 쓰는 게 낫다.
- `결론적으로`, `종합해보면` 같은 접속 상투구
- 이모지 — 안 쓰는 게 기본이다. 쓰더라도 글 전체에 한두 개.
- `안녕하세요! 오늘은 ~에 대해 알아보겠습니다` 식의 인사 도입부

## 구조

### frontmatter

GitHub 블로그(Jekyll/Hugo)를 쓴다면 이 형태로 시작한다:

```markdown
---
title: "제목"
date: 2026-08-18
topic: 프론트엔드
tags: [react, 성능최적화]
description: "한 줄 요약"
---
```

`topic`은 글이 속한 큰 분류 하나다. `tags`와 역할이 다르다 — 태그는 여러 개 붙는 키워드고, topic은 글 하나당 하나다. 분류로 묶어서 보여주려면 값이 글마다 일관돼야 하니까, 쓰던 값이 있으면 새로 만들지 말고 그대로 쓴다. (프론트엔드 / 백엔드 / 인프라 / 회고 정도의 굵기가 적당하다.)

velog는 에디터에서 제목과 태그를 따로 입력하니까, frontmatter는 참고용으로 남겨두고 본문만 복사해서 붙이면 된다고 알려준다.

### 본문

- **도입 (2~4문장)**: 인사 대신 상황으로 시작한다. "빌드가 갑자기 4분에서 11분으로 늘었다." 같은 문장 하나가 인사말 세 줄보다 낫다. 이 글에서 뭘 다루는지 도입 안에서 분명해야 한다.
- **본문**: `##`로 나눈다. `###`는 정말 필요할 때만. 소제목은 `1. 개요` 같은 라벨 말고 내용을 담는다 — `왜 캐시가 안 먹혔나`처럼.
- **마무리**: 요약 반복이 아니라 남은 것을 쓴다. 배운 점 한두 줄, 아직 못 푼 문제, 다음에 볼 것. `도움이 되셨으면 좋겠다`로 반사적으로 닫지 않는다.
- **참고 링크**: 실제로 본 문서만. 없으면 섹션 자체를 뺀다. 재료가 얇아서 검색으로 채웠다면 여기가 필수다 (위 '재료가 얇을 때' 참고).

문단 길이를 섞는다. 전부 세 문장짜리면 리듬이 죽는다. 한 문장짜리 문단도 써도 된다.

리스트는 진짜 나열일 때만 쓴다. 설명을 불릿으로 쪼개면 읽기 편해 보이지만 논리 연결이 사라진다.

### 줄 간격

새 섹션이 시작하는 `##` 앞에는 빈 줄을 넣는다. 앞 문단에 바로 붙여 쓰면 raw 마크다운에서 섹션 경계가 안 보여서 나중에 고쳐 쓸 때 불편하고, 에디터에 따라 헤딩으로 렌더링되지 않는 경우도 있다. 소제목 뒤에도 빈 줄을 하나 둔다.

````markdown
이전 문단의 마지막 문장이다.

## 새 섹션

새 섹션의 첫 문장이다.
````

코드 블록, 표, 리스트도 앞뒤로 빈 줄을 둔다. 리스트 항목 안에 코드 블록을 넣을 때 빈 줄이 없으면 렌더링이 깨진다.

빈 줄은 하나면 충분하다. 두 줄 이상 넣어도 렌더링 결과는 같고 raw 파일만 늘어진다.

## 코드 블록

- 언어 태그를 꼭 붙인다 (```js, ```python, ```bash)
- 파일 경로는 첫 줄 주석으로: `// src/hooks/useDebounce.ts`
- 한 블록에 20줄 넘어가면 자르거나 핵심만 남긴다. 전체 파일 붙여넣기는 안 읽힌다.
- 바꾼 부분이 핵심이면 before/after 두 블록으로 보여주고, 무엇이 달라졌는지 한 줄로 짚는다.
- 에러 메시지는 원문 그대로 블록에 넣는다 — 같은 에러로 검색해서 들어오는 사람이 있다.

## 파일 저장

`/mnt/user-data/outputs/`에 저장한다.

- GitHub 블로그(Jekyll): `YYYY-MM-DD-english-slug.md` — Jekyll은 이 형식을 요구한다
- 그 외: `english-slug.md`

슬러그는 영문 소문자와 하이픈으로 만든다. 한글 파일명은 배포 환경에 따라 깨진다.

## 마지막 점검

저장 전에 초고를 다시 읽으면서 확인한다:

- [ ] 한다체가 끝까지 유지됐나 (후반부 `-습니다`, `-해요` 확인)
- [ ] 위 번역투 표 패턴이 남아 있나
- [ ] `나는`, `그것은`이 몇 번 나오나 — 빼도 되는 건 뺀다
- [ ] 문제 해결 글이면 왜 → 어떻게 → 무엇을 순서인가
- [ ] 도입부가 인사말로 시작하지 않나
- [ ] 소제목이 내용을 담고 있나
- [ ] 모든 문단이 비슷한 길이는 아닌가
- [ ] `##` 앞뒤에 빈 줄이 있나
- [ ] 코드 블록에 언어 태그가 있나
- [ ] 확인 안 한 버전 번호나 API를 단정적으로 쓰지 않았나
- [ ] 검색으로 채운 부분이 있다면 출처를 문장 안에서 밝혔나
- [ ] 참고 섹션의 링크를 전부 실제로 열어봤나
- [ ] 분량이 유형 범위 안에 있나

## 예시

**Input:** "webpack 빌드 느려진 거 고친 거 블로그 글로 써줘"

**Output (도입부):**

````markdown
빌드가 갑자기 느려졌다. 4분이면 끝나던 게 11분이 됐고, 그 주에 웹팩 설정을 건드린 사람은 없었다.

처음엔 CI 러너 문제라고 생각했다. 로컬에서 돌려보니 거기서도 느렸고.
````

인사말 없이 상황으로 열고, 첫 의심이 틀렸다는 걸 바로 보여준다. 이 두 문단이 "오늘은 웹팩 빌드 최적화에 대해 알아보겠습니다"보다 훨씬 잘 읽힌다.
