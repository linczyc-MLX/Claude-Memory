# Universal Memory — Michael Linczyc

> **This file is loaded at the start of every Claude session, regardless of topic, project, or interface.**
> **Last Updated**: 2026-02-27

---

## Owner

- **Name**: Michael Linczyc
- **Email**: linczyc@gmail.com
- **Company**: MLX Consulting
- **Role**: Principal, Luxury Residential Advisory (LRA)

---

## The Not4Sale Ecosystem

Not4Sale is a luxury residential advisory platform for ultra-high-net-worth families and family offices. It helps plan and validate 10,000–20,000+ SF custom residences through structured workflows.

The ecosystem has two tightly linked applications:

| App | Purpose | Audience | Repo |
|-----|---------|----------|------|
| **N4S** | Advisor dashboard — full project management, 7+ modules | LRA team (advisors) | linczyc-MLX/N4S |
| **Luxebrief** | Client-facing portal — briefing, reports, Parker AI | UHNW clients | linczyc-MLX/Luxebrief |

These apps share a VPS backend, database layer, and brand identity. Data integrity between them is critical — no local data, everything live on the server.

---

## Working Preferences

### Code & Files
- **Never ask me to paste code into files.** Provide complete edited files for upload, then after my confirmation, push directly to GitHub.
- **Git-first workflow.** All changes committed and pushed. GitHub Actions auto-deploys.
- **No manual zip uploads.** Auto-deploy via GitHub Actions to IONOS.
- **No local data.** Everything live and up to date on the server.
- **Relative URLs only.** Never hardcode absolute URLs — use relative `/api`.

### Session Style
- **Topic-based sessions** with clear handover at start and end.
- Concise communication. Get to the point.
- When investigating issues, check both N4S and Luxebrief repos — they're tightly coupled.
- Always read the relevant CLAUDE.md and memory files before starting work.

### Development Tools
- **Superpowers plugin** for all development work. Use its structured workflows:
  - Brainstorming before jumping into code
  - Writing plans with bite-sized tasks
  - Subagent-driven development for implementation
  - Test-driven development (RED-GREEN-REFACTOR)
  - Systematic debugging (4-phase root cause process)
  - Code review before completion
  - Verification before declaring done
- Reference: github.com/linczyc-MLX/Superpowers (or obra/superpowers upstream)

---

## Active Topics

| Topic | Description | Status | Last Touched | Projects |
|-------|-------------|--------|-------------|----------|
| BYT | Build Your Team module — consultant matching, RFQ, synergy | Active dev | 2026-02-25 | N4S |
| PARKER | Parker AI assistant — Phase 2 standalone microservice | Architecture approved | 2026-02-25 | N4S + Luxebrief |
| BRAND | Universal brand guidelines for Not4Sale ecosystem | In progress | 2026-02-27 | N4S + Luxebrief |

---

## Key Architectural Facts

1. **N4S frontend**: React 18 + TypeScript (CRA), custom CSS, Playfair Display + Inter fonts
2. **Luxebrief frontend**: React + TypeScript (Vite), shadcn/ui + Tailwind CSS, Inter + Crimson Pro fonts
3. **N4S backend**: PHP on IONOS shared hosting (website.not-4.sale/api/)
4. **Luxebrief backend**: Node.js/Express on VPS (74.208.250.22)
5. **Databases**: MySQL/MariaDB on IONOS (N4S data), PostgreSQL on VPS (RFQ, Luxebrief, Parker)
6. **VPS**: 74.208.250.22 — runs RFQ API, Luxebrief, and (soon) Parker API
7. **VPS consultant_id (UUID) ≠ IONOS consultant_id (auto-increment)** — always match by firm_name+discipline across systems

---

## Brand Identity (Summary)

- **Primary Colors**: Navy `#1e3a5f`, Gold `#c9a227`
- **Fonts**: Playfair Display (headings), Inter (body/UI)
- **Tone**: Sophisticated, trustworthy, warm — like private banking materials
- Full guide: see `BRAND-GUIDE.md` in this repo

---

*This file should be updated only when preferences, tools, or ecosystem-level facts change — not per-session.*
