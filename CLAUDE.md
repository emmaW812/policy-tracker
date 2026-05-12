# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project overview

A static HTML/CSS/JS site tracking US democratic backsliding through an analytical, historically-grounded framework. No build system, no package manager, no backend — open HTML files directly in a browser. D3.js is loaded from CDN (`cdn.jsdelivr.net/npm/d3@7`).

## Development

```bash
open index.html          # open any page directly in browser
open timeline.html
open propaganda.html
```

No build, lint, or test commands exist. The site is plain HTML files served from the filesystem.

## Architecture

### File structure
- `style.css` — all shared styles; every page links to this
- `index.html` — landing page with a single sample event card
- `timeline.html` — D3 scatterplot + vertical timeline with the 3-phase framework
- `propaganda.html` — mechanism taxonomy, filterable event feed, rights trackers, placeholder charts

### Shared CSS variables (defined in `style.css`)
Two separate color systems exist and must stay consistent across pages:

**Phase colors** (used on timeline and classification framework):
- `--phase1` `#4a7fc1` blue — Preconditions
- `--phase2` `#d4a017` amber — Emergence
- `--phase3` `#c0392b` red — Consolidation

**Mechanism/group colors** (defined locally in `propaganda.html`, will be needed on other pages):
- `--mech-prop` `#7c3aed` purple — propaganda mechanisms
- `--mech-coerce` `#dc2626` crimson — coercive mechanisms
- `--mech-inst` `#0369a1` sky — legal/institutional mechanisms
- `--grp-women` `#db2777`, `--grp-lgbtq` `#0d9488`, `--grp-press` `#d97706`, `--grp-immig` `#ea580c`, `--grp-oppo` `#64748b`

When these colors are needed on additional pages, move them from `propaganda.html` into `style.css`.

### Component patterns
Each page uses a `<style>` block for page-specific styles on top of `style.css`. Reusable patterns to follow:

- **`.pill`** — small inline tag; add a class for the color system (`.pill.prop`, `.pill.women`, etc.)
- **`.section-label`** — small all-caps blue label above each section
- **`.placeholder-wrap`** — dashed-border container with `.placeholder-banner` for any coming-soon section; always include "Placeholder — [description] coming in v2" text
- **Nav bar** — duplicated in every HTML file; the active page sets `class="active"` on its own link

### Data pattern
All data is hardcoded as JS arrays in `<script>` blocks within each page. Events have a consistent shape:
```js
{ id, date, phase, theme, title, summary, source }
```
The `date` field is `"YYYY-MM-DD"` and parsed with `d3.timeParse("%Y-%m-%d")`.

### Planned pages (not yet built)
Nav links exist for: Environment, Militarized Tech, Monopolies, Hope & Resilience, Comparators, Methodology.

### Tone and framing constraints
- Historical comparisons are always labeled explicitly as historical comparisons
- Placeholder sections are visually distinct (dashed border, muted opacity, banner label)
- The framework is analytical, not editorial — language in copy should reflect this
