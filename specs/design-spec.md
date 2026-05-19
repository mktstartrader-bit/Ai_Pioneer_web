# Design Specification

## Page architecture

Single document. All sections render in this order:

1. **Topbar** (`.topbar`) — absolute-positioned over the hero. Contains STARTRADER logo only.
2. **Hero** (`section.hero`) — full-viewport min-height, background image (`assets/images/hero-bg.webp`), large "STAR AGENT" watermark, two-column layout (text left, model photo right with 3 floating callouts), bottom countdown strip.
3. **Pillars** (`section.pillars`) — 6 interactive cards rendered from `PILLARS[]`. The hovered/focused/clicked card becomes the `.is-active` one; the others recede.
4. **Offer** (`section.offer`) — two-column: left card lists 4 items from `OFFER[]`, right card is the "2 months" donut feature with two orb decorations.
5. **Journey** (`section.journey`) — Alternating left/right timeline driven by `JOURNEY[]` (7 entries). Each row has a numbered dot and a card.
6. **Judges** (`section.judges`) — Centered portrait of Peter Karsten flanked by 4 criterion cards (20% / 20% on left column, 30% / 30% on right), with quote underneath. Background uses the same `hero-bg.webp` asset.
7. **Awards** (`section.awards`) — Centered "AI Leadership Award" headline with 3 icon-cards (🏆, 🚀, ⭐) and a repeat CTA.
8. **Application form** (`section.form-section#apply`) — see [form-spec.md](form-spec.md).
9. **Footer** (`footer.footer`) — Logo, tagline, copyright year (rendered via JS).

## Section padding

```css
.section-pad { padding: 5rem 0 6rem; }
@media (min-width: 768px) { .section-pad { padding: 7rem 0 8rem; } }
```

Container: `width: 100%; max-width: 1200px; margin-inline: auto; padding-inline: 1.5rem;`

## Typography rhythm

- **Eyebrow** above every section title: uppercase, 0.25em tracking, cyan.
- **Section title**: clamp(2.25rem, 5.5vw, 4rem). Almost always rendered as two `<h2>` lines — the second uses `.gradient-text` and completes the thought.

See [`../docs/brand-guide.md`](../docs/brand-guide.md) for all colors, gradients, and font.

## Hero callouts

Three floating absolute-positioned chips overlaid on the model photo:

| Position | Big number | Label | SVG connector line |
|---|---|---|---|
| Top-right (`.callout-tr`) | `10 Ai` | Pioneer Awards | none |
| Middle-left (`.callout-ml`) | `2 mo` | Enterprise Access | line goes right then up |
| Bottom-right (`.callout-br`) | `10` | Assessment Questions | line goes left then up |

> ⚠️ The bottom-right callout reads "10 Assessment Questions" but `QUESTIONS[]` has 31 entries. Update one or the other before launch.

## Countdown strip (bottom of hero)

- Label: "Registration Countdown"
- 4 digit groups: Days / Hours / Minutes / Seconds (zero-padded to 2 digits)
- Deadline copy: "Deadline: May 29, 2026 · 23:59:59 GMT+4"
- 3 trailing features with SVG icons: **Learn Faster**, **Think Bigger**, **Build Smarter**
- When the deadline passes, label changes to "Applications Closed" and all digits show `00`.

Implementation: `const DEADLINE = new Date("2026-05-29T23:59:59+04:00").getTime();` ticked every second.

## Motion

### Reveal-on-scroll

Every element with class `.reveal` is observed by an `IntersectionObserver` at threshold 0.12. Once intersecting, the class `.in` is added and the observer disconnects from that element.

### Animated gradient text

`.gradient-text` runs the `gradient-shift` keyframe over 8 seconds, infinite ease.

### Pillar active state

The first pillar is active on load. Pillars become active on `mouseenter`, `focus`, or `click`.

## Decorative system

- `.dot-grid` overlay on Pillars, Journey, Judges (opacity 0.2–0.35).
- `.glow` text-shadow on the Judges eyebrow.
- `.orb-big` and `.offer-feature-orb-*` are soft radial glows behind the Awards and Offer feature card.
- Hero contains a large faint "STAR AGENT" watermark element (`.hero-watermark`).

## Responsive

- Single explicit breakpoint at `min-width: 768px` (controls topbar padding and section padding).
- Most sizing relies on `clamp()` and flex/grid intrinsic layout. The hero grid, pillar grid, offer grid, and timeline are responsive by CSS rules already in `index.html`.
- Test at: 360px (small phone), 768px (tablet), 1280px (desktop), 1600px+ (large desktop).

## Browser compatibility

- Uses `IntersectionObserver` (no fallback) — IE11 and older not supported.
- WebP images for photos; PNG for favicon. All decoded inline at load time.
- Google Fonts loaded via `<link rel="preconnect">` then a stylesheet `<link>`.

## Accessibility notes

- Hero model photo has `alt=""` (decorative).
- Callouts marked `aria-hidden="true"`.
- Countdown container has `aria-live="polite"`.
- Toast container has `role="status"` and `aria-live="polite"`.
- Form inputs all have associated `<label for="...">`.
- All interactive pillar elements are `<button type="button">` (not `<div>`).
- Color contrast: cyan-on-navy passes WCAG AA for large text; verify body copy contrast if the design changes.

## Assets

See [`../assets/README.md`](../assets/README.md) for the inventory of extracted images and where each one is referenced.
