# Insurance Pre-Licensing Study Planner

A free, interactive study planning tool that generates personalized pre-licensing study calendars for insurance professionals. Built by [Aceable Insurance](https://insurance.aceable.com).

## What It Does

Users answer 5 quick questions about their license type, state, life situation, schedule preferences, and timeline — then get a fully customized study plan they can download directly to their calendar app.

### Features

- **Personalized Study Calendar** — Sessions mapped to specific dates and times based on the user's availability, with topics assigned to each session
- **All 50 States + DC** — Accurate pre-licensing hour requirements by state and license type (P&C, Life, Health, Life & Health, Personal Lines, All Lines)
- **Life-Aware Scheduling** — Adjusts pacing for working parents, caregivers, students, and other life situations
- **Goal Date Aware** — Distributes study hours to fit within the user's target exam date
- **.ICS Calendar Export** — Downloads all sessions as a single file compatible with Google Calendar, Apple Calendar, Outlook, and any standard calendar app
- **Exam Content Flashcards** — Tap-to-reveal flashcard deck covering key terms for each license type, with printable PDF download
- **Study Topics Mapped to Sessions** — Full exam content outline broken into categories and matched to the user's schedule
- **State Exam Snapshot** — Passing score, number of questions, time limit, and test provider for the user's state
- **Exam Day Checklist** — What to bring, when to arrive, pacing tips
- **Personalized Study Tips** — Advice tailored to the user's life situation (working parent tips, student tips, etc.)
- **Optional Email Gate** — Toggle lead capture on/off with a single config variable

## Quick Start

This is a single HTML file with zero dependencies. No build step, no npm, no framework.

### Option 1: Open Locally
```
Just open index.html in any browser.
```

### Option 2: GitHub Pages
1. Push this repo to GitHub
2. Go to **Settings → Pages**
3. Set source to **main branch**, root folder
4. Your tool will be live at `https://yourusername.github.io/aceable-study-planner/`

### Option 3: Embed on Your Site
```html
<iframe src="https://yourusername.github.io/aceable-study-planner/" 
        width="100%" 
        height="800" 
        frameborder="0"
        style="max-width: 720px; margin: 0 auto; display: block;">
</iframe>
```

Or simply copy `index.html` into your CMS or hosting platform.

## Configuration

### Email Gate (Lead Capture)

At the top of the `<script>` block in `index.html`:

```javascript
const GATE = false; // Set to true to require email before showing results
```

When `GATE = true`, users must enter their email before seeing their study plan. The email is logged to the browser console — connect it to your CRM/email platform by replacing the `console.log` in `submitGate()` with your API call:

```javascript
// In submitGate(), replace:
console.log('Lead:', { email, name });

// With your integration, e.g.:
fetch('https://your-api.com/leads', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ email, name, state: S.st, license: LIC[S.lic].l })
});
```

### Customizing State Data

State requirements are in the `ST` object. Each state has:
- `n` — State name
- `pc`, `life`, `health`, `lh`, `pl` — Hours by license type (0 = no mandate)
- `qs` — Approximate exam question count
- `pass` — Passing score percentage
- `time` — Exam time limit in minutes
- `prov` — Test provider (PSI or Pearson VUE)
- `nt` — Optional note displayed to users

### Customizing Flashcards & Topics

The `FC` and `TOPICS` objects contain all flashcard and study topic data, organized by license type (`pc`, `life`, `health`). Combined license types (`lh`, `pl`, `pclh`) are auto-generated from these base sets.

## File Structure

```
aceable-study-planner/
├── index.html    ← The entire tool (single file, zero dependencies)
├── README.md     ← This file
└── LICENSE       ← MIT License
```

## Tech Stack

- Vanilla HTML/CSS/JS — no frameworks, no build tools
- Google Fonts (DM Sans + Fraunces) — loaded via CDN
- .ICS generation — built-in, spec-compliant calendar export
- Flashcard PDF — generated in-browser via print dialog

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). Mobile responsive.

## License

MIT — see [LICENSE](LICENSE) for details.

---

Built by [Aceable Insurance](https://insurance.aceable.com)
