# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A two-person project (Asim & Ishita) building small, opinionated home-AI
experiments and writing them up. Two things live side by side under
`website/`:

- **`website/site/`** — the public marketing/blog site (static HTML, no
  build step), deployed to Netlify at `https://aihomeprojects.netlify.app`.
- **`website/chores-assistant/`** and **`website/experiments/`** — the
  actual project work: a home clutter-detection assistant, developed as a
  series of small numbered experiments before being built out into a real
  pipeline.

There is no application code yet (no package.json, no Python files) — the
site content and the experiment/pipeline scaffolding exist, but Project 01
itself is still pre-implementation.

## Commands

The site has no build step and no dependencies. To preview it locally:

```bash
cd website/site && python3 -m http.server 8000
# visit http://localhost:8000
```

There is currently no lint, test, or build tooling anywhere in this repo —
don't assume any exists when working here.

## Architecture

### Site (`website/site/`)

Three plain HTML files (`index.html`, `about.html`, `projects.html`), each
fully self-contained: the same design-token CSS (`:root` custom properties
for color/spacing/typography, plus shared `.btn`/`.card`/`.tag`/`.nav`
classes) is duplicated verbatim in a `<style>` block at the top of every
page rather than pulled from a shared stylesheet. **When changing shared
styling, the edit has to be made identically in all three files** — check
all of them, not just the one being worked on.

Deploy: Netlify's package/base directory is configured (in the Netlify
dashboard, not in this repo) to point at `website/site`. The folder was
previously named `aihomeprojects/` and was renamed to `website/` in a past
commit — if the site ever fails to deploy or serves stale content, check
that the Netlify dashboard setting still matches the current path.

### Project pipeline (`website/chores-assistant/`)

The clutter-detection assistant is designed as five sequential stages, each
mapped to its own build-log episode (documented in
`website/chores-assistant/README.md` and on `website/site/projects.html`):

```
capture -> detect -> judge -> compare -> notify
```

Hard rule baked into the design (not a settings toggle): captured frames
are processed and deleted on the machine that captured them. Only text
(labels, scores, task history) persists past that machine; notifications
never carry images.

### Experiments (`website/experiments/`)

Before a pipeline stage becomes real code in `chores-assistant/`, it gets
validated as a numbered experiment here:

```
experiments/
  NNN-short-slug/
    README.md   # question, method, data, result, verdict — follows TEMPLATE.md
```

Numbers are zero-padded, three digits, and never reused even if an
experiment is abandoned. Raw captured data (photos, model weights, etc.)
is never committed — see `.gitignore` in `website/` (media file extensions,
`captures/`, `frames/`, `.db`/`.sqlite3` are all excluded). Only the
write-up and small code snippets are committed; that write-up doubles as
the source material for the eventual blog post / video.

## Git workflow

Never commit directly to `main`. Do all work on a branch (or a git
worktree) and merge/PR into `main` instead.
