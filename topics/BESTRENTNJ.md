# Topic: BESTRENTNJ (Township News Tool)

> **Status**: Live (harvest reliability degraded) | **Projects**: BestRentNJ | **Last Updated**: 2026-03-01

---

## What This Topic Covers

Single-user internal tool for generating 27 monthly township news posts for BestRentNJ.com. Built for Ricky. Node.js/Express backend + React/Vite frontend + SQLite + BullMQ.

---

## Current State (as of Mar 1, 2026)

### What's Working
- Live at https://ricky.longshot.productions (login: admin / Ricky2026!)
- Railway deployment (project: bestrentnj, service: bestrentnj-app)
- 27 NJ townships, 6 event types each = 162 harvest jobs per batch
- OpenAI gpt-4o-mini for extraction/drafting
- Serper Google search API for event harvesting
- Upstash Redis for BullMQ job queue
- Postmark for email (FROM locked to @longshot.productions)

### Known Issues
- **Harvest reliability degraded** — most townships failing. Top priority to investigate.
- SQLite DB is ephemeral on Railway (recreated each deploy from schema.sql + seed.sql)
- Volume mounted at `/app/data` (contains SQLite DB)

### Critical Lessons (Feb 17, 2026)
- Do NOT increase BullMQ concurrency above 1 on Railway — causes OOM crashes
- Queue rate limiter MUST stay: `max: 2, duration: 1000`
- BullMQ `getFailedCount()` is GLOBAL — use `queue.obliterate()` before new harvest
- `getSupportStories()` takes 60+ seconds — has 30s timeout wrapper
- Always deploy to `bestrentnj-app` service (NOT `bestrentnj`)

### External Services
- **OpenAI** (cherryseer@mac.com) — gpt-4o-mini
- **Serper** (cherryseer@mac.com) — Google search API
- **Upstash Redis** (ricky@longshot.productions) — BullMQ queue
- **Postmark** (ricky@longshot.productions) — Email sending

---

## Key References
- Project dir: `~/Dropbox/"MY FILES"/MLX/PERSONAL/RICKY/bestrentnj-tool`
- `BESTRENTNJ_GUIDE.md` in project root — full credentials, structure, API keys
- `HANDOVER.md` in project root — Feb 17 session details

---

## Suggested Next Steps

1. **Fix harvest reliability** — investigate why most townships are failing
2. **Consider persistent storage** — SQLite ephemeral on Railway is fragile

---

*Updated by memory migration 2026-03-01.*
