# Project State: Luxebrief (Client Portal)

> **Last Updated**: 2026-02-27

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

## Cross-Project Notes

- Luxebrief generates PDFs (C1-C6) that N4S portal references
- Phase 1 PDF migration (ITR-14) updated all 6 generators in Luxebrief's `server/n4sDatabase.ts`
- ITR-21/22: Phase 1 bugs in C2/C3 and missing portal card need fixing in Luxebrief repo
- Parker Phase 2 will create a separate N4S-specific Parker on VPS alongside Luxebrief's Parker

---

*Updated by session close-out protocol.*
