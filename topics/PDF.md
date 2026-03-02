# Topic: PDF
> **Status**: Active | **Created**: 2026-03-01 | **Projects**: N4S, Luxebrief

## Context
Unified PDF Architecture (ITR-23) — migrating all 32+ PDFs across the N4S ecosystem to a single PDFKit engine with shared `pdfBrandKit` foundation. Eliminates 6 technologies (jsPDF, html2canvas, PDFKit standalone, ReportLab, Puppeteer, jspdf-autotable) in favor of one.

## Current State
- **ITR-23 Phase 1 COMPLETE** (Feb 26): pdfBrandKit foundation deployed to LuXeBrief (`/var/www/luxebrief/server/pdf/`). 8 fonts installed on VPS (`/var/www/shared/fonts/`). Test PDF validated (32KB).
- **KYC Profile Report — FULLY UPDATED** (Mar 1): All 35 previously missing UI fields now in PDF. P1.TLN Gantt chart added. Caption positioning fixed. Label maps updated. 100% field parity between KYC UI and PDF.
- **N4S-PDF-STANDARD.md**: Comprehensive spec (v1.0, Feb 2026) — covers page setup, colors, typography, cover page, headers, footers, tables, orphan protection, sliders, provenance.
- **N4S-UNIFIED-PDF-PLAN.md**: Full migration roadmap — 4 phases.

## Key Files
- `docs/N4S-PDF-STANDARD.md` — Visual specification
- `docs/N4S-UNIFIED-PDF-PLAN.md` — Migration roadmap
- LuXeBrief `server/pdf/pdfBrandKit.ts` — Shared foundation (on VPS)
- LuXeBrief `server/pdf/pdfFonts.ts` — Font registration
- LuXeBrief `server/pdf/pdfLayout.ts` — Cover, headers, footers, orphan protection
- LuXeBrief `server/n4sDatabase.ts` — KYC Profile Report generator (`generateKYCProfileReport()` ~line 886)
- VPS `/var/www/shared/fonts/` — Playfair Display + Inter TTF files

## Critical Knowledge

### KYC PDF Routing (Important!)
The **Export Report** button in KYC (P1.A.1) calls the **VPS server-side** generator, NOT the client-side `KYCReportGenerator.js`:
- Button: `KYCModule.jsx` → `downloadServerPDF('kyc', 'profile-report', slug)`
- Route: `luxebrief.not-4.sale/api/n4s/pdf/kyc/profile-report`
- Generator: `n4sDatabase.ts` → `generateKYCProfileReport()` (PDFKit)
- The client-side `src/components/KYC/KYCReportGenerator.js` (jsPDF) is **ORPHANED** — not called by any button. Changes there have no effect on the exported PDF.

### KYC PDF Changes Made (Mar 1 Session)
1. **Label maps fixed**: Discovery Timeline (`urgent/standard/flexible` → `<3mo / 3-6 / 6+`), Target Timeline (`urgent/24-36mo/36-48mo/flexible` → `<24mo / 24-36 / 36-48 / Flexible 48+`)
2. **Caption positioning**: Section codes (P1.A.1, etc.) now render BELOW the heading gold line (was above)
3. **Project Launch Date**: Added to P1.A.3 table
4. **P1.TLN Project Timeline**: Full Gantt chart (9 phases, 3-layer opacity bars, vertical year/quarter markers) using projectParameters + budgetFramework directly (timelineData is not persisted to backend)
5. **35 missing fields added** across all sections:
   - P1.A.1: moveInExpectation, decisionMakingProcess, concurrentProjects, primaryResidences
   - P1.A.3: specificAddress, architecturalIntegration, localKnowledgeCritical
   - P1.A.4: perSFExpectation, architectFeeStructure, interiorDesignerFeeStructure
   - P1.A.6: separateOfficesRequired, officeRequirements, hobbyDetails, dailyRoutinesSummary
   - P1.A.7: storageNeeds, adjacencyRequirements, accessibilityRequirements
   - P1.A.9: existingIndustryConnections
6. **Gantt phase name shortened**: "Pre-Design & Team Assembly" → "Team Assembly"

### Timeline Data Note
`timelineData.complexityFactors` is computed client-side in AppContext but **never persisted** to the backend. The P1.TLN section uses `projectParameters.targetGSF`, `budgetFramework.interiorQualityTier`, and `projectParameters.siteTypology` directly — these ARE saved.

## Migration Phases
1. **Phase 1** ✅ — Build pdfBrandKit + install fonts on VPS
2. **Phase 2** (NEXT) — Migrate LuXeBrief reports (C1-C6, D1-D6) to shared kit
3. **Phase 3** — Documentation PDFs via VPS API (eliminate static files)
4. **Phase 4** — N4S client-side reports (A1-A9) → server-side via VPS API
5. **Phase 5** — Build missing generators (E1-E4)
6. **Phase 6** — Remove jsPDF/html2canvas/ReportLab dependencies

### Taste Exploration PDF (Client-Side jsPDF) — Overhauled Mar 1
Generator: `src/utils/TasteReportGenerator.js` (~1800 lines)
Call sites: `src/components/KYC/sections/DesignIdentitySection.jsx`

**Changes made (3 commits):**
1. `778ddda0` — Principal report: pass `null` for profileS at all 4 call sites so no partner data appears. Added brand-standard cover page (addCoverPage method). Renamed addPage1Cover → addOverviewPage. Updated generate() flow: cover → overview → [partner alignment if both] → 3 selection pages → [narrative if exists] → provenance. Base page count 4→5.
2. `0ff78183` — Partner narrative page: strip `**` markdown from H2/H3 headings. Fix table rendering with splitTextToSize + dynamic row heights. Replace Unicode emoji (✓⚠🚨) with ASCII (OK/CAUTION/ALERT) for jsPDF compatibility. Force page break before "Needs Facilitation" section.
3. `061d3b83` — Polish: fix blank page (only break if y>120), fix CAUTIONCAUTION (multi-codepoint ⚠️ matched as pair), strip HTML entities (&p etc.) from all text, reduce narrative maxY to prevent overlap with Data Provenance panel.

**Report variants:**
- **Principal only** (5 pages): cover + overview + 3 selection pages + provenance
- **Secondary only** (5 pages): same flow, uses stakeholderRole:'Secondary' + clientName from options
- **Combined** (7+ pages): cover + overview + partner alignment + 3 selection pages + narrative + provenance

**Secondary report**: no separate code needed — same generator, secondary call sites already pass secondary profile as profileP with null for profileS and include `stakeholderRole: 'Secondary'`.

**LuXeBrief replication**: NOT YET DONE. Next step is to ensure the same Taste Exploration PDF is generated when clicking "Principal DNA" on the LuXeBrief portal.

## Next Steps
1. **Replicate Taste Exploration PDF to LuXeBrief** — ensure "Principal DNA" button on LuXeBrief portal produces same report
2. Begin Phase 2: Migrate LuXeBrief C1-C6 generators to pdfBrandKit
3. Fix Phase 1 cosmetic issues (page numbering, footer spacing)
4. Consider removing orphaned client-side `KYCReportGenerator.js` (all PDF gen is now server-side)
5. Validate each migrated report visually against PDF Standard

## Last Session
2026-03-01 — Taste Exploration PDF overhaul: principal/secondary reports now show own data only + brand-standard cover page. Partner narrative formatting fixed (markdown stripping, emoji→ASCII, table readability, page breaks, provenance overlap). 3 commits pushed (778ddda0, 0ff78183, 061d3b83). LuXeBrief replication still pending.
