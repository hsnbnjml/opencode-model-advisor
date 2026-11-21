# OpenCode model advisor

A semi-automatic model advisor for OpenCode. It watches what kind of task you
are starting, and when your current model is a poor fit it suggests a better one
in a single line. It never switches models itself — you do, via `/models`.

Built for the free models on the `opencode` provider, but the rules are generic.

## How it works

| Step | Who |
| --- | --- |
| Detect the task category | automatic |
| Check which models are actually available | automatic |
| Name the better model | automatic |
| Switch | you, via `/models` |

It stays quiet when your current model is already a good fit. One suggestion per
category per session, and none after you say **stay**.

## Files

```
AGENTS.md        the advisor rules and the ranked model picks
opencode.jsonc   default model
.gitignore       keeps secrets out of git
```

`AGENTS.md` lives in the global config directory, so it applies to every
project. Project-level `AGENTS.md` files are added on top.

## Triggers

The advisor speaks up for: vision on a text-only model, audio/video, jobs that
exceed the context window, image generation, and heavy coding or reasoning on
the default model.

It stays silent for plain questions and small tasks.

## Refreshing

Say **"refresh models"**. The picks table is a ranking, not a fact sheet —
quality comes from the table, availability is checked live.

## Setup

Copy `AGENTS.md` and `opencode.jsonc` into your OpenCode config directory:

- Windows: `%USERPROFILE%\.config\opencode\`
- macOS / Linux: `~/.config/opencode/`

OpenCode picks up changes automatically; no restart needed.

## Warning

Never commit `service.json` — it contains a local service password. It is
already listed in `.gitignore`.
