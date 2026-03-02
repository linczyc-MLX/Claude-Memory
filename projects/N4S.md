# Project State: N4S (Advisor Platform)

> **Last Updated**: 2026-03-01

---

## Git State

- **Branch**: main
- **Latest commit**: `0ff78183` — fix(KYC): improve partner narrative PDF formatting
- **Repo**: linczyc-MLX/N4S

## Deploy State

- **IONOS Space**: https://home-5019406629.app-ionos.space/ — auto-deployed from main
- **FTP Site**: https://website.not-4.sale/ — auto-deployed from main
- **Build**: Clean (last build successful)
- **Deploy method**: GitHub Actions (push to main triggers build + deploy)

## Current Phase

Active development on BYT module. Parker Phase 2 LIVE (v2.0.0-phase2d). KYC Profile Report PDF fully updated (Mar 1) — all fields, Gantt chart, caption fix. Note: KYC PDF changes are on VPS `n4sDatabase.ts` (direct SSH edits, not in git yet).

## Module Status

| Module | Status | Notes |
|--------|--------|-------|
| Dashboard | Live | Stable |
| KYC | Live | Stable |
| FYI | Live | ITR-1 (minor display issue) |
| MVP | Live | ITR-5, ITR-6 (minor) |
| KYM | Live | Stable, RapidAPI key required |
| KYS | Live | Stable |
| VMX | Live (separate app) | ITR-2 (manual SF entry) |
| BYT | Active dev | Synergy Sandbox live, Compare Mode pending |
| Settings | Live | Stable |

## Open ITR Items

See `docs/memory/itr/ITR-MASTER.md` in N4S repo for full list. Key items:
- ITR-10: BYT Synergy scoring pipeline testing
- ITR-12: Parker Phase 2 (LIVE — v2.0.0-phase2d, knowledge audit + contextBuilder fix + relay audit done)
- ITR-13: BYT Documentation PDF
- ITR-14: PDF Standard Migration (Phase 1 complete)
- ITR-21/22: PDF Phase 1 bugs (C2/C3 BLUE, portal card)

## Cross-Project Notes

- N4S PHP API on IONOS reads/writes MariaDB — same DB that Parker (planned) will read
- BYT engagements sync between IONOS MySQL and VPS PostgreSQL (rfq_db)
- Match by firm_name+discipline across systems, never by ID (VPS UUID ≠ IONOS auto-increment)

---

*Updated by session close-out protocol.*
