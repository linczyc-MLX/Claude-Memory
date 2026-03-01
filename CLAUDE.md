# CLAUDE.md — Claude-Memory Repository

## ⚠️ THIS IS THE CANONICAL MEMORY HUB

**All Claude session memory for the Not4Sale ecosystem lives HERE — in this GitHub repo.**

- This repo is cloned at the start of every session (via `/start-session` or the "Read memory" prompt)
- Session state is saved back here at the end of every session (via `/end-session` or "Save and hand off")
- **NEVER save session memory to `~/.claude/projects/`** — that is local-only and invisible to other machines
- **NEVER save session memory to local disk, Dropbox, or any path outside this repo**
- If Claude Code, CLI, or any Claude interface tries to save memory locally, redirect it here

## Structure

```
├── UNIVERSAL.md        ← Always loaded. Preferences, tools, working style.
├── PROTOCOL.md         ← Session start/end commands and rules.
├── REPOS.md            ← All repos, URLs, access details.
├── CREDENTIALS.md      ← Where to find credentials (no secrets stored here).
├── BRAND-GUIDE.md      ← Universal Not4Sale brand guide.
├── topics/             ← Topic-specific handover state (BYT, PARKER, BRAND, etc.)
├── projects/           ← Project-level state (N4S, LUXEBRIEF — git/deploy status)
└── .claude/commands/   ← Slash commands for session start/end
```

## Session Commands

- **`/start-session {TOPIC}`** — Clone this repo, read memory files in order, clone project repos, print status
- **`/end-session {TOPIC}`** — Update topic + project files, commit and push this repo, print handover

## Rules

1. **UNIVERSAL.md is always loaded** — every session, every model, every interface
2. **Topic files are the handover** — they replace scattered HANDOVER.md files in project repos
3. **Project files track state, not history** — current git branch, deploy status, cross-project notes
4. **No secrets in this repo** — CREDENTIALS.md has pointers only
5. **This repo is public** — do not add API keys, tokens, passwords, or sensitive client data
