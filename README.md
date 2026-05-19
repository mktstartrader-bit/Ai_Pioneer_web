# STARTRADER AI Pioneer Program

Landing page and 31-question assessment for STARTRADER's internal 2-month enterprise AI training program.

**Tagline:** Built on Trust. Driven by Growth.

## What's in this repo

- **`index.html`** — Fully self-contained landing page. All CSS, JavaScript, images, and assets are inlined as base64 / data URIs, so there is nothing else to load. Open it directly in any modern browser, drop it on any static host, or deploy via GitHub Pages.

## Sections

1. **Hero** — Headline, tagline, CTA, masked-model photo, three callouts, "STAR AGENT" watermark, registration countdown strip with live timer to **May 29, 2026 23:59:59 GMT+4**.
2. **Pillars** — *6 Qualities. Not a Job Title.* Six interactive cards (Curiosity, Learning Motivation, Innovation, Exploration, Transformation, Knowledge Sharing) with icons.
3. **Offer** — *Your AI Toolkit. Fully Sponsored.* Enterprise accounts, sandboxes, learning resources, project priority.
4. **Journey** — Seven-step alternating timeline (application → exploration → champion selection).
5. **Reviewed by the Best** — Peter Karsten, STARTRADER CEO, with the four scoring criteria (Learning Initiative 30%, Business Application 30%, AI Understanding 20%, Collaboration & Sharing 20%).
6. **Awards** — AI Leadership Award, Advanced Projects, AI Champion status.
7. **Application Form** — Two-step: personal info (name / phone / company email validation) → 31-question assessment with sticky progress, auto-advance for multiple choice, textarea character counters, and success screen.

Form submissions are written to `localStorage`. To wire them up to Supabase later, replace the `saveApplication()` function with `supabase.from('applications').insert(payload)`.

## Brand

| Color    | Hex       | Where it's used                         |
|----------|-----------|-----------------------------------------|
| Navy     | `#0D0D4B` | Section backgrounds, base               |
| Cyan     | `#16E9D7` | Accents, highlights, gradient terms     |
| Blue     | `#0047BB` | CTA, primary buttons                    |
| Mist     | `#DAE3ED` | Body text on dark backgrounds           |

Font: **Plus Jakarta Sans** (loaded from Google Fonts).

## Deploy

### GitHub Pages

1. Push this repo to GitHub.
2. Open repo **Settings → Pages**.
3. Source: deploy from `main` branch, root folder.
4. Save. Your site will be live at `https://<your-username>.github.io/AI-Pioneer/`.

### Any static host

Drop `index.html` on Netlify, Vercel, Cloudflare Pages, S3, or any web server. There are no build steps.

## License

Internal — STARTRADER © 2026.
