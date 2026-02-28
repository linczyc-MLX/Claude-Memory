# Topic: BYT (Build Your Team)

> **Status**: Active Development | **Projects**: N4S | **Last Updated**: 2026-02-28

---

## What This Topic Covers

The BYT module in N4S — consultant matching, RFQ questionnaire, scoring, synergy analysis, and team assembly. Includes the RFQ Portal (separate VPS apps) and Library functionality.

---

## Current State (as of Feb 28, 2026)

### What's Working
- All 7 BYT tabs functional: AI Discovery, Import Queue, Registry Search, Shortlist, Matchmaking, Synergy Sandbox, Library, Admin
- Tab order corrected: AI Discovery → Import Queue → Registry Search (workflow-first order)
- Manual Search → AI Discovery criteria handoff: switching carries discipline, states, budget tier, style keywords
- JSON truncation fix: max_tokens increased to 16384 + JSON repair logic for truncated AI responses
- All 4 test consultants (Ehrlich Yanai, Cliff Fong, Premier Dev, Mayfair Construction) have submitted RFQs
- Synergy Sandbox verified: score 73 with 6 dimensions, 6 conflict nodes, 3 complementary signals
- Library tab dual-view working (Project Responses + Consultant Library)
- BYT Admin Panel config system (global + project-level)

### Known Issues
- **ITR-26 ⚡ PRIORITY**: PM/OR AI Discovery returns weak results — needs discipline-specific prompt engineering, exemplar firms, source-aware search instructions. Detailed research PDF analyzed. See `docs/memory/itr/ITR-MASTER.md`.
- **ITR-8**: PM/Owner's Rep Discovery data quality — registry only has 16 consultants (4 PM), all from AI imports. `gid_discovery_candidates` has 50 entries (14 PM).
- **ITR-13**: BYT Documentation PDF — interim ReportLab version exists, will be replaced by ITR-23 PDFKit migration
- Compare Mode in Synergy Sandbox: state vars exist but not wired

### Recent Commits (this session)
```
4ca9b08c BYT: Manual Search → AI Discovery criteria handoff (style keywords, discipline, states, budget tier)
a2d517d5 BYT Discovery: reorder tabs (AI Discovery first) + fix JSON truncation error (max_tokens 4096→16384 + repair logic)
```

### Previous Commits
```
ea726556 Add expandable detail view to saved Synergy configurations
a91d836d Fix Synergy Sandbox crash on save: handle JSONB already-parsed objects
b5efd130 Fix Synergy Sandbox: use activeProjectId from context
81b45e21 fix(shortlist): Send RFQ button now reflects actual invitation status
ee4d94e6 BYT Matchmaking: discipline-aware sub-metric display + v3 support
```

---

## Key References (in N4S repo)

- Module docs: `docs/memory/modules/BYT.md` — full tab structure, files, DB tables, API endpoints
- ITR items: `docs/memory/itr/ITR-MASTER.md` — open issues tagged BYT
- Architecture: `docs/memory/ARCHITECTURE.md` — hosting, tech stack, data flow
- PM/OR research PDF: uploaded Feb 28 — "Strategic Evaluation of Premier Owner's Representation and Project Management in the California Ultra-Luxury Residential Sector" (saved in session uploads, key findings captured in ITR-26)

---

## Suggested Next Steps

1. **ITR-26 ⚡ PM/OR Discovery Overhaul** — Top priority. Implement discipline-specific prompt engineering for PM/Owner's Rep search. Reference PDF research insights: boutique advisory firms, solo principals, luxury real-estate network discovery, regional regulatory specialization. Inject exemplar firms (MGMT Partners, SPECTRE8, Peak Projects, etc.) as calibration anchors. Files: `BYTDiscoveryScreen.jsx` (runAISearch prompt), `useBYTConfig.js` (PM/OR defaults), Admin config.
2. **Compare Mode** — Wire Synergy Sandbox multi-select comparison (state vars exist)
3. **Export Brief** — Wire Synergy results into Export Brief tab

---

*Updated by session close-out protocol. See PROTOCOL.md.*
