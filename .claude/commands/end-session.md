# End Session (Save and Hand Off)

Save session state to this repo and push all changes.

## Usage
```
/end-session {TOPIC}
```
- `{TOPIC}`: BYT, PARKER, BRAND, or any topic file in topics/

## Steps — Execute ALL, no confirmation prompts

### 1. Update Topic File
Edit `topics/{TOPIC}.md` with:
- **What was done this session** — commits, decisions, changes made (with commit hashes)
- **Current state** — build/deploy status, where things stand
- **Blockers or warnings** — anything the next session needs to know
- **Suggested next steps** — prioritized list for the next session
- **Key files modified** — so the next session knows where to look
- Update the "Last Updated" date

### 2. Update Project State
Edit `projects/{PROJECT}.md` for each affected project:
- Current git branch and latest commit hash
- Deploy status (clean/broken/pending)
- Any cross-project implications

### 3. Update Universal (only if needed)
Edit `UNIVERSAL.md` ONLY if:
- Preferences or working style changed
- New topics were created
- Ecosystem-level facts changed (new repos, new services, etc.)

### 4. Commit and Push This Repo
```bash
git add -A
git commit -m "Session close: {TOPIC} — {one-line summary of what was done}"
git push origin main
```

### 5. Commit and Push Project Repos
If code was modified during the session, ensure all changes in the project repo(s) are committed and pushed:
```bash
cd /tmp/n4s  # or wherever the project repo was cloned
git add -A
git commit -m "{descriptive commit message}"
git push origin main
```

### 6. Print Handover Summary
```
── Session Complete ──────────────────
Topic: {TOPIC}
Date: {today}

Commits:
  claude-memory: {hash} — {message}
  N4S: {hash} — {message} (if applicable)
  Luxebrief: {hash} — {message} (if applicable)

Deploy: {status for each affected service}

To continue next session:
> /start-session {TOPIC}
──────────────────────────────────────
```

## Critical Rules
- **ALL session state goes to THIS GitHub repo** — never to ~/.claude/projects/ or local files
- **Topic file is the single source of truth** for "what happened" and "what's next"
- **Keep topic files concise** — 1-2 pages max. Move historical detail to SESSION-LOG.md in the project repo if needed
- **Do not ask for confirmation** between steps — run the entire sequence, report at end
