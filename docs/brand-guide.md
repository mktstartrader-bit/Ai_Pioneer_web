# Brand Guide

Source of truth: CSS `:root` variables in `index.html`.

## Color tokens

| Token | Hex | Usage |
|---|---|---|
| `--navy` | `#0D0D4B` | Page background, section backgrounds, brand base |
| `--deep-blue` | `#001489` | Gradient stop (trust gradient) |
| `--blue` | `#0047BB` | Primary CTA, primary buttons |
| `--cyan` | `#16E9D7` | Accents, highlights, gradient terms, selection |
| `--mist` | `#DAE3ED` | Body text on dark backgrounds |
| `--ink` | `#1C1F2A` | Dark text on light surfaces |
| `--graphite` | `#50555B` | Secondary text |
| `--sand` | `#DFC5AE` | Award accent |
| `--bronze` | `#AC7C59` | Award accent |
| `--silver` | `#A0A8AE` | Award accent |

## Gradients

| Token | Definition | Where it's used |
|---|---|---|
| `--gradient-momentum` | `linear-gradient(135deg, #0D0D4B 0%, #0047BB 50%, #16E9D7 100%)` | Hero, CTAs, marquee gradients |
| `--gradient-trust` | `linear-gradient(180deg, #0D0D4B 0%, #001489 100%)` | Section gradients |
| `--gradient-growth` | `linear-gradient(90deg, #0047BB 0%, #16E9D7 100%)` | Progress, accent strips |

### Animated gradient text

`.gradient-text` uses `linear-gradient(120deg, #16E9D7 0%, #7BFFEF 50%, #16E9D7 100%)` with a `gradient-shift` keyframe (8s loop). Used on the second line of every section title (e.g. "Not a Job Title.", "Fully Sponsored.", "Curious to Champion.").

## Typography

- **Font family:** Plus Jakarta Sans (loaded from Google Fonts), fallback `system-ui, -apple-system, "Segoe UI", sans-serif`
- **Weights loaded:** 300, 400, 500, 600, 700, 800
- **Body:** 400, line-height 1.5, antialiased
- **Section titles:** `clamp(2.25rem, 5.5vw, 4rem)`, weight 800, letter-spacing -0.02em, line-height 1.05
- **Eyebrow:** uppercase, 0.72rem, letter-spacing 0.25em, weight 700, cyan

## Decorative system

- `.dot-grid` — radial-dot pattern at 24px × 24px, 6% mist over dark backgrounds. Used on Pillars, Journey, Judges sections.
- `.glow` — `text-shadow: 0 0 24px rgba(22,233,215,.45)` for the Judges eyebrow.
- `::selection` — cyan background, navy text.
- "STAR AGENT" hero watermark — large faint text behind the hero content.

## Voice

- **Tagline:** Built on Trust. Driven by Growth.
- **Hero promise:** Learn Faster. Think Bigger. Build Smarter.
- Headlines use a *two-line pattern*: a plain first line + a gradient-text second line that completes the thought.
  - "6 Qualities. / Not a Job Title."
  - "Your AI Toolkit. / Fully Sponsored."
  - "7 Steps. / Curious to Champion."
  - "Reviewed by / the Best."
  - "AI Leadership / Award"
