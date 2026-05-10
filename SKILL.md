---
name: rinex-merger-design
description: Use this skill to generate well-branded interfaces and assets for RINEX Merger — a browser-based GNSS survey utility for merging and resampling RINEX 2.11 observation files. Contains essential design guidelines, colors, type, fonts, assets, and UI-kit components for prototyping or production work.
user-invocable: true
---

Read the `README.md` file within this skill, and explore the other available files.

If creating visual artifacts (slides, mocks, throwaway prototypes, etc), copy assets out of `assets/`, link to `colors_and_type.css`, and create static HTML files for the user to view. If working on production code, you can copy the assets and read the rules here to become an expert in designing with this brand.

If the user invokes this skill without any other guidance, ask them what they want to build or design, ask some questions (audience, surface, level of fidelity, what variations they want to explore), and act as an expert designer who outputs HTML artifacts _or_ production code, depending on the need.

## Quick reference

- **Vibe:** clean white minimalist, surveyor-orange accent, low-contrast topographic contour pattern as page texture. Calm, technical, precise. Not industrial. No emoji.
- **Primary accent:** `#E55A1F` (orange-500). One per visual block, max.
- **Typography:** Geist (sans) + Geist Mono. Mono is used for file names, log lines, epoch counts, and dates.
- **Layout:** white cards on a `#FAFAF7` page wash with a fixed full-bleed `assets/contour-bg.svg` background. 12 px radius cards with 1 px ink-200 borders; almost no shadow.
- **Tone:** imperative, direct, technical. *"Drop .26o files here"*, *"Merge files"*, *"No epochs remain after resampling."* Never *"awesome"*, *"powerful"*, or 🎉.

## File map

- `README.md` — full visual + content fundamentals.
- `colors_and_type.css` — token + semantic CSS (drop into any `<link>`).
- `assets/contour-bg.svg`, `logo.svg`, `mark.svg`, `logo-mono.svg` — copy these out, do not redraw them.
- `preview/` — Design System tab cards. Useful as visual reference; not import targets.
- `ui_kits/rinex-merger/` — clickable JSX recreation of the app. Use components from `components.jsx` as the starting point for any new RINEX Merger surface.
