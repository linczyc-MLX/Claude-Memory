# Topic: BYT (Build Your Team)

> **Status**: Active Development | **Projects**: N4S | **Last Updated**: 2026-02-27

---

## What This Topic Covers

The BYT module in N4S — consultant matching, RFQ questionnaire, scoring, synergy analysis, and team assembly. Includes the RFQ Portal (separate VPS apps) and Library functionality.

---

## Current State (as of Feb 25, 2026)

### What's Working
- All 7 BYT tabs functional: Registry, Discovery, Shortlist, Matchmaking, Synergy Sandbox, Library, Admin
- All 4 test consultants (Ehrlich Yanai, Cliff Fong, Premier Dev, Mayfair Construction) have submitted RFQs
- Individual scores computed: Ehrlich 61, Cliff Fong 55, Premier 68, Mayfair 69
- Synergy Sandbox live with saved config "Team Thornwood Alpha" (score: 73/100)
- Library tab dual-view working (Project Responses + Consultant Library)
- BYT Admin Panel config system (global + project-level)

### Known Issues
- **ITR-11**: Library "Shortlist" button not greying out — FIXED 2026-02-22
- **ITR-13**: BYT Documentation PDF missing (N4S-BYT-Documentation.pdf)
- **ITR-10**: Need full test of Synergy Sandbox reading Section 4 RFQ responses
- Compare Mode in Synergy Sandbox: state vars exist but not wired

### Recent Commits
```
ea726556 Add expandable detail view to saved Synergy configurations
a91d836d Fix Synergy Sandbox crash on save: handle JSONB already-parsed objects
b5efd130 Fix Synergy Sandbox: use activeProjectId from context
81b45e21 fix(shortlist): Send RFQ button now reflects actual invitation status
ee4d94e6 BYT Matchmaking: discipline-aware sub-metric display + v3 support
```

### Last Working Session Issue
The Library screen Shortlist button fix was documented in `CLAUDE-CODE-HANDOVER.md` (now superseded by this file). Root cause: API_BASE was empty string on website.not-4.sale, so engagement fetch hit /gid.php (404) instead of /api/gid.php.

---

## Key References (in N4S repo)

- Module docs: `docs/memory/modules/BYT.md` — full tab structure, files, DB tables, API endpoints
- ITR items: `docs/memory/itr/ITR-MASTER.md` — open issues tagged BYT
- Architecture: `docs/memory/ARCHITECTURE.md` — hosting, tech stack, data flow

---

## Suggested Next Steps

1. **Compare Mode** — Wire Synergy Sandbox multi-select comparison (state vars exist)
2. **Export Brief** — Wire Synergy results into Export Brief tab
3. **ITR-13** — Generate BYT Documentation PDF using ReportLab
4. **ITR-10** — Verify Synergy Sandbox reads Section 4 correctly for all candidates

---

*Updated by session close-out protocol. See PROTOCOL.md.*
