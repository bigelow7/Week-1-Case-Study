# IS Career Launchpad

A single-file, no-build HTML/CSS/JS prototype built for the BYU IS Junior Core Case Competition ("IS Career Launchpad"). Everything lives in **`index.html`** — no server, no build step, no dependencies. Open it directly in any browser, or host it for free on GitHub Pages.

## What's in it

1. **Career Path Discovery** — 8 IS career paths (Software/App Developer, Business/Systems Analyst, Data Analyst/Data Scientist, Cybersecurity Analyst, IT Project Manager, UX Designer/Product Manager, ERP/Systems Consultant, Cloud/Infrastructure Engineer). Each path page covers what makes it unique, day-to-day work, technical skills, entry-level expectations, sourced salary/growth data, what makes a strong candidate, and which BYU IS Junior Core classes prepare you for it.
2. **"Find My Path" quiz** — 10 questions, deterministic point-based scoring (no external AI call), matches the user to a best-fit career path (or paths, on a tie).
3. **Interview Prep** — for all 8 paths, real behavioral + technical interview questions researched from Glassdoor candidate reports, DataLemur/InterviewQuery, Exponent, and other public interview-prep sources, each with a written model answer. In supported Chrome browsers, the **built-in Prompt API** uses Gemini Nano to generate personalized feedback entirely on the user's device. Other browsers automatically receive the existing rule-based feedback, so the module remains functional everywhere.

## How to edit it

Everything is data-driven at the top of the `<script>` block in `index.html`:

- **`PATHS`** array — one object per career path. Edit `courses` here to swap in real BYU IS Junior Core course numbers/names once finalized (currently placeholders, clearly flagged on each career page).
- **`INTERVIEW`** object — behavioral/technical questions, model answers, and (for technical questions) a `keyTerms` list used by the feedback engine per path.
- **`QUESTIONS`** array — the 10 quiz questions and their point values per path (each answer option awards points to one or more paths via the `points` object).

No build tools needed — edit the file, refresh the browser.

## How the interview feedback works

Clicking "Get AI Feedback on My Answer" first checks for Chrome's built-in `LanguageModel` API. When available, Gemini Nano evaluates the exact career, question, answer, reference answer, and technical concepts, then returns structured strengths and improvements. The model runs locally, so the answer is not sent to a remote AI service and no API key or application server is required. Chrome may need to download the on-device model the first time it is used.

If the Prompt API is not supported or the model cannot start, the page automatically uses `buildBehavioralFeedback()` or `buildTechnicalFeedback()`. Behavioral answers are checked for specificity and STAR elements; technical answers are checked against curated `keyTerms`, examples, and reasoning. The interface always identifies which engine produced the feedback.

Chrome's Prompt API currently requires a supported desktop Chrome installation and eligible hardware. The fallback makes the deployed GitHub Pages site safe to demonstrate in any browser even when on-device AI is unavailable.

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
