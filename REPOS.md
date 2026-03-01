# Repository Map — Not4Sale Ecosystem

> **Purpose**: Central reference for all repos, their purpose, URLs, and access.
> **Last Updated**: 2026-03-01

---

## Repos

### N4S (Advisor Platform)
- **Repo**: `linczyc-MLX/N4S`
- **URL**: https://github.com/linczyc-MLX/N4S
- **Visibility**: Public
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
- **Live URL**: https://luxebrief.not-4.sale
- **Has CLAUDE.md**: Yes

### Claude-Memory (This Repo)
- **Repo**: `linczyc-MLX/Claude-Memory`
- **URL**: https://github.com/linczyc-MLX/Claude-Memory
- **Visibility**: Public
- **Purpose**: Canonical session memory — universal preferences, topic handovers, project state
- **Clone at start of every session**
- **Has CLAUDE.md**: Yes
- **Has .claude/commands/**: Yes (start-session, end-session)

### Parker API
- **Repo**: `linczyc-MLX/N4S-Parker-API`
- **URL**: https://github.com/linczyc-MLX/N4S-Parker-API
- **Purpose**: Parker AI advisor backend (standalone microservice on VPS)
- **Tech**: Express + TypeScript, Anthropic SDK, SSE streaming, PostgreSQL
- **Deploy**: VPS (74.208.250.22) via PM2 (`parker-api`)
- **Live URL**: https://parker.not-4.sale

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
  - RFQ API (rfq.not-4.sale) — PM2 process `n4s-rfq-api`
  - Luxebrief (luxebrief.not-4.sale) — PM2 process `luxebrief`
  - Parker API (parker.not-4.sale) — PM2 process `parker-api`
- **Databases**:
  - PostgreSQL: rfq_db, luxebrief_db, parker_db

## IONOS Details

- **Static hosting**: app-ionos.space (N4S frontend builds)
- **FTP hosting**: website.not-4.sale (PHP API + static frontend)
- **Database**: MariaDB/MySQL (N4S project data, KYC, FYI, etc.)

---

## Access Notes

- **N4S and Claude-Memory are public repos** — no token needed to clone
- **Luxebrief is private** — requires GitHub token or SSH key
- VPS SSH access requires the SSH key configured for root@74.208.250.22
- IONOS deployment is automated via GitHub Actions — no manual access needed for deploys
- If cloning fails with auth error, try `git -c http.proxyAuthMethod=basic clone` or check token scope

---

*Update this file when new repos are created or infrastructure changes.*
