# Project State: Luxebrief (Client Portal)

> **Last Updated**: 2026-03-01 (PDF session)

---

## Git State

- **Branch**: main
- **Repo**: linczyc-MLX/Luxebrief

## Deploy State

- **VPS**: 74.208.250.22 — PM2 process
- **URL**: https://luxebrief.not-4.sale (or Replit dev environment)
- **Deploy method**: SSH + git pull + npm install + pm2 restart

## Tech Stack

- **Frontend**: React + TypeScript (Vite), shadcn/ui + Tailwind CSS, Radix UI, Lucide React
- **Backend**: Node.js/Express + TypeScript
- **Database**: PostgreSQL (Drizzle ORM) on VPS
- **Voice**: MediaRecorder → ffmpeg → OpenAI Whisper
- **Reports**: OpenAI GPT analysis → PDFKit generation
- **Schema**: `shared/schema.ts`

## Key Features

- Voice-recorded briefing questionnaire (per-question, single-screen flow)
- AI transcription (Whisper) + AI report generation (GPT)
- Admin panel at /admin (question management, site content)
- PDF export of briefing reports
- Parker AI (Phase 1 — static tips/tooltips, client-facing butler persona)
- Cloud storage for audio/transcripts/reports

## Parker in Luxebrief

- Phase 1 live: parkerService.ts, parkerRoutes.ts, parkerKnowledge.ts
- Client-facing persona: warm butler, limited knowledge, portal auth
- Conversations stored in PostgreSQL (parker_conversations, parker_messages, parker_client_memory)
- This serves as the "gold standard reference" for N4S Parker Phase 2

## KYC Profile Report (n4sDatabase.ts)
- `generateKYCProfileReport()` at ~line 886 — server-side PDFKit generator
- Called by N4S Export Report button via `luxebrief.not-4.sale/api/n4s/pdf/kyc/profile-report`
- **Mar 1**: All 35 missing fields added, P1.TLN Gantt chart, caption positioning fixed, label maps updated
- **WARNING**: Changes were made directly on VPS via SSH/python patch scripts — NOT committed to git. Must be committed to Luxebrief repo to persist across deploys.

## Cross-Project Notes

- Luxebrief generates PDFs (C1-C6) that N4S portal references
- ITR-24 Brand Guidelines Standardization COMPLETE (Feb 27) — 33/34 PDFs brand-compliant
- All 18 generators verified: full pipeline `createDoc → addCoverPage → [content] → addProvenanceNotice → finalizeDoc`
- Footer overlap bug fixed (commits `42fa450`, `6bc774a`)
- BYT dual export removed, dead `BYTExportBrief.js` deleted (commit `ca55ca23`)
- Parker Phase 2 will create a separate N4S-specific Parker on VPS alongside Luxebrief's Parker

---

*Updated by session close-out protocol.*
