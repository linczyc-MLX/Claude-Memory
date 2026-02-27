# Topic: PARKER (AI Advisor)

> **Status**: Phase 2 Architecture Approved | **Projects**: N4S + Luxebrief | **Last Updated**: 2026-02-27

---

## What This Topic Covers

Parker (PANDA — Personal Asset Networked Development Advisor) is an AI assistant that exists in both N4S (advisor-facing) and Luxebrief (client-facing) with different personas, context access, and capabilities.

---

## Current State (as of Feb 25, 2026)

### Phase 1 (Live in N4S)
- Widget + chat panel with static tips per module
- Narrative greetings (professional/friendly/formal per module)
- Tooltip system with localStorage persistence, badge count
- Panda avatar, warm/professional tone

### Phase 2 Architecture (Approved — ITR-12)
- **Decision**: Option A2 — Standalone Parker microservice on VPS
- **Service**: parker.not-4.sale (Express + Anthropic SDK + SSE streaming)
- **DB**: VPS PostgreSQL (parker_db) for conversations + IONOS MariaDB reader for project context
- **Full spec**: `docs/PARKER-PHASE2-SPEC.md` in N4S repo
- **Module docs**: `docs/memory/modules/PARKER.md` in N4S repo

### N4S Parker vs Luxebrief Parker

| Dimension | Luxebrief (Client) | N4S (Advisor) |
|---|---|---|
| Tone | Butler, luxury, protective | Collaborative colleague, technical |
| Knowledge | Limited process overview | Full N4S workflow + live data |
| Auth | Portal token | N4S session auth |
| Context | Client name, completed modules | Everything — KYC, FYI, MVP, BYT, etc. |

### Implementation Phases (Not Yet Started)
- **2a (Foundation)**: Scaffold N4S-Parker-API repo, VPS setup (PM2, Nginx, SSL, DNS), PostgreSQL schema, Express service, Anthropic streaming, IONOS MariaDB reader
- **2b (Frontend)**: Wire N4S parkerAPI.js SSE, ParkerChat.jsx streaming, auth tokens
- **2c (Intelligence)**: Live project data injection, cross-module insights, memory extraction

---

## Key References

- N4S module docs: `docs/memory/modules/PARKER.md`
- Phase 2 spec: `docs/PARKER-PHASE2-SPEC.md` in N4S repo
- Luxebrief Parker code: `server/parkerService.ts`, `server/parkerRoutes.ts`, `server/parkerKnowledge.ts` in Luxebrief repo
- ITR-12 in N4S `docs/memory/itr/ITR-MASTER.md`

---

## Suggested Next Steps

1. **Phase 2a** — Scaffold N4S-Parker-API repo, VPS setup, PostgreSQL schema, Express service
2. **Phase 2b** — Wire N4S frontend (parkerAPI.js SSE, ParkerChat.jsx streaming)
3. **Phase 2c** — Live project data injection, cross-module insights

---

*Updated by session close-out protocol. See PROTOCOL.md.*
