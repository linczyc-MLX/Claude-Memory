# Not4Sale Universal Brand Guide

> **Purpose**: Defines the visual identity and brand standards that apply across ALL Not4Sale ecosystem products (N4S advisor platform, Luxebrief client portal, Parker AI, generated reports, documentation).
> **Version**: 0.1 (placeholder — to be developed in the BRAND topic)
> **Last Updated**: 2026-02-27

---

## Brand Essence

**Not4Sale** is a luxury residential advisory platform serving ultra-high-net-worth families and family offices. Every visual element must communicate:

- **Sophistication** — Refined, never flashy
- **Trust** — Professional, established, credible
- **Clarity** — Information presented cleanly without clutter
- **Warmth** — Approachable luxury, not cold minimalism

The visual language should feel like a private banking report or a luxury hotel's guest materials — understated elegance with meticulous attention to detail.

---

## Universal Color Palette

### Primary
| Name | Hex | Usage |
|------|-----|-------|
| **Navy** | `#1e3a5f` | Primary brand color across all products |
| **Gold** | `#c9a227` | Accent — CTAs, highlights, selected states |

### Neutrals
| Name | Hex | Usage |
|------|-----|-------|
| **Background** | `#fafaf8` | Page backgrounds (warm, not pure white) |
| **Surface** | `#ffffff` | Cards, panels |
| **Border** | `#e5e5e0` | Dividers, card borders |
| **Text** | `#1a1a1a` | Primary text |
| **Text Muted** | `#6b6b6b` | Secondary text, labels |

### Semantic
| Name | Hex |
|------|-----|
| **Success** | `#2e7d32` |
| **Warning** | `#f57c00` |
| **Error** | `#d32f2f` |

---

## Universal Typography

| Role | N4S | Luxebrief | Reports/PDFs |
|------|-----|-----------|-------------|
| **Headings** | Playfair Display | Crimson Pro (or Playfair) | Playfair Display |
| **Body/UI** | Inter | Inter | Inter |

### Rules
- Sentence case for headings (never all-caps except overlines)
- Playfair/Crimson for personality, Inter for clarity
- No bold body text — use medium weight (500) for emphasis

---

## Platform-Specific Guidelines

### N4S (Advisor)
- Full brand guide in N4S repo: `docs/N4S-BRAND-GUIDE.md`
- Custom CSS with CSS variables (no framework)
- Module color system: "Soft Pillow" palette for module headers
- Three-column layout pattern

### Luxebrief (Client)
- Design guidelines in Luxebrief repo: `design_guidelines.md`
- shadcn/ui + Tailwind CSS
- Apple HIG-inspired with luxury refinements
- Single-question-per-screen flow pattern

---

## Status

This universal brand guide is a **work in progress** under the BRAND topic. The full version will:
- Harmonize N4S and Luxebrief visual systems
- Define shared component patterns
- Establish cross-product consistency rules
- Cover Parker AI visual identity
- Define report and PDF standards that apply across both apps

Currently, each app has its own design guide. The goal is one canonical source that both reference.

---

*This file will be expanded as the BRAND topic progresses. See `topics/BRAND.md` for current status.*
