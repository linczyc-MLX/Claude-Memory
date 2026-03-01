# Start Session

Load universal memory from this repo, then prepare for work.

## Usage
```
/start-session {TOPIC}    — load a specific topic (BYT, PARKER, BRAND, PDF, etc.)
/start-session            — load universal memory only, list available topics
```

## Steps — Execute ALL, no confirmation prompts

### 1. Read Universal Memory (ALWAYS — in this exact order)
You're already in the Claude-Memory repo. Read these files:
1. `UNIVERSAL.md` — owner preferences, working style, ecosystem overview
2. `PROTOCOL.md` — session start/end rules
3. `REPOS.md` — all repos, URLs, access details

### 2. If NO topic was specified:
List all available topics by reading the `topics/` directory:
```bash
ls topics/
```
Print:
```
✓ Universal memory loaded

Available topics:
  - BYT    — Build Your Team module (N4S)
  - PARKER — Parker AI advisor (N4S + Luxebrief)
  - BRAND  — Universal brand guidelines (N4S + Luxebrief)
  - PDF    — PDF generation & reports (N4S + Luxebrief)
  {any other .md files found in topics/}

To start with a topic: /start-session {TOPIC}
Or describe what you'd like to work on and I'll pick the right topic (or create a new one).
```
Then STOP here — wait for Michael to choose.

### 3. If a topic WAS specified:

#### 3a. Read Topic Handover
- Read `topics/{TOPIC}.md`
- This contains: what was done last session, current state, suggested next steps

#### 3b. Read Project State
- From the topic file, identify which projects are involved (N4S, Luxebrief, or both)
- Read `projects/{PROJECT}.md` for each

#### 3c. Clone or Update Project Repos
For each relevant project repo, clone if missing or pull latest if already cloned:
```bash
# N4S
if [ -d /tmp/n4s ]; then cd /tmp/n4s && git pull; else git clone https://github.com/linczyc-MLX/N4S.git /tmp/n4s; fi

# Luxebrief (only if topic requires it)
if [ -d /tmp/luxebrief ]; then cd /tmp/luxebrief && git pull; else git clone https://github.com/linczyc-MLX/Luxebrief.git /tmp/luxebrief; fi
```
If clone fails, retry with `git -c http.proxyAuthMethod=basic clone`.

#### 3d. Read Project Context
- Read `CLAUDE.md` in each cloned project repo
- For N4S: also read `docs/memory/ARCHITECTURE.md` and `docs/memory/HANDOVER.md`
- If relevant, read `docs/memory/modules/{MODULE}.md` for the specific module being worked on

#### 3e. Print Status Summary
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
- **Universal memory is ALWAYS loaded** — even without a topic, preferences and working rules apply
