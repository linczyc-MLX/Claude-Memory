# Topic: PARKER (AI Advisor)

> **Status**: Phase 2 LIVE (v2.0.0-phase2d) — contextBuilder major fix + relay audit complete | **Projects**: N4S + Luxebrief | **Last Updated**: 2026-03-01

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
- **SSH key**: `~/.ssh/parker_vps` (use `ssh -i ~/.ssh/parker_vps root@74.208.250.22`)

### Knowledge Audit Completed (2026-03-01, earlier session)
- **38 errors found** across 4 knowledge files, **30 corrections applied**
- **37 unverifiable facts** flagged for manual review
- Audit artifacts: `~/parker-audit/` (audit reports, changes-log, truth map)

### contextBuilder Major Fix (2026-03-01, this session)

**18 new field extractions added + 21 KYC Tier 1 fields added:**

1. FYI brief totals (net/circulation/gross SF, targetSF, programTier, spacesByZone)
2. FYI root-level selections/settings fallback paths
3. MVP root-level fields (mvpAdjacencyConfig, mvpChecklistState, mvpAdjacencyDecisions, mvpModuleReviewStatus)
4. MVP path correction: fields live INSIDE `fyiData` in relay (not at root) — `fyiData.mvpAdjacencyConfig` is primary path
5. KYS detailed site scores (string-keyed "1.1"→"7.5", category averages, traffic lights, dealbreakers)
6. KYS site basicInfo (name, city, state, acreage, askingPrice) + handoffNotes
7. selectedArchitect / selectedID (root-level)
8. advisorAssessed (profileCompleteness, dataConfidenceScore, visionFlexibilityIndex, divergenceLog)
9. Family & Household: petGroomingRoom, petDogRun, anticipatedFamilyChanges, familyMembers details
10. Project Parameters: sfCapConstraint, complexityFactors, architecturalIntegration, localKnowledgeCritical, levelsAboveArrival/Below
11. Lifestyle: dailyRoutinesSummary, hobbies, hobbyDetails, lateNightMediaUse, noiseSensitivity
12. Space Requirements: all 5 boolean flags, viewPriorityRooms, currentSpacePainPoints, storageNeeds, accessibilityRequirements

**Temporary logging active** — discovery logging for VMX/BYT/LCD/KYC paths + pets debug logging. Remove after one test cycle (`pm2 logs parker-api`).

**VPS backup**: `contextBuilder.ts.bak2` preserved.

### Relay Audit Completed (2026-03-01, this session)

Full data pipeline audit saved to `~/parker-audit/RELAY-AUDIT-REPORT.md`. Key findings:

1. **RELAY-PAYLOAD-MAP was wrong about nesting** — selections, settings, mvpChecklistState, mvpAdjacencyConfig are INSIDE `fyiData`, not at root of projectData
2. **Pets pipeline is clean** — string end-to-end, "garbled" likely historic data corruption or AI reformatting
3. **42 KYC fields missing from contextBuilder** — 21 Tier 1 now fixed, 21 Tier 2 remaining
4. **Module-selective visibility** — Parker only sees non-KYC module data when user is on that module (design limitation)
5. **"Client Data Read Only" has zero effect on Parker** — purely UI lock
6. **No `consolidated` key in kycData** — computed on-the-fly in FYIModule only, never persisted
7. **kysData stored inside fyiData** — not in PHP save whitelist, smuggled for persistence

### Key Knowledge Files (VPS)
- `/var/www/parker-api/src/knowledge/moduleKnowledge.ts` — Per-module knowledge
- `/var/www/parker-api/src/knowledge/processKnowledge.ts` — Workflow/process knowledge
- `/var/www/parker-api/src/knowledge/systemPrompt.ts` — System prompt builder
- `/var/www/parker-api/src/services/contextBuilder.ts` — Live project data extraction

### Critical Relay Architecture Facts
- `buildParkerPayload()` in `src/components/Parker/parkerPayload.js` builds the POST payload
- Always sends: `kycData` (all respondents), `clientData`, `_completionFlags`
- Module-selective: adds active module's data blob only (e.g., FYI only sent when on FYI module)
- `kycData` has 3 respondents: `principal`, `secondary`, `advisor` (NO `consolidated`)
- MVP fields live inside `fyiData` (stored together for PHP save compatibility)
- `kysData` is extracted from `fyiData.kysData` on load (not in PHP whitelist)
- PHP save whitelist: `kycData, fyiData, activeRespondent, lcdData, vmxData, kymData, bytData, mvpData`

### Critical Parker Facts
- FYI is source of truth for SF via `transformFYIToMVPProgram()`
- FYI selections is an OBJECT (not array) keyed by space code
- Client names live in `kycData.principal.portfolioContext` (NOT designIdentity)
- Secondary respondent completes ONLY P1.A.5 and P1.A.6
- BAM v2.0 belongs to BYT (NOT KYM)
- 7 cross-module data flows: KYC→FYI, FYI→MVP, KYC→BYT, KYC→VMX, FYI→VMX, KYC→KYS, KYC→LCD

---

## Key References

- N4S module docs: `docs/memory/modules/PARKER.md`
- Relay audit report: `~/parker-audit/RELAY-AUDIT-REPORT.md`
- Relay payload map: `~/parker-audit/RELAY-PAYLOAD-MAP.md`
- Truth map: `~/parker-audit/TRUTH-MAP.md`
- Luxebrief Parker code: `server/parkerService.ts`, `server/parkerRoutes.ts`, `server/parkerKnowledge.ts` in Luxebrief repo
- ITR-12 in N4S `docs/memory/itr/ITR-MASTER.md`

---

## Suggested Next Steps

1. **Remove temporary logging** — send a test message to Parker, check `pm2 logs parker-api` for discovery output, then remove the logging lines
2. **Fix 2 Tier 2: remaining 21 KYC fields** — Design Identity (inspirationImages, aspirationKeywords, antiInspiration, benchmarkProperties, exteriorMaterialPreferences, structuralAmbition), Cultural Context (entertainingCulturalNorms, crossCulturalRequirements, languagesPreferred), Working Preferences (presentationFormat, existingIndustryConnections, celebrity prefs, contractor prefs)
3. **Investigate Thornwood pets data** — run DB query from IONOS PHP side (VPS can't reach IONOS MariaDB)
4. **Consider Fix 4: send all module data always** — architectural change to fix cross-module question blindness
5. **Manual review of 37 unverifiable facts** — cross-check against N4S source code
6. **Add KYM documentation** to truth map (currently undocumented)

---

*Updated by session close-out protocol. See PROTOCOL.md.*
