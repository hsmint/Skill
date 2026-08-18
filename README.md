<div align="center">

<img src="./assets/images/logo.svg" alt="" height="64" />

# Skill

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)

> 글쓰기를 대신해주는 [Claude Code](https://claude.com/claude-code) 스킬 모음

[개요](#개요) • [스킬](#스킬) • [시작하기](#시작하기) • [사용법](#사용법)

<!-- 데모 GIF나 스크린샷을 docs/images/demo.gif 에 넣고 아래 두 줄의 주석을 풀면 된다:
![Demo](./docs/images/demo.gif)
-->

</div>

## 개요

사용자가 스킬을 직접 부르지 않아도, 요청이 `description` 에 걸리면 Claude가 알아서 불러온다.

| 디렉터리 | 스킬 이름 | 하는 일 |
|---|---|---|
| [`create-post/`](create-post/SKILL.md) | `blog-post` | 한국어 블로그 글을 `.md`로 쓴다 (velog / GitHub 블로그) |
| [`create-til/`](create-til/SKILL.md) | `til` | 오늘 배운 것을 `til-{topic}.md` 한 항목으로 남긴다 |
| [`create-readme/`](create-readme/SKILL.md) | `create-readme` | 프로젝트 `README.md`를 쓰거나 다시 쓴다 |


## 스킬
각 스킬들은 백지에서 쓰지 않는다. 대화에 이미 재료가 있으면 다시 묻지 않고, 무엇으로 쓸지 한 줄로 확인한 다음 바로 쓴다.

- **`blog-post` — 유형별로 분량과 뼈대가 다르다.** 트러블슈팅 1,500~2,500자, 개념 정리 2,500~4,000자, 회고 800~2,000자처럼 유형표를 먼저 고르고 그 범위 안에서 쓴다. 직접 해결한 문제는 왜 → 어떻게 → 무엇을 순서로 간다.
- **`til` — TIL은 짧은 블로그 글이 아니다.** 서론도 인사도 없이 500~800자로, 반년 뒤의 자신이 검색해서 찾을 노트를 쓴다.
- **`create-readme` — 로고까지 만든다.** 저장소에 로고가 없으면 `docs/images/logo.svg`를 직접 그려 넣고, 데모 이미지가 없으면 깨진 `<img>` 대신 주석 자리표시자를 남긴다.

## 시작하기

### 준비물

- [Claude Code](https://docs.claude.com/en/docs/claude-code/overview) — 설치되어 있어야 한다
- `git`

### 설치

스킬 디렉터리를 개인 스킬 경로(`~/.claude/skills/`)로 복사한다.

```bash
git clone git@github.com:hsmint/Skill.git
cd Skill
mkdir -p ~/.claude/skills
cp -R create-post create-til create-readme ~/.claude/skills/
```

저장소를 계속 손볼 거라면 복사 대신 심볼릭 링크를 건다. 여기서 고친 내용이 바로 반영된다.

```bash
mv "$PWD/create-post" ~/.claude/skills/create-post
mv "$PWD/create-til" ~/.claude/skills/create-til
mv "$PWD/create-readme" ~/.claude/skills/create-readme
```

특정 프로젝트에서만 쓰려면 `~/.claude/skills/` 대신 그 프로젝트의 `.claude/skills/`에 넣는다.

## 사용법

스킬 이름을 부르지 않아도 된다. 요청이 `description`에 걸리면 Claude가 알아서 고른다.

```text
> 오늘 웹팩 빌드 느려진 거 고친 거 블로그 글로 써줘
```

`blog-post`가 걸린다. 재료(맥락 / 처음 오해 / 에러 원문)를 먼저 묻고, 트러블슈팅 유형으로 1,500~2,500자를 쓴 다음 `english-slug.md`로 저장한다.

```text
> 방금 알아낸 거 til로 남겨줘
```

`til`이 걸린다. 방금 대화에 재료가 있으면 다시 묻지 않고, 주제 슬러그를 정해 `til-git-reflog.md`에 날짜 항목 하나를 덧붙인다.

```text
> README 파일 작성해줘
```

`create-readme`가 걸린다. 저장소를 먼저 읽고, 알 수 없는 부분(한 줄 소개, 실행 명령, 환경 변수, 링크)을 한 번에 물은 다음 `README.md`를 쓴다.

GitHub 블로그(Jekyll)에 올릴 글은 `YYYY-MM-DD-english-slug.md` 형식으로 저장된다. 슬러그는 영문 소문자와 하이픈만 쓴다 — 한글 파일명은 배포 환경에 따라 깨진다.

## 알아둘 것

> [!WARNING]
> `blog-post`와 `til`은 결과물을 `/mnt/user-data/outputs/`에 저장하도록 쓰여 있다. claude.ai 환경 경로라서 로컬 Claude Code에는 없다. 로컬에서 쓰려면 각 `SKILL.md`의 저장 경로 섹션(`## 파일 저장`, `## 파일 다루기`)을 원하는 경로로 바꿔야 한다.

`til`은 대화가 끝나면 이전에 쓴 파일을 찾아오지 못한다. 같은 주제로 전에 쓴 파일이 있으면 대화에 같이 올려주면 이어서 쓴다.
