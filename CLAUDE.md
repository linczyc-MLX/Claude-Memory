# Claude Memory — Not4Sale Ecosystem

> **This repo is the canonical memory hub for all Claude sessions working on the Not4Sale ecosystem.**

## On Session Start

1. Read `UNIVERSAL.md` — preferences, working style, tools
2. Read `PROTOCOL.md` — session start/end commands and rules
3. Read `REPOS.md` — which repos exist, how to access them
4. Read `topics/{TOPIC}.md` — if a topic was specified
5. Read `projects/{PROJECT}.md` — for each relevant project

## On Session End

Follow the "Save and Hand Off" procedure in `PROTOCOL.md`.

## Structure

```
├── UNIVERSAL.md        ← Always read. Preferences, tools, working style.
├── PROTOCOL.md         ← Session commands and rules.
├── REPOS.md            ← All repos, URLs, access tokens, purpose.
├── CREDENTIALS.md      ← Where to find credentials (no secrets stored here).
├── BRAND-GUIDE.md      ← Universal Not4Sale brand guide (N4S + Luxebrief).
├── topics/             ← Topic-specific handover state.
│   ├── BYT.md
│   ├── PARKER.md
│   ├── BRAND.md
│   └── {new-topics}.md
└── projects/           ← Project-level state (deploy, git, cross-project).
    ├── N4S.md
    └── LUXEBRIEF.md
```

## Rules

- **UNIVERSAL.md is always loaded** — every session, every model, every interface.
- **Topic files are the handover** — they replace HANDOVER.md files scattered in repos.
- **Project files track deploy/git state** — not session-by-session logs.
- **No secrets in this repo** — CREDENTIALS.md has pointers only.
- **This repo must be private** — it contains project state and architectural context.
