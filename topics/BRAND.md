# Topic: BRAND (Universal Brand Guidelines)

> **Status**: In Progress | **Projects**: N4S + Luxebrief | **Last Updated**: 2026-02-27

---

## What This Topic Covers

Establishing a unified brand identity for the Not4Sale ecosystem that covers both N4S (advisor platform) and Luxebrief (client portal). The goal is one canonical brand guide that both apps reference, replacing the currently separate per-app design guides.

---

## Current State

### What Exists Today
- **N4S**: Full brand guide at `docs/N4S-BRAND-GUIDE.md` — colors, typography, spacing, components, module colors, report standards, PDF standards
- **Luxebrief**: Design guidelines at `design_guidelines.md` — Apple HIG-inspired, voice recording UI patterns, typography, layout
- **Universal placeholder**: `BRAND-GUIDE.md` in claude-memory (this repo)

### Key Differences Between Apps

| Aspect | N4S | Luxebrief |
|--------|-----|-----------|
| **CSS approach** | Custom CSS + CSS variables | Tailwind CSS + shadcn/ui |
| **Heading font** | Playfair Display | Crimson Pro (optional Playfair) |
| **Body font** | Inter | Inter |
| **Layout** | Three-column module layout | Single-question flow |
| **Components** | Custom from scratch | shadcn/ui primitives |
| **Colors** | Navy + Gold + Soft Pillow module palette | Navy + Gold (same primary palette) |

### What Needs Harmonizing
1. Heading font decision — Playfair Display everywhere? Or Crimson Pro for Luxebrief?
2. Component patterns that appear in both apps (buttons, cards, forms)
3. Parker AI visual identity across both apps
4. PDF/report standards (already mostly unified via ITR-14 work)
5. Shared CSS variables or Tailwind config that stays in sync

---

## Suggested Next Steps

1. **Decide heading font** — Playfair Display as universal heading font, or allow Crimson Pro in Luxebrief?
2. **Document shared patterns** — buttons, cards, forms, modals, toasts that should look the same
3. **Expand BRAND-GUIDE.md** — fill in the universal guide with finalized decisions
4. **Cross-reference** — update N4S-BRAND-GUIDE.md and Luxebrief design_guidelines.md to reference the universal guide

---

*Updated by session close-out protocol. See PROTOCOL.md.*
