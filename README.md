# Control Room — RRB JE + CUET Prep Tracker

A personal study-tracking dashboard for RRB JE 2026 and CUET UG 2027 preparation.
No backend, no login — everything is saved in your browser's storage.

## Features

- **Dashboard** — today's hours vs target, RRB JE / CUET split, streak, revision queue
- **Daily Log** — add/edit/delete study sessions, search & filter, duplicate a past session
- **Daily Plan** — targets, topics, checklist, end-of-day reflection, saved per date
- **Calendar** — every day since your start date, hours studied, mark Completed / Partial / Missed / Rest
- **Syllabus Tracker** — add your own topics (nothing pre-filled), track status and revision count
- **Mock Tests** — log test scores, see your score trend over time
- **Analytics** — weekly/monthly hours, subject breakdown, weakest subjects, missed days
- **Settings** — edit daily targets, manage subjects, export/import backup (JSON), export CSV, reset

All data lives in `localStorage` in your browser, under the key `prep-tracker:data:v1`.

## Run it locally

```bash
npm install
npm run dev
```

Open the printed local URL (usually `http://localhost:5173`).

## Build for production

```bash
npm run build
npm run preview   # optional, to check the production build locally
```

The build output goes to `dist/`.

## Deploy to GitHub Pages

This repo includes a ready-to-use GitHub Actions workflow at
`.github/workflows/deploy.yml`. To use it:

1. Push this project to a GitHub repository.
2. In the repo, go to **Settings → Pages** and set **Source** to **GitHub Actions**.
3. Push to the `main` branch (or run the workflow manually from the **Actions** tab).
4. The app will be built and published automatically. The URL will appear in the
   Actions run summary and under **Settings → Pages**.

No manual `gh-pages` branch setup is needed — the workflow builds and publishes
`dist/` directly. The app uses hash-based routing (`/#/log`, `/#/calendar`, etc.)
so it works correctly from any subpath GitHub Pages assigns it.

## Backing up your data

Because everything is stored only in your browser, **back up regularly**,
especially before clearing browser data, switching browsers/devices, or
reinstalling. Go to **Settings** in the app:

- **Export full backup (JSON)** — saves every session, topic, mock test, and plan.
  Keep this file somewhere safe (cloud drive, email to yourself, etc.).
- **Import backup** — restores from a previously exported JSON file. This
  replaces all current data, so export first if you want to keep it.
- **Export sessions (CSV)** — a spreadsheet-friendly export of your study log only.

## Project structure

```
src/
  lib/          date helpers, types, localStorage read/write, CSV export
  context/      DataContext — single source of truth, persisted on every change
  components/   shared UI (Panel, Button, Modal, etc.) and Layout/SessionModal
  pages/        one file per section (Dashboard, DailyLog, Calendar, Syllabus, ...)
```

## Notes

- The preparation day counter counts every calendar day from your start date
  (set in Settings), including missed days — a missed day still counts as a
  day, it's just visible as "Missed" rather than silently skipped.
- The syllabus list starts empty on purpose — add topics from your own official
  notification/syllabus PDF so the tracker matches exactly what you need to cover.
