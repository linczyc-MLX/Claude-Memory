# Topic: PDF
> **Status**: Active | **Created**: 2026-03-01 | **Projects**: N4S, Luxebrief

## Context
Unified PDF Architecture (ITR-23) — migrating all 32+ PDFs across the N4S ecosystem to a single PDFKit engine with shared `pdfBrandKit` foundation. Eliminates 6 technologies (jsPDF, html2canvas, PDFKit standalone, ReportLab, Puppeteer, jspdf-autotable) in favor of one.

## Current State
- **ITR-23 Phase 1 COMPLETE** (Feb 26): pdfBrandKit foundation deployed to LuXeBrief (`/var/www/luxebrief/server/pdf/`). 8 fonts installed on VPS (`/var/www/shared/fonts/`). Test PDF validated (32KB).
- **Phase 1 cosmetic issues noted**: page numbering on separate blank pages, footer text spacing — to address in Phase 2.
- **KYC Profile Report** (A2): Phase 1 compliant — cover page, header all pages, accent stripe, 3-col footer, gold rules, bottom-third protection, provenance. Still Helvetica-only (Phase 2 will add Playfair+Inter).
- **N4S-PDF-STANDARD.md**: Comprehensive spec (v1.0, Feb 2026) — covers page setup, colors, typography, cover page, headers, footers, tables, orphan protection, sliders, provenance.
- **N4S-UNIFIED-PDF-PLAN.md**: Full migration roadmap — 4 phases.

## Key Files
- `docs/N4S-PDF-STANDARD.md` — Visual specification
- `docs/N4S-UNIFIED-PDF-PLAN.md` — Migration roadmap
- LuXeBrief `server/pdf/pdfBrandKit.ts` — Shared foundation (on VPS)
- LuXeBrief `server/pdf/pdfFonts.ts` — Font registration
- LuXeBrief `server/pdf/pdfLayout.ts` — Cover, headers, footers, orphan protection
- VPS `/var/www/shared/fonts/` — Playfair Display + Inter TTF files

## Migration Phases
1. **Phase 1** ✅ — Build pdfBrandKit + install fonts on VPS
2. **Phase 2** (NEXT) — Migrate LuXeBrief reports (C1-C6, D1-D6) to shared kit
3. **Phase 3** — Documentation PDFs via VPS API (eliminate static files)
4. **Phase 4** — N4S client-side reports (A1-A9) → server-side via VPS API
5. **Phase 5** — Build missing generators (E1-E4)
6. **Phase 6** — Remove jsPDF/html2canvas/ReportLab dependencies

## Next Steps
1. Begin Phase 2: Migrate LuXeBrief C1-C6 generators to pdfBrandKit
2. Fix Phase 1 cosmetic issues (page numbering, footer spacing)
3. Validate each migrated report visually against PDF Standard

## Last Session
2026-03-01 — Topic file created (first PDF-specific session).
