# IS Career Launchpad

A single-file, no-build HTML/CSS/JS prototype built for the BYU IS Junior Core Case Competition ("IS Career Launchpad"). Everything lives in **`index.html`** — no server, no build step, no dependencies. Open it directly in any browser, or host it for free on GitHub Pages.

## What's in it

1. **Career Path Discovery** — 8 IS career paths (Software/App Developer, Business/Systems Analyst, Data Analyst/Data Scientist, Cybersecurity Analyst, IT Project Manager, UX Designer/Product Manager, ERP/Systems Consultant, Cloud/Infrastructure Engineer). Each path page covers what makes it unique, day-to-day work, technical skills, entry-level expectations, sourced salary/growth data, what makes a strong candidate, and which BYU IS Junior Core classes prepare you for it.
2. **"Find My Path" quiz** — 10 questions, deterministic point-based scoring (no external AI call), matches the user to a best-fit career path (or paths, on a tie).
3. **Interview Prep** — for all 8 paths, real behavioral + technical interview questions researched from Glassdoor candidate reports, DataLemur/InterviewQuery, Exponent, and other public interview-prep sources, each with a written model answer. Also includes a **working, rule-based feedback engine** ("Get Feedback on My Answer") that gives real, specific coaching on whatever the user types — no AI model, API key, or network call required — built to be swapped for a real AI model later without changing the UI.

## How to edit it

Everything is data-driven at the top of the `<script>` block in `index.html`:

- **`PATHS`** array — one object per career path. Edit `courses` here to swap in real BYU IS Junior Core course numbers/names once finalized (currently placeholders, clearly flagged on each career page).
- **`INTERVIEW`** object — behavioral/technical questions, model answers, and (for technical questions) a `keyTerms` list used by the feedback engine per path.
- **`QUESTIONS`** array — the 10 quiz questions and their point values per path (each answer option awards points to one or more paths via the `points` object).

No build tools needed — edit the file, refresh the browser.

## How the interview feedback works right now

Clicking "Get Feedback on My Answer" does **not** call an AI model — it runs a small rule-based checker entirely in the browser (`buildBehavioralFeedback()` / `buildTechnicalFeedback()` in `index.html`), the same way the quiz scoring works. For a behavioral question it checks the answer against the STAR framework (does it set up a situation, describe a specific action with "I," and end with a concrete result). For a technical question it checks the answer against a curated `keyTerms` list attached to that question, plus whether the answer includes a concrete example and explains *why*, not just *what*. It returns real "what's working" / "what to improve" feedback either way — there's nothing to configure, and it works with zero setup, no API key, and no internet connection.

## Wiring in a real AI model later (optional)

The rule-based engine above is fully functional on its own and satisfies the assignment's feedback requirement without any external dependency. If you want to upgrade it to a real AI model later, replace the body of the `getFeedback()` function near the bottom of the script with a `fetch()` call to your model/API endpoint (passing the question text and the user's typed answer), and render the response in place of the `buildBehavioralFeedback()`/`buildTechnicalFeedback()` output. The surrounding UI (the panel, the "Show Model Answer" comparison) needs no changes.

## Publishing to GitHub Pages

See the step-by-step instructions provided separately (or in the chat) — short version:

```bash
git init
git add index.html README.md
git commit -m "Initial IS Career Launchpad prototype"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo-name>.git
git push -u origin main
```

Then in the repo on GitHub: **Settings → Pages → Source: Deploy from a branch → Branch: main / (root)** → Save. Your live link will appear at `https://<your-username>.github.io/<your-repo-name>/` within a minute or two.

## Data sources

- U.S. Bureau of Labor Statistics, Occupational Outlook Handbook (bls.gov/ooh)
- Glassdoor salary and interview-question data
- Payscale, Salary.com, ZipRecruiter salary data
- DataLemur / InterviewQuery (SQL/data-analyst interview questions)
- Exponent (product manager / UX designer interview questions)

Every salary figure on a career page links directly to its source.
