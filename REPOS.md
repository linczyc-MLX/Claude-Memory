# Repository Map — Not4Sale Ecosystem

> **Purpose**: Central reference for all repos, their purpose, URLs, and access.
> **Last Updated**: 2026-02-27

---

## Repos

### N4S (Advisor Platform)
- **Repo**: `linczyc-MLX/N4S`
- **URL**: https://github.com/linczyc-MLX/N4S
- **Purpose**: Main advisor dashboard — KYC, FYI, MVP, KYM, KYS, VMX, BYT modules
- **Tech**: React 18 + TypeScript (CRA), PHP backend, MySQL/MariaDB
- **Deploy**: GitHub Actions → IONOS (static site + PHP API)
- **Live URLs**:
  - IONOS Space: https://home-5019406629.app-ionos.space/
  - FTP Site: https://website.not-4.sale/
- **Has CLAUDE.md**: Yes
- **Has docs/memory/**: Yes (module-specific reference docs, ITR, ARCHITECTURE)

### Luxebrief (Client Portal)
- **Repo**: `linczyc-MLX/Luxebrief`
- **URL**: https://github.com/linczyc-MLX/Luxebrief
- **Purpose**: Client-facing briefing portal — voice recording, AI transcription, PDF reports, Parker AI
- **Tech**: React + TypeScript (Vite), Node.js/Express, PostgreSQL, shadcn/ui + Tailwind
- **Deploy**: VPS (74.208.250.22) via PM2
- **Live URL**: https://luxebrief.not-4.sale (or Replit dev URL)
- **Has CLAUDE.md**: Yes (created 2026-02-27)

### Claude Memory (This Repo)
- **Repo**: `linczyc-MLX/claude-memory`
- **URL**: https://github.com/linczyc-MLX/claude-memory
- **Purpose**: Canonical session memory — universal preferences, topic handovers, project state
- **Visibility**: Private
- **Clone at start of every session**

### VMX Standalone
- **Repo**: `linczyc-MLX/N4S-VisualMatrix`
- **URL**: https://github.com/linczyc-MLX/N4S-VisualMatrix
- **Purpose**: Standalone Vision Matrix app (also integrated into N4S)
- **Live URL**: https://home-5019398597.app-ionos.space/

### N4S-RFQ (RFQ Portal)
- **Repo**: `linczyc-MLX/N4S-RFQ` (frontend) + `linczyc-MLX/N4S-RFQ-API` (backend)
- **Purpose**: Consultant-facing RFQ questionnaire portal
- **Live URL**: https://rfq.not-4.sale
- **Tech**: React frontend, Express/Node backend on VPS

### Superpowers (Development Plugin)
- **Repo**: `linczyc-MLX/Superpowers` (fork of obra/superpowers)
- **URL**: https://github.com/linczyc-MLX/Superpowers
- **Purpose**: Claude Code plugin for structured dev workflows (brainstorming, TDD, code review, subagent-driven dev)

---

## VPS Details

- **IP**: 74.208.250.22
- **SSH**: `ssh root@74.208.250.22`
- **Services**:
  - RFQ API (rfq.not-4.sale) — PM2 process
  - Luxebrief (luxebrief.not-4.sale) — PM2 process
  - Parker API (parker.not-4.sale) — planned, PM2 process
- **Databases**:
  - PostgreSQL: rfq_db, luxebrief_db, parker_db (planned)

## IONOS Details

- **Static hosting**: app-ionos.space (N4S frontend builds)
- **FTP hosting**: website.not-4.sale (PHP API + static frontend)
- **Database**: MariaDB/MySQL (N4S project data, KYC, FYI, etc.)

---

## Access Notes

- GitHub tokens are repo-scoped. If cloning fails, the token may need updating.
- N4S repo token is typically embedded in the CLAUDE.md or provided at session start.
- Claude-memory repo requires its own token (may differ from N4S token).
- VPS SSH access requires the SSH key configured for root@74.208.250.22.
- IONOS deployment is automated via GitHub Actions — no manual access needed for deploys.

---

*Update this file when new repos are created or infrastructure changes.*
