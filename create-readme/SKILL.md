---
name: create-readme
description: Create or rewrite a project's README.md — a well-structured, appealing README with a proper header, overview, getting-started and usage sections. Use this skill whenever the user asks for a readme, mentions "readme", "readme.md", "document my project", "docs for this repo", or asks to explain or introduce their project to other people. Also use it when the user asks to improve, expand, or update an existing README, or when a project is finished and needs documentation before being shared or published — even if they never say the word "readme".
---

# Create README

## Role

You're a senior software engineer with extensive open source experience. The READMEs you write are appealing, informative, and easy to read — a reader should understand what the project is within one screen, and be running it within five minutes.

## Workflow

### 1. Review the project

Read the workspace before writing anything. Look at:

- `package.json` / `pyproject.toml` / `Cargo.toml` / `go.mod` — name, description, scripts, dependencies, entry points
- Existing `README.md`, `docs/`, `.env.example`, `Dockerfile`, CI workflows
- The source tree — top-level folders, what each package or module does
- `assets/`, `docs/images/`, `public/` — a logo or icon to use in the header

### 2. Ask the gaps

The code tells you *what* the project is. It doesn't tell you the rest. Ask the user in one batch — not a drip feed — about whatever you couldn't determine:

1. **The pitch** — one sentence on what it does and who it's for.
2. **Audience** — public/open source, internal team, or personal. Sets the tone.
3. **Verification** — confirm the install and run commands you inferred are actually correct.
4. **Environment** — env vars, API keys, external services needed to run it.
5. **Links** — repo URL, docs site, live demo.
6. **Demo image** — if you found no screenshot or GIF in the repo, ask the user to add one. Tell them the exact path to drop it at (`docs/images/demo.gif`) and what it should show: the main flow in a few seconds, or one screenshot of the primary screen. A README with a demo converts far better than one without, so ask directly rather than skipping it.

> [!IMPORTANT]
> Never invent facts. No made-up badge, URL, author, version, or command. If something is unknown and the user won't answer, write `TODO:` — a README with honest gaps beats one with commands that don't work.

### 3. Create the missing logo

Look for an existing logo or banner first: `assets/`, `docs/images/`, `public/`, `.github/`, any favicon, or an image in the current README.

**If there isn't one, create it.** Don't ask permission and don't skip the header image — write an SVG to `docs/images/logo.svg` and reference it from the README.

Design rules:

- **Derive the mark from the project.** What it does, or its initials. A terminal prompt for a CLI, a plug for a connector, a stacked layer for a build tool. Simple geometry — circles, arcs, rounded rects, a single path.
- **Legible at 64px.** No fine detail, no thin hairlines, no more than a handful of shapes.
- **Works on light and dark.** GitHub renders README on both. Avoid pure `#000` or `#fff` fills; pick mid-tone colors that hold up against either background. Test by imagining it on `#0d1117` and `#ffffff`.
- **Two colors plus a neutral, maximum.** A flat palette reads as intentional; a gradient mesh reads as clip art.
- **`viewBox="0 0 64 64"`** for a square mark, or `0 0 1280 320` for a wide banner. Banners suit public flagship projects; a square mark is the safe default.
- **No brand imitation.** Never reproduce or closely riff on an existing company's logo, and don't reference webfonts — GitHub won't load them. Keep text minimal, or leave the wordmark to the `# Heading` and let the SVG be a pure mark.

Tell the user you generated it, where it lives, and that it's easy to swap out.

### 4. Write it

Write to `README.md` in the project root, following the structure below.

## Structure

Model the layout on these projects — fetch them if you need a closer look at the conventions:

- https://raw.githubusercontent.com/Azure-Samples/serverless-chat-langchainjs/refs/heads/main/README.md
- https://raw.githubusercontent.com/Azure-Samples/serverless-recipes-javascript/refs/heads/main/README.md
- https://raw.githubusercontent.com/sinedied/run-on-output/refs/heads/main/README.md
- https://raw.githubusercontent.com/sinedied/smoke/refs/heads/main/README.md

### Header

For larger projects, a centered block: logo (if one exists, ~64px), title, badge row, one-line tagline, section nav links, demo image or GIF.

````markdown
<div align="center">

<img src="./docs/images/logo.png" alt="" height="64" />

# Project Name

[![Build](badge-url)](link) [![npm](badge-url)](link) [![License](badge-url)](link)

> One-line description of what this does

[Overview](#overview) • [Getting started](#getting-started) • [Usage](#usage)

![Demo](./docs/images/demo.gif)

</div>
````

For small libraries and CLI tools, drop the `<div>` and keep it flat: title, badges, blockquote tagline. Only include badges that correspond to something real — a CI workflow that exists, a package that's actually published.

If the user hasn't supplied a demo image yet, don't ship a broken `<img>`. Leave a commented placeholder at the exact spot so they can drop the file in and delete two lines:

````markdown
<!-- Add a demo GIF or screenshot at docs/images/demo.gif, then uncomment:
![Demo](./docs/images/demo.gif)
-->
````

### Body sections

| Section | Content | Include when |
|---|---|---|
| Intro paragraph | What it is, built with what (link the technologies) | Always |
| Quick example | Smallest possible working example, right up front | CLIs, libraries |
| Overview | Why it exists, architecture, components and their folders | Non-trivial projects |
| Features | Bulleted, `**Bold lead-in**: explanation` | Always |
| Getting started | Prerequisites as a linked list, then install steps | Always |
| Usage | Real commands with real arguments, CLI options, config | Always |
| Deployment | Deploy steps, cleanup | Web apps and services |
| Troubleshooting | Common failures, or a link to `docs/` | Common failure modes exist |
| Resources | Links to related docs and projects | Public projects |

> [!NOTE]
> Do not write `License`, `Contributing`, `Changelog`, or `Code of Conduct` sections. Those live in their own files. Linking to them from a badge is fine.

## Style rules

- **GFM throughout** — tables, task lists, fenced blocks with language tags, relative links to files in the repo.
- **GitHub admonitions** where they earn their place: `> [!NOTE]`, `> [!TIP]`, `> [!IMPORTANT]`, `> [!WARNING]`, `> [!CAUTION]`. Use them for the cost warning, the "you can run this free locally" tip, the step people always get wrong. Two or three in a README, not ten.
- **Emojis sparingly.** A leading emoji in the title is fine. Not one per heading.
- **Concise.** Roughly 80–200 lines. Anything longer goes in `docs/` with a link.
- **Commands over prose.** Show the fenced block, don't describe it in a sentence. Every command should work as written from a fresh clone.
- **Concrete examples.** Real invocations with real-looking arguments and expected output — not `foo bar baz`.
- **Second person, present tense.** "Run the migrations", not "the migrations should then be run."
- **No filler.** Skip "this project aims to leverage cutting-edge technologies". State what it does.

## Rewriting an existing README

Read it first. Keep what's accurate — especially the project description, which the author knows better than you do. Fix structure, stale commands, dead links, and missing getting-started steps. Tell the user what you changed rather than silently replacing their words.
