# Application Form Specification

The application form is a two-step flow inside `section.form-section#apply`. State is held in a single module-level `state` object inside the inline `<script>` in `index.html`.

## State shape

```js
state = {
  name: "",
  phone: "",
  email: "",
  detailsSubmitted: false,
  answers: {},          // { [questionId]: "A" | "B" | "C" | "D" | "<text>" }
  currentIndex: 0,      // index into QUESTIONS[]
  submitting: false,
  submitted: false,
}
```

## Step 1 — Personal details

Visible elements: name, phone, company email, "Continue to Assessment →" button.

### Validation (on Continue click)

| Field | Rule | Error toast |
|---|---|---|
| Full name | `.trim().length >= 2` | "Please enter your full name." |
| Phone | `.trim().length >= 6` | "Please enter a valid phone number." |
| Email — format | `/^[^\s@]+@[^\s@]+\.[^\s@]+$/` | "Please enter a valid company email address." |
| Email — domain | `/@(startrader\|starprime)\.com$/i` | "Only @startrader.com or @starprime.com emails are allowed." |

All checks gate progression; the first failure shows a toast and aborts.

On success:
- `state.detailsSubmitted = true`
- Hide `#infoCard`, show `#assessShell`, `#submitRow`, `#progressBar`
- Render the first assessment question and scroll smoothly to it

## Step 2 — Assessment

31 questions across 3 sections (see [`../docs/assessment-questions.md`](../docs/assessment-questions.md)).

### Per-question card

Header line shows:
- Left: `Section {n} of 3` + section title
- Right: `Question {indexInSection} of {sectionTotal} · Q{id} / 31`

### Multiple-choice (`type: "mc"`)

- Four lettered options (A/B/C/D) — Q31 has only A/B/C.
- Selecting an option:
  1. Writes the letter into `state.answers[q.id]`
  2. Calls `updateProgress()`
  3. **Auto-advances** to the next question (smooth scroll). On the last question, re-renders in place.

### Open-ended (`type: "open"`)

- Single `<textarea>` with `maxlength` of `q.maxLength` (defaults to 2000).
- Character counter below: `{n} / {max}`. The `.warn` class is applied when `n > max * 0.9`.
- "Next Question →" button stays disabled until the field has non-whitespace content.
- No auto-advance — user must click Next.

### Navigation

- "← Previous" button enabled when `currentIndex > 0`.
- "Next Question →" button enabled when the current question has an answer (MC: any option selected; Open: non-whitespace text).
- Both navigation transitions scroll-into-view the assessment card with `behavior: "smooth"`.

## Progress bar

Always reflects `answeredCount() / QUESTIONS.length`:

```
progressFill.style.width = pct + "%"
progressPct.textContent  = pct + "%"
progressStep.textContent = state.detailsSubmitted ? "Progress" : "Step 1 of 2"
```

## Submit button

States, based on `answeredCount() === QUESTIONS.length`:

| State | Disabled | Label |
|---|---|---|
| Some unanswered (`n < 31`) | yes | `Answer {31 - n} more question{s} to submit` |
| All answered | no | `Submit Application` |
| Submitting | yes | `Submitting…` |

### On submit click

1. If `answeredCount() < total`: jump to the first unanswered question, scroll to it, show toast `"Please answer all 31 questions before submitting."` and abort.
2. Set `state.submitting = true`, disable button, label "Submitting…".
3. Build payload:
   ```json
   {
     "name": "...",
     "phone": "...",
     "company_email": "...",
     "answers": { ... },
     "created_at": "2026-05-19T..."
   }
   ```
4. Push to `localStorage` key `startrader_applications` (array of all submissions). Failures are swallowed (storage may be blocked).
5. After 700ms: hide `#formShell` and `#progressBar`, show `#successScreen`, scroll it into view.

## Success state

```
✓
Application Submitted

Thank you for applying to the STARTRADER AI Pioneer Program.
Your application will be reviewed by Peter and the STARTRADER AI expert team.
We'll be in touch.
```

## Toast component

Container: `#toast`, classes `.show` and (for success) `.success-toast`. Auto-dismisses after 3 seconds.

Triggered from validation errors and the "submit before complete" guard.

## Currently *not* implemented

- No server-side submission — see [`../docs/deployment.md`](../docs/deployment.md) for the suggested Supabase wiring.
- No reCAPTCHA / bot protection.
- No resume-where-you-left-off across reloads (state is in-memory only; only the final payload is persisted to localStorage on submit).
- No multi-device sync.
- No analytics events.

