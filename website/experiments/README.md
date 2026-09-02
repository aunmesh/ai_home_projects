# Experiments

Small, timeboxed tests that answer one question before we commit to building
it properly in `chores-assistant/`. An experiment is not a feature — it's how
we decide whether an idea survives contact with our actual kitchen.

## Convention

Each experiment gets its own numbered folder:

```
experiments/
  NNN-short-slug/
    README.md
```

- `NNN` — three-digit, zero-padded, always increasing. Never reused, even if
  an experiment is abandoned.
- `short-slug` — a few kebab-case words naming what's being tested, not the
  project ("baseline-clutter-signal", not "vision-stuff").
- Each `README.md` follows `TEMPLATE.md` — question, method, result, verdict.
  That's also the raw material for the blog post / video, so write it like
  someone else will read it.

Photos, model weights, and other captured data stay out of git (see the repo
`.gitignore`) — only the write-up and any small code snippets get committed.

## Log

| # | Experiment | Verdict |
|---|------------|---------|
| [001](./001-baseline-clutter-signal/README.md) | Can a stock vision model tell clutter from normal? | In progress |
