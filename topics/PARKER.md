# Topic: PARKER (AI Advisor)

> **Status**: Phase 2 LIVE (v2.0.0-phase2d) — Knowledge audit complete | **Projects**: N4S + Luxebrief | **Last Updated**: 2026-03-01

---

## What This Topic Covers

Parker (PANDA — Personal Asset Networked Development Advisor) is an AI assistant that exists in both N4S (advisor-facing) and Luxebrief (client-facing) with different personas, context access, and capabilities.

---

## Current State (as of Mar 1, 2026)

### Phase 1 (Live in N4S)
- Widget + chat panel with static tips per module
- Narrative greetings (professional/friendly/formal per module)
- Tooltip system with localStorage persistence, badge count
- Panda avatar, warm/professional tone

### Phase 2 — LIVE (v2.0.0-phase2d)
- **Service**: parker.not-4.sale (Express + Anthropic SDK + SSE streaming)
- **PM2 process**: `parker-api` on VPS 74.208.250.22
- **DB**: VPS PostgreSQL (parker_db) for conversations + IONOS MariaDB reader for project context
- **Health**: `curl -s https://parker.not-4.sale/api/parker/status | jq .`
- **Build**: `cd /var/www/parker-api && npm run build`
- **Restart**: `pm2 delete parker-api && pm2 start ecosystem.config.cjs` (NOT pm2 restart)
- **No git on VPS** — direct file edits only, always backup `.ts.bak` before editing

### Knowledge Audit Completed (2026-03-01)
- **38 errors found** across 4 knowledge files, **30 corrections applied**
- Major fixes: KYC section numbering (9→8), FYI zones (6 fake→10 correct), Taste Exploration categories (11→9), Architectural Styles (12→9), BYT screens (8→7), BAM moved from KYM to BYT, VMX name corrected, MVP gates/tiers added, KYS scoring categories added
- **37 unverifiable facts** flagged for manual review
- **16 missing field extractions** in contextBuilder.ts (lower priority)
- Audit artifacts: `~/parker-audit/` (audit reports, changes-log, truth map)

### Key Knowledge Files (VPS)
- `/var/www/parker-api/src/knowledge/moduleKnowledge.ts` — Per-module knowledge
- `/var/www/parker-api/src/knowledge/processKnowledge.ts` — Workflow/process knowledge
- `/var/www/parker-api/src/knowledge/systemPrompt.ts` — System prompt builder
- `/var/www/parker-api/src/services/contextBuilder.ts` — Live project data extraction

### N4S Modules Parker Knows About
| Module | Color | Key Facts |
|--------|-------|-----------|
| Dashboard | #1e3a5f | Project overview |
| KYC | #315098 | 8 sections P1.A.1-P1.A.8, Taste Exploration (9 categories, 9 AS styles) |
| FYI | #8CA8BE | 10 zones (Z1_APB-Z10_PH), source of truth for SF |
| MVP | #AFBDB0 | 5 deployment gates (A-E), 4 tiers (5K/10K/15K/20K) |
| KYM | #E4C0BE | Know Your Market |
| KYS | #A8B0BF | 7 scoring categories, weights total 100% |
| VMX | #C9B8C9 | Vision Matrix (NOT Visual Matrix), tiers: select/reserve/signature/legacy |
| BYT | #BCA89A | 7 screens, BAM v2.0 (8 dimensions, 2 output scores) |
| Settings | #374151 | Users, Admin Tools, Parker Usage |
| LCD | — | LuXeBrief Client Dashboard |

### Critical Parker Facts
- FYI is source of truth for SF via `transformFYIToMVPProgram()`
- FYI selections is an OBJECT (not array) keyed by space code
- Client names live in `kycData.principal.portfolioContext` (NOT designIdentity)
- Secondary respondent completes ONLY P1.A.5 and P1.A.6
- BAM v2.0 belongs to BYT (NOT KYM)
- 7 cross-module data flows: KYC→FYI, FYI→MVP, KYC→BYT, KYC→VMX, FYI→VMX, KYC→KYS, KYC→LCD

### N4S Parker vs Luxebrief Parker

| Dimension | Luxebrief (Client) | N4S (Advisor) |
|---|---|---|
| Tone | Butler, luxury, protective | Collaborative colleague, technical |
| Knowledge | Limited process overview | Full N4S workflow + live data |
| Auth | Portal token | N4S session auth |
| Context | Client name, completed modules | Everything — KYC, FYI, MVP, BYT, etc. |

---

## Key References

- N4S module docs: `docs/memory/modules/PARKER.md`
- Phase 2 spec: `docs/PARKER-PHASE2-SPEC.md` in N4S repo
- Luxebrief Parker code: `server/parkerService.ts`, `server/parkerRoutes.ts`, `server/parkerKnowledge.ts` in Luxebrief repo
- ITR-12 in N4S `docs/memory/itr/ITR-MASTER.md`

---

## Suggested Next Steps

1. **Resolve 16 missing field extractions** in contextBuilder.ts (advisorAssessed, KYS scoring data, BYT match details, VMX regions, LCD config)
2. **Manual review of 37 unverifiable facts** — cross-check against N4S source code
3. **Add KYM documentation** to truth map (currently undocumented)
4. **Add CI validation** to prevent future knowledge drift in VPS files

---

*Updated by session close-out protocol. See PROTOCOL.md.*
