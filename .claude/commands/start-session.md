# Start Session

Load universal memory from this repo, then clone and prepare project repos for work.

## Usage
```
/start-session {TOPIC}
```
- `{TOPIC}`: BYT, PARKER, BRAND, or any topic file in topics/

## Steps — Execute ALL, no confirmation prompts

### 1. Read Memory Files (in this exact order)
You're already in the Claude-Memory repo. Read these files:
1. `UNIVERSAL.md` — owner preferences, working style, ecosystem overview
2. `PROTOCOL.md` — session start/end rules
3. `REPOS.md` — all repos, URLs, access details

### 2. Read Topic Handover
- Read `topics/{TOPIC}.md`
- This contains: what was done last session, current state, suggested next steps

### 3. Read Project State
- From the topic file, identify which projects are involved (N4S, Luxebrief, or both)
- Read `projects/{PROJECT}.md` for each

### 4. Clone Project Repos
Clone each relevant project repo:
```bash
git clone https://github.com/linczyc-MLX/N4S.git /tmp/n4s
git clone https://github.com/linczyc-MLX/Luxebrief.git /tmp/luxebrief
```
If clone fails, retry with `git -c http.proxyAuthMethod=basic clone`.

### 5. Read Project Context
- Read `CLAUDE.md` in each cloned project repo
- For N4S: also read `docs/memory/ARCHITECTURE.md` and `docs/memory/HANDOVER.md`
- If relevant, read `docs/memory/modules/{MODULE}.md` for the specific module being worked on

### 6. Print Status Summary
```
✓ Memory loaded (Claude-Memory repo)
✓ Topic: {TOPIC}
✓ Projects: {list}
✓ Last session: {date} — {summary from topic file}
✓ Suggested next steps:
  1. {step}
  2. {step}
```

## Critical Rules
- **ALL memory lives in THIS GitHub repo** — never in ~/.claude/projects/ or local files
- **Read before writing** — always load all memory files before starting any work
- **Do not ask for confirmation** between steps — run the entire sequence silently
