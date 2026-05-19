# Deployment

`index.html` is a single, self-contained file. All CSS, JavaScript, and images are inlined as base64 / data URIs. There is no build step and no runtime dependency apart from Google Fonts.

## GitHub Pages

1. Push the repo to GitHub.
2. Open **Settings → Pages**.
3. Source: deploy from `main`, root folder.
4. Save. Site goes live at `https://<owner>.github.io/<repo>/`.

## Any static host

Drop `index.html` on:

- Netlify (drag-and-drop deploy)
- Vercel (`vercel --prod`)
- Cloudflare Pages
- AWS S3 + CloudFront
- Any plain HTTP server

No environment variables, no secrets, no API keys.

## What runs in the browser

| Behavior | Mechanism |
|---|---|
| Countdown to May 29, 2026 23:59:59 GMT+4 | `setInterval(tickCountdown, 1000)` reading `Date.now()` |
| Reveal-on-scroll | `IntersectionObserver` adding `.in` to `.reveal` |
| Form submission | Stored in `localStorage` under key `startrader_applications` |

## Wiring submissions to a real backend

Form submissions today are persisted only to `localStorage`. To send them somewhere real, replace the `localStorage.setItem(...)` call inside `submitBtn`'s click handler (in `index.html`) with your backend call. The payload shape is:

```json
{
  "name": "Jane Smith",
  "phone": "+971 50 000 0000",
  "company_email": "jane@startrader.com",
  "answers": { "1": "A", "2": "B", "22": "free text...", "...": "..." },
  "created_at": "2026-05-19T08:30:00.000Z"
}
```

Suggested integration (per the project README): Supabase

```js
await supabase.from('applications').insert(payload);
```

## Post-deploy checklist

- [ ] Verify the countdown shows the correct remaining time in GMT+4
- [ ] Test step 1 form validation (name, phone, email domain `@startrader.com` or `@starprime.com`)
- [ ] Complete the assessment end-to-end and confirm submission stores the payload
- [ ] Check OpenGraph / Twitter card preview rendering
- [ ] Confirm hero callout copy matches actual question count (currently inconsistent — see `docs/README.md`)
