# Kamino Cell — Radiation Emergency Manual

A single-file HTML document designed as an in-universe safety manual for colonists living on the ocean world of Kamino. It covers radiation biology, protection protocols, and emergency response — presented as a polished, editorial-quality web interface.

---

## Overview

| Property | Value |
|---|---|
| File | `kamino_emergency_manual_v5.html` |
| Type | Single-file HTML (no build step, no dependencies) |
| Revision | Rev 8.0 |
| Setting | Kamino · Tipoca Spire · Standard Year 22 BBY |

---

## Design Language

The aesthetic is inspired by clean editorial product UIs — soft translucent cards floating over a misty ocean-blue background, with frosted glass panels and generous white space. The reference direction was a right-panel floating navigation card similar to modern SaaS dashboards.

**Tone:** Refined and clinical. Authoritative without being harsh. The visual softness is intentional — it contrasts with the serious subject matter and keeps the reader calm.

---

## Colour Palette

All colours are defined as CSS custom properties on `:root`.

### Backgrounds

| Token | Hex | Use |
|---|---|---|
| `--bg` | `#c6e0ec` | Page background — misty ocean blue |
| `--bg2` | `#d4eaf4` | Lighter background tint |
| `--surface` | `rgba(255,255,255,0.72)` | Subtle surface layer |
| `--card` | `rgba(255,255,255,0.88)` | Card and panel backgrounds |
| `--nav-bg` | `rgba(255,255,255,0.82)` | Navigation card background |

### Text

| Token | Hex | Use |
|---|---|---|
| `--txt` | `#08263a` | Primary headings and strong text |
| `--txt2` | `#1c5268` | Body copy |
| `--txt3` | `#3a7a98` | Labels, captions, secondary text |
| `--txt4` | `#6aaac8` | Muted hints and placeholders |

### Accent — Kamino Teal

| Token | Hex | Use |
|---|---|---|
| `--ac` | `#0d7a96` | Primary accent — active states, highlights |
| `--ac-lt` | `#29aece` | Light accent — chart lines, animated elements |
| `--ac-dk` | `#085c72` | Dark accent — labels, borders |
| `--ac-pale` | `rgba(13,122,150,0.08)` | Hover backgrounds, tinted fills |
| `--ac-glow` | `rgba(13,122,150,0.18)` | Glow effects on the pulse dot |

### Emergency — Red Zone

| Token | Hex | Use |
|---|---|---|
| `--red` | `#bf3b2e` | Emergency zone accent |
| `--red-lt` | `#e04b3c` | Light red — alert highlights |
| `--red-dk` | `#8f2a20` | Dark red — emergency text |
| `--red-pale` | `rgba(191,59,46,0.07)` | Emergency hover backgrounds |

### Borders & Shadows

| Token | Value | Use |
|---|---|---|
| `--border` | `rgba(120,180,210,0.32)` | Default card borders |
| `--border2` | `rgba(120,180,210,0.55)` | Stronger borders, dividers |
| `--sh` | subtle two-layer drop shadow | Cards at rest |
| `--sh-md` | medium two-layer drop shadow | Cards on hover, modals |
| `--sh-lg` | strong two-layer drop shadow | Bottom banner, elevated panels |

---

## Typography

Three font families loaded from Google Fonts. Each has a specific role.

### Lora — Display & Brand
- **Source:** Google Fonts
- **Weights used:** 400, 500, 600 (upright and italic)
- **Used for:** Page title, chapter numbers, section titles, navigation brand name, nav footer ID, planet name, post-event step numbers
- **Why:** Lora's high-contrast bracketed serifs give editorial weight. The italic cuts are especially distinctive — used to inject warmth into otherwise clinical content.

### Plus Jakarta Sans — UI & Body
- **Source:** Google Fonts
- **Weights used:** 300, 400, 500, 600, 700
- **Used for:** All body paragraphs, card body text, navigation links, badges, chips, tags, callout text, table cells, footer metadata
- **Why:** Humanist sans with slightly quirky terminals. Friendlier than geometric options (Inter, DM Sans) without feeling informal.

### DM Mono — Data & Labels
- **Source:** Google Fonts
- **Weights used:** 300, 400, 500
- **Used for:** Section eyebrows, chart axis labels, stat cell labels, exposure table column headers, nav section labels, dosimeter readings, channel IDs, revision numbers
- **Why:** Narrow and precise. DM Mono reads clearly at very small sizes (down to 0.44rem) without feeling mechanical. Better rhythm than Courier or IBM Plex Mono for this scale.

---

## Layout

### Page Structure

```
body (padding-right: 220px to clear nav)
├── #progress          — top reading progress bar
├── #mainNav           — fixed right-side floating card
├── header             — centred title area
└── .wrapper           — centred content column (max-width: 900px)
    ├── #kamino-stats  — planet profile panel
    ├── #rad-meter     — live radiation meter bar
    ├── Part I         — The Threat (sections 01–04)
    ├── Part II        — Protection (sections 05–08)
    ├── Part III       — Safe Ops (sections 09–10)
    └── Part IV        — Emergency (sections 11–13)
```

### Navigation Card

Positioned `fixed`, `right: 16px`, `top: 50%`, `transform: translateY(-50%)` — vertically centred on screen at all times. The design references editorial product UIs with a floating right panel.

- Width: `220px`
- Background: frosted glass (`backdrop-filter: blur(20px) saturate(1.5)`)
- Border radius: `26px`
- Entrance animation: slides in from the right on load (`navIn` keyframe)
- Groups: Planet, I, II, III, IV — each with an italic Roman numeral, spaced-caps label, and a fading rule line
- Active link: tinted background + font-weight 600
- Emergency group: soft terracotta tint instead of full red
- Collapses off-screen on mobile (≤900px) with a hamburger toggle

### Bottom Brochure Banner

Fixed centred rectangle at the bottom of the viewport — styled like a non-intrusive notification card.

- `position: fixed`, `bottom: 18px`, horizontally centred accounting for nav width
- Width: `480px`, frosted glass, `border-radius: 14px`
- Contains: icon, title, body copy, pill tag
- Enters with `bannerUp` slide-up animation on page load (0.5s delay)
- Hides on very small screens to avoid obstruction

---

## Animations

All animations are CSS-only. No animation libraries.

| Name | Duration | Easing | Purpose |
|---|---|---|---|
| `fadeUp` | 0.6s | `ease` | Header elements appear on load (staggered 0.1s each) |
| `navIn` | 0.6s | `cubic-bezier(0.22,1,0.36,1)` | Nav card slides in from right |
| `bannerUp` | 0.7s | `cubic-bezier(0.22,1,0.36,1)` | Bottom banner slides up |
| `pulse` | 2.5s | `ease-in-out` | Nav dot and alert status dot — gentle opacity fade |
| `meterScan` | 3s | `ease-in-out` | Radiation meter fill bar animates back and forth |
| `ticker` | 22s | `linear` | Emergency alert scrolling text ticker |
| `stormRing` | 4s | `ease-out` | Expanding pulse rings around planet diagram |
| Section reveal | 0.65s | `ease` | Sections fade up as they scroll into view (IntersectionObserver) |

**Design principle:** One well-orchestrated entrance (staggered header + nav slide), then only purposeful micro-animations. No decorative loops except where they communicate live data (meter scan, pulse dot).

---

## Interactive Features

### PMAT Cell Division Diagram
Four clickable cards — Prophase, Metaphase, Anaphase, Telophase. Each card has a canvas drawing of the cell stage. Clicking any card reveals a two-column detail panel comparing **Normal Cell** behaviour vs **Radiation-Damaged Cell** behaviour. Drawn entirely with Canvas 2D API.

### Scroll Reveal
Every `<section>` starts invisible (`opacity: 0`, `transform: translateY(20px)`) and transitions to visible when it enters the viewport. Uses `IntersectionObserver` with `threshold: 0.07`.

### Reading Progress Bar
A 2px bar across the top of the page shows scroll depth. Transitions to red gradient when the Emergency section is reached.

### Active Navigation
As the user scrolls, the current section's nav link receives the `.active` class. Uses a passive scroll listener comparing `getBoundingClientRect().top` against a 120px threshold.

---

## Canvas Charts

All charts are drawn with the Canvas 2D API and use the same colour tokens as the CSS. Charts scale to their container width via a `setupCanvas()` helper that accounts for device pixel ratio.

| Chart | ID | Description |
|---|---|---|
| Radiation Penetration | `radTypeChart` | Horizontal bar showing how far Alpha, Beta, Gamma travel through matter |
| DNA Damage Types | `dnaBarChart` | Vertical bars — frequency of 4 damage types per 1 Gy dose |
| Inverse Square Law | `inverseChart` | Curve showing intensity drop vs distance with annotated points |
| Cancer Risk | `cancerChart` | Curve showing relative cancer risk vs cumulative dose, with annual limit marker |

---

## SVG Diagrams

### DNA Helix (`#dnaSVG`)
Side-by-side comparison of normal S-phase replication vs radiation-damaged DNA. Shows single-strand breaks, crosslinks, wrong base insertion, and the new strand being copied. Drawn with `createElementNS` SVG API.

### Meiosis (`#meiosisSVG`)
Two-column diagram: normal meiosis producing 4 correct gametes vs radiation-induced non-disjunction producing gametes with wrong chromosome counts. Illustrates aneuploidy.

### Planet Diagram (inline SVG in stats panel)
Kamino rendered as an ocean world with radial gradients, storm band patterns, orbital rings, a failed satellite (red dot), and a working satellite (teal dot). Storm rings animate outward using the `stormRing` keyframe.

---

## Content Structure

The manual is divided into four parts, each with a chapter banner and numbered sections.

| Part | Sections | Topic |
|---|---|---|
| I | 01–04 | Radiation on Kamino, DNA & S Phase, Mitosis & Cancer, Meiosis & Fertility |
| II | 05–08 | The Three Principles, Minimising Time, Maximising Distance, Shielding Protocols |
| III | 09–10 | Exposure Level Reference Table, Safe Operating Conditions & Daily Limits |
| IV | 11–13 | The Three Imperatives (Get In / Stay In / Stay Tuned), Post-Exposure Response, Emergency Channels |

### Emergency Zone (Part IV)
When the reader reaches Part IV, the CSS variable overrides in `.zone-emerg` shift all accent colours to the red tokens — chapter numbers, underlines, card borders, callout borders, and section number ghosts all transition to terracotta red. The extreme alert banner uses a frosted card with a scrolling ticker and a pulsing status dot.

---

## Component Reference

| Class | Type | Description |
|---|---|---|
| `.card` | Card | General info card with hover lift |
| `.safe-card` | Card | Compact stat card for limits and values |
| `.callout` | Inline block | Left-border callout with icon and bold label |
| `.explainer` | Inline block | Italic "Plain English" plain-language explanation block |
| `.rule-list` | List | Left-border rule items with icon and bold label |
| `.exposure-table` | Table | Zone reference table with colour-coded badge cells |
| `.e-step` | Emergency card | Two-column step card with large italic number |
| `.e-checklist` | List | Emergency checklist items with arrow prefix |
| `.post-card` | Card | Post-event action card |
| `.schip` | Chip | Symptom pill with warn/crit colour variants |
| `.channel-card` | Card | Emergency channel card with large channel ID |
| `.badge` | Inline | Zone level badge — safe / low / elevated / high / critical |
| `.graph-wrap` | Container | Chart wrapper with floating data-label |
| `.diagram-wrap` | Container | SVG/interactive diagram wrapper with floating pill label |

---

## Responsive Behaviour

| Breakpoint | Changes |
|---|---|
| ≤ 900px | Nav collapses off-screen, hamburger toggle appears, body padding-right removed, banner centres fully |
| ≤ 680px | Stats panel switches to single column |
| ≤ 640px | PMAT grid goes from 4 columns to 2 columns |
| ≤ 600px | Header title shrinks, all multi-column grids collapse to 1 column, wrapper padding reduced |

---

## File Notes

- Zero external JavaScript dependencies
- Zero build tooling required — open directly in any browser
- All fonts loaded from Google Fonts CDN (requires internet connection)
- Canvas charts re-draw on load; no animation frame loops running during idle
- Fully self-contained — one file, all CSS and JS inline
