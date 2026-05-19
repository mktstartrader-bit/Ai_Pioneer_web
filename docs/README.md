# Documentation

Reference docs for the STARTRADER AI Pioneer Program landing page.

| File | What it covers |
|---|---|
| [program-overview.md](program-overview.md) | The program itself — pillars, offer, journey, judging, awards |
| [brand-guide.md](brand-guide.md) | Colors, gradients, typography, voice |
| [assessment-questions.md](assessment-questions.md) | All 31 assessment questions, grouped by section |
| [deployment.md](deployment.md) | How to deploy `index.html` (GitHub Pages, Netlify, Vercel, S3) |

See also: [`../specs/`](../specs/) for design and form specs, [`../assets/`](../assets/) for extracted images.

## Known inconsistencies in the current build

- **Question count:** `README.md` says "30-question assessment" but the `QUESTIONS` array in `index.html` contains 31 entries (Q1–Q31). The form UI strings say "31".
- **Hero callout:** The bottom-right hero callout displays "10 Assessment Questions" — also stale relative to the 31-item array.

Fix either the copy or the data before launch.
