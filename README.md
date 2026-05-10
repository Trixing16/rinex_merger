# RINEX Merger Design System

A design system for **RINEX Merger** — a browser-based GNSS survey utility that lets mine surveyors merge and resample RINEX 2.11 observation files locally, without uploading anything.

The product is a single-screen tool: drag in `.26o` / `.rnx` files, pick an output interval (AUSPOS expects 30 s), watch the processing log, and download the merged file. Everything runs in-browser.

This system is a **redirection** of the original cyberpunk-styled prototype into a clean, professional, surveyor-friendly visual language: white space, a single confident orange accent, and topographic contour line motifs that nod to the mapping/surveying context.

## Sources

- **Codebase:** `Trixing16/rinex_merger` ([GitHub](https://github.com/Trixing16/rinex_merger)) — single `index.html`, no build step. The original used Barlow + Share Tech Mono on a dark `#0a0e14` panel layout with cyan/green accents. We kept the **functional surface** (drop zone, file list, interval radios, processing log, result card, download button) and rebuilt the **visual language** from scratch per the brief.
- **Brief:** Clean white minimalist, primary accent orange, topographic / contour-line pattern as a subtle background or decorative element, plenty of whitespace, sans-serif (nothing heavy or industrial).

## Index

Root files:

- `README.md` — this file. Product context, content fundamentals, visual foundations, iconography.
- `SKILL.md` — agent skill manifest. Cross-compatible with Claude Code.
- `colors_and_type.css` — design tokens (colors, type ramp, spacing, radii, shadows, motion) as CSS variables, plus semantic element styles.
- `fonts/` — local fallbacks (none currently — fonts are loaded from Google Fonts; see Visual Foundations).
- `assets/` — logos, the contour-line topographic SVG, and any other static visual assets.
- `preview/` — Design System tab cards (one HTML file per concept). Registered as assets so they render in the Design System pane.
- `ui_kits/rinex-merger/` — the application UI kit (full clickable mock + JSX components). Open `index.html`.

---

## CONTENT FUNDAMENTALS

The product is a **technical utility for working surveyors**, not a consumer app. Copy is precise, declarative, and short. It does not try to be friendly — it tries to be *correct*.

### Voice

- **Direct.** Imperative verbs. "Drop files here." "Merge files." "Download merged file."
- **Technical, but unpretentious.** Use the real domain words — *epoch*, *interval*, *RINEX 2.11*, *AUSPOS*, *observation file*, *resample* — without softening them. Surveyors know what these mean. Don't explain them in body copy; explain them once in a hint if at all.
- **No hype.** No "blazing", "powerful", "smart". The tool's value is correctness and locality, not adjectives.
- **Quietly reassuring on data handling.** Mention "All processing happens locally in your browser — no data is uploaded anywhere." once, plainly. Don't repeat it.

### Person & address

- **Second person ("you")** for instructions and hints: *"Files are filtered to epochs where seconds % interval = 0."*, *"AUSPOS requires 30 s."*
- **First person plural ("we") is never used.** This is a tool, not a company speaking.
- **Imperative mood** for actions: *Merge files*, *Download merged file*, *Clear all*.

### Casing

- **Sentence case for everything user-facing.** Headings, buttons, labels, hints. *"Output settings"*, not *"OUTPUT SETTINGS"* or *"Output Settings"*.
- **One exception:** small section / overline labels use UPPERCASE TRACKED tracking-wide (`letter-spacing: 0.12em`), as a typographic device, not a copy choice. *INPUT FILES*, *PROCESSING LOG*. Treat these as visual labels — keep them short (1–3 words) and never end with punctuation.
- **Units stay lower-case and tight to numbers:** `30s`, `1.2 MB`, `4.8 hrs`. No space before `s` for seconds in compact UI; a space is fine in long-form prose.

### Tone examples

| Don't | Do |
|---|---|
| "Drag and drop your awesome RINEX files here!" | "Drop `.26o` or `.rnx` files here" |
| "Merge complete! 🎉 Your file is ready." | "Merge complete · 2,880 epochs · 1.2 MB" |
| "Oops — something went wrong." | "No epochs remain after resampling." |
| "Powerful, blazing-fast in-browser merging." | "Merge and resample RINEX 2.11 files locally." |
| "Click here to download." | "Download merged file" |

### Numbers, units, paths

- File extensions are written with a leading dot in mono: `.26o`, `.rnx`, `.obs`. Pluralize in plain text: *".26o files"*.
- Counts are bare integers, comma-separated for thousands: `2,880 epochs`, `12 files`.
- Times in the result panel are ISO-shaped, space-separated date and time, no timezone: `2026-05-09 04:00:00`. Surveyors live in GPS time; we don't decorate it.
- Status glyphs in the log are typographic, not emoji: `✓` for ok, `✗` for error, `⚠` for warn, `//` as a comment / heading prefix.

### Emoji

**No emoji anywhere.** The brand uses minimal Unicode glyphs (`✓ ✗ ⚠ ⊕ ⬇ ↻ //`) as functional indicators in the log and on buttons, but never decorative emoji. If you find yourself reaching for 🚀 or 📂, replace it with a Lucide icon or a typographic glyph.

---

## VISUAL FOUNDATIONS

The system is **white-first, orange-accented, contour-textured**. The page should read like a clean technical document with a single piece of energy — the orange — and a single piece of place — the contour lines.

### Colors

A small, confident palette. One accent does all the heavy lifting; everything else is a near-neutral.

- **Surveyor orange `#E55A1F`** (primary). Used for: the active state of controls, the merge button, the inline `// RINEX MERGER` wordmark accent, focus rings, the progress bar fill, and key numerical results. **Never use orange for body text or for more than one element per visual block.**
- **Orange tint `#FDF1EB`** for hovered drop-zone fill and result-card background.
- **Ink scale (neutrals)** drawn from a near-zinc cool-gray ramp: `#0F1115` (primary text), `#3F4147` (secondary), `#71757C` (muted, hint copy, log timestamps), `#D4D6DA` (borders/dividers), `#ECEDF0` (subtle fills), `#F6F6F4` (page wash).
- **Surface white `#FFFFFF`** for cards. The page itself is the slightly warmer `#FAFAF7` so cards lift off it without needing shadow.
- **Semantic** kept narrow: `--ok #166534`, `--warn #B45309`, `--danger #B42318`. These appear only in log lines and badges.

The full token list and ramps live in `colors_and_type.css`.

### Type

- **Geist Sans** (Google Fonts) — body, headings, labels, buttons. Modern, neutral, slightly geometric, *not* industrial. Weights used: 400 (body), 500 (labels, buttons), 600 (headings, emphasis). Tracking: -0.01em on display sizes, normal on body, +0.12em uppercase on overlines.
- **Geist Mono** (Google Fonts) — file names, the processing log, file sizes, intervals, dates in result panel, code samples. Weight 400. Slightly muted color (`--ink-700`) so it recedes against UI chrome.
- **Fallback:** if Geist fails to load we fall back to system UI sans / system UI mono. We do **not** ship local font files in this system — the original product is a single offline `index.html`, but Google Fonts is acceptable and matches its current behaviour.

Type scale (matches the CSS):

| Role | Size / line-height | Weight |
|---|---|---|
| Display | 40 / 44 px | 600 |
| H1 | 28 / 34 px | 600 |
| H2 | 20 / 28 px | 600 |
| Body | 15 / 22 px | 400 |
| Small / hint | 13 / 20 px | 400 |
| Overline | 11 / 16 px, +0.12em, UPPERCASE | 500 |
| Mono | 13 / 20 px | 400 |

### Spacing

8 px base. Tokens: `--s-1` 4, `--s-2` 8, `--s-3` 12, `--s-4` 16, `--s-5` 24, `--s-6` 32, `--s-7` 48, `--s-8` 64. Card interior padding is `--s-5` (24 px) on small cards and `--s-6` (32 px) on the main app shell.

### Backgrounds & textures

The defining visual motif is a **topographic contour-line pattern**, hand-tuned in SVG (`assets/contour-bg.svg`).

- It sits on the **page background only** — never inside cards. Cards are flat white so the page texture frames them.
- It is **drawn at very low contrast** (`#E4E2DA` lines on `#FAFAF7`) so it reads as paper texture, not graphic.
- It is **always full-bleed** and lives behind everything via a fixed `body::before`. It does not parallax; it does not animate; it does not respond to scroll.
- It is **decorative** — no content sits on top of it where it might be miscopied as a chart.

No gradients on cards, surfaces, or text. The only soft fill is the orange-tint hover state. No glassmorphism, no blur backgrounds. No grain overlays.

### Borders, radii, dividers

- **Radii:** `--r-sm` 4 px (chips, badges, small inputs), `--r-md` 8 px (buttons, inputs, file rows), `--r-lg` 12 px (cards, drop zone). Nothing larger; no pill buttons except for status badges.
- **Borders:** `1px solid var(--ink-200)` (#ECEDF0) for cards. The drop zone uses a `1.5px` dashed `--ink-300` that turns solid orange on hover/drag.
- **Dividers:** hair-thin (`1px solid var(--ink-200)`); never colored.

### Shadows / elevation

Almost none. The system relies on **borders + page wash** for separation, not shadow.

- `--shadow-sm`: `0 1px 2px rgba(15, 17, 21, 0.04)` — only on hover lift for the merge button and download button.
- `--shadow-md`: `0 6px 24px rgba(15, 17, 21, 0.06)` — only on the result card when it appears, as a soft "this is your output" emphasis.
- No inset shadows. No colored shadows. No double-shadow stacks.

### Motion

Quiet, fast, functional.

- **Durations:** 120 ms for state changes (hover, focus), 200 ms for layout transitions (drop zone activation), 280 ms for entrance (result card, file row). Cap at 300 ms.
- **Easing:** `cubic-bezier(0.2, 0, 0, 1)` (quick out / settled in) for entrances; `ease-out` for hover.
- **Entrances:** new file rows fade + slide 4 px down. The result card fades + slides 8 px down. The progress bar fill animates width with `200ms ease-out`.
- **No bounces, no springs, no parallax.** Reduced motion turns off the slide component but keeps the fade.

### Hover & press states

- **Buttons (primary):** background darkens from `#E55A1F` to `#CC4A12` on hover. On press: no scale change, just background to `#B43F0E` and `transform: translateY(1px)` removed. Focus ring is `0 0 0 3px rgba(229, 90, 31, 0.25)`.
- **Buttons (secondary / ghost):** border darkens, fill goes to `--ink-100` on hover. No scale change.
- **Drop zone:** border becomes solid orange and fill becomes `--orange-50` (#FDF1EB) on hover and during drag.
- **File row:** border softly appears (`--ink-200`) on hover. The remove `✕` darkens to `--danger`.
- **Radio chips (interval selector):** inactive chips on hover get `border-color: --ink-300`; active is solid orange border + orange text + `--orange-50` fill.
- **Links:** underline appears on hover; color stays the same.

No element ever scales up on hover. No icon ever spins on hover.

### Transparency & blur

Not part of the system. The single tinted fill is `--orange-50`, applied as a solid color, not as `rgba(...) ` over an unknown background. The result card uses an opaque `#F8FBF7` (very faint mint) — also a solid color.

### Layout rules

- **Max content width 1100 px.** Center the app shell with auto margins.
- **App layout is two columns:** left (input + log) is fluid, right (settings + actions) is a fixed 340 px panel. Below 880 px viewport the right panel stacks beneath.
- **Header is full width**, sticky-on-scroll *off* — it scrolls with content. The page is short by design.
- **Cards never nest more than one level deep.** A card may contain field rows; it does not contain other cards.
- **Card titles** use the overline style (UPPERCASE TRACKED) and sit 24 px above their content.

### Imagery

The system has almost no imagery. The contour pattern is the only "image". If a screenshot is ever needed (docs, marketing) it should be the app itself, captured cleanly, on the page wash. No stock photography, no illustrated mascots, no abstract gradients.

### Cards

Cards are **defined by border, not shadow**. Spec:

- Background: `#FFFFFF`
- Border: `1px solid var(--ink-200)`
- Radius: `--r-lg` (12 px)
- Padding: `--s-6` (32 px) on the main app cards, `--s-5` (24 px) on smaller ones
- No hover state on cards themselves
- Card title (overline) → 24 px gap → content
- Optional terminal divider (1 px, `--ink-200`) between sections inside a card; never between cards

The only "lifted" card is the **result card**, which gets `--shadow-md` and a 1 px `var(--orange-100)` border to signal "look here, your output is ready".

### Iconography preview

Stroke icons only, 1.5 px line, rounded caps. We use **Lucide** via CDN. See ICONOGRAPHY.

---

## ICONOGRAPHY

The original codebase uses **typographic glyphs** (`⊕`, `✓`, `✗`, `⚠`, `▶`, `⬇`, `✕`) rather than icons, plus the `//` prefix as a code-style heading. We keep these in two places where they are functional, idiomatic, and screen-reader friendly with `aria-label`:

- `//` — section heading prefix in the wordmark and in the processing log (`// Ready. Load files…`)
- `✓ ✗ ⚠` — log line status indicators (paired with semantic color)
- `↻` — clear/reset button glyph

For everything else — buttons, drop zone, file rows, controls, header chrome — the system uses **[Lucide](https://lucide.dev/)** stroke icons.

- **Source:** Lucide via the official CDN (`https://unpkg.com/lucide@latest`). No local sprite, no icon font.
- **Stroke:** 1.5 px, rounded caps and joins, 24 px source size, sized down to 16 / 18 / 20 px in UI.
- **Color:** inherit `currentColor`. Default is `--ink-500`; on active controls or hover, `--ink-900` or `--orange-600` depending on the control.
- **Substitution flag:** Lucide is a substitution — the original codebase ships no icon assets. Lucide was chosen because its 1.5 px stroke and rounded geometry match the system's calm, technical, non-industrial feel; Heroicons (2 px, square caps) and Phosphor (variable weight) read as either heavier or more playful than this brand wants. **If a project owner has a preferred icon set, this is the first thing to swap.**

Specific mappings:

| Use | Lucide name |
|---|---|
| Drop zone / upload | `upload-cloud` |
| File row | `file-text` |
| Remove file | `x` |
| Clear all | `trash-2` |
| Merge / play | `play` |
| Download | `download` |
| Settings card / cog | `sliders-horizontal` |
| About / info | `info` |
| Warning badge | `triangle-alert` |
| Success | `check` |

### No emoji, ever

We do not use emoji. If a designer wants visual warmth, they should use orange or whitespace, not 🎉.

### Logo

`assets/logo.svg` — a wordmark + mark composed of:

- A small **contour-ring mark** (three concentric near-circular contours, the innermost filled orange) — a literal nod to a topo map peak.
- The wordmark **RINEX MERGER** in Geist 600, slight letter-spacing, with the `//` prefix in `--ink-500` aligned to the left.

A monochrome variant (`logo-mono.svg`) exists for dark surfaces and print. The mark alone (`mark.svg`) can be used as a favicon or app icon.
