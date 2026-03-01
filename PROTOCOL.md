# Session Protocol — Not4Sale Claude Sessions

> **Purpose**: Defines the exact commands, steps, and rules for starting and ending Claude sessions.
> **Location**: `claude-memory/PROTOCOL.md` (canonical — no other PROTOCOL.md is authoritative)
> **Last Updated**: 2026-02-27

---

## Session Start Commands

### `Claude: Read memory and hand off Topic: {TOPIC}`

Use this at the start of any working session. Replace `{TOPIC}` with: BYT, PARKER, BRAND, or any topic file that exists in `topics/`.

**What Claude does:**

1. **Clone `claude-memory`** repo
2. **Read `UNIVERSAL.md`** — load owner preferences, working style, tools, ecosystem context
3. **Read this file (`PROTOCOL.md`)** — understand session rules
4. **Read `REPOS.md`** — know which repos exist and how to access them
5. **Read `topics/{TOPIC}.md`** — load the topic-specific handover (what was done last, current state, next steps)
6. **Identify relevant projects** from the topic file → read `projects/{PROJECT}.md` for each
7. **Clone relevant project repos** (N4S, Luxebrief, or both — based on what the topic requires)
8. **Read each repo's `CLAUDE.md`** — load project-specific technical context
9. **Print a status summary**:
   ```
   ✓ Memory loaded
   ✓ Topic: {TOPIC}
   ✓ Projects: {list}
   ✓ Last session: {date} — {summary}
   ✓ Suggested next steps:
     1. {step}
     2. {step}
   ```

### `Claude: Read memory`

Use this when starting a session **without a specific topic** — general questions, new topic exploration, or cross-cutting work.

**What Claude does:**

1. Clone `claude-memory` repo
2. Read `UNIVERSAL.md`
3. Read `PROTOCOL.md`
4. Read `REPOS.md`
5. Print available topics and their status
6. Ask what you'd like to work on

---

## Session End Commands

### `Claude: Save and hand off Topic: {TOPIC}`

Use this at the end of any working session. Triggers the full close-out sequence.

**What Claude does:**

1. **Update `topics/{TOPIC}.md`** in claude-memory:
   - What was done this session (commits, decisions, changes made)
   - Current state (build/deploy status, where things stand)
   - Blockers or warnings
   - Suggested next steps for the next session
   - Key files modified this session

2. **Update `projects/{PROJECT}.md`** for each affected project:
   - Current git state (branch, latest commit hash)
   - Deploy status
   - Any cross-project implications

3. **Update `UNIVERSAL.md`** — only if preferences or ecosystem-level facts changed

4. **Commit and push `claude-memory`**:
   ```
   Session close: {TOPIC} — {one-line summary}
   ```

5. **Commit and push project repos** (N4S, Luxebrief) — if code was modified during the session

6. **Print a handover summary**:
   ```
   ── Session Complete ──
   Topic: {TOPIC}
   Commits: {list with hashes}
   Deploy: {status}

   To continue next session:
   > Claude: Read memory and hand off Topic: {TOPIC}
   ```

### `Claude: Save and hand off`

Use this when ending a session that **wasn't tied to a specific topic** or spanned multiple topics.

**What Claude does:**

Same as above, but:
- Updates all topic files that were touched
- Updates all affected project files
- Handover summary lists all topics worked on

---

## Rules

### Memory Files

1. **UNIVERSAL.md is always loaded.** Every session, every model (Claude Code, Cowork, claude.ai), every interface.

2. **Topic files are the handover.** They replace all other handover files (HANDOVER.md in repos, CLAUDE-CODE-HANDOVER.md, etc.). One file per topic, always current.

3. **Project files track state, not history.** Current git branch, latest commit, deploy status, cross-project notes. NOT session-by-session logs.

4. **Module-specific docs stay in their repos.** N4S `docs/memory/modules/*.md` and `docs/memory/ARCHITECTURE.md` are repo-specific reference material. They're read during sessions but NOT duplicated in claude-memory.

5. **ITR (Items To Resolve) stays in N4S.** `docs/memory/itr/ITR-MASTER.md` is N4S-specific and referenced from topic handovers when relevant.

### Code Work

6. **Never ask Michael to paste code.** Provide complete edited files, then push directly to GitHub after confirmation.

7. **Git-first.** All changes committed and pushed. GitHub Actions handles deployment.

8. **Both repos matter.** When investigating issues, always consider whether the fix needs to touch N4S, Luxebrief, or both. Read both CLAUDE.md files if unsure.

### Session Hygiene

9. **Read before writing.** Always load memory files before starting work. Don't rely on assumptions from previous sessions.

10. **One handover, one truth.** When closing a session, the topic file becomes the single source of truth for "what happened" and "what's next."

11. **Keep it current, keep it concise.** Topic files should be 1-2 pages max. If a topic file grows too large, split off historical content into SESSION-LOG.md in the project repo.

---

## Topic ↔ Project Mapping

| Topic | Primary Project | Secondary Project | Notes |
|-------|----------------|-------------------|-------|
| BYT | N4S | — | BYT module dev, RFQ Portal on VPS touches Luxebrief patterns |
| PARKER | N4S + Luxebrief | — | Parker exists in both apps with different personas |
| BRAND | N4S + Luxebrief | — | Universal brand guide covers both apps |
| INFRA | N4S + Luxebrief | — | VPS, deployment, database, CI/CD |
| UI | N4S | Luxebrief | UI refinements, usually module-specific |
| BESTRENTNJ | BestRentNJ | — | Personal project — township news tool for Ricky |

*Add new rows as new topics are created.*

---

## Creating a New Topic

When starting work on something that doesn't fit an existing topic:

1. Create `topics/{TOPIC-NAME}.md` with:
   ```markdown
   # Topic: {Name}
   > **Status**: New | **Created**: {date} | **Projects**: {list}

   ## Context
   {What this topic is about and why it exists}

   ## Current State
   {Starting point}

   ## Next Steps
   {What to do first}
   ```

2. Add the topic to the table in `UNIVERSAL.md`
3. Add the topic-project mapping to the table above

---

*This protocol is the canonical reference. If CLAUDE.md in a repo contradicts this, this file wins.*
