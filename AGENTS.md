# AGENTS.md

## Project overview

Single-page static site (`index.html`) for SMANCA's LCC 4 Pilar MPR RI team: home page, per-pillar material + quiz, advisor voting, and an impressions/messages form. No backend framework, no build step — Tailwind and Font Awesome are loaded from CDN.

## Architecture

- All markup, styles, and JavaScript live in `index.html`. Client-side "pages" are `<div class="page-view">` sections toggled via `navigateTo()`; there is no router or reload between them.
- `pilarData` is an in-file object holding the study material and 10-question quiz per pillar (Pancasila, UUD 1945, NKRI, Bhinneka Tunggal Ika). Quiz state (`currentQuizIndex`, `userAnswers`, `scoreCount`) is plain module-scope JS state, reset each time a quiz starts.
- Data submission (registration, votes, impressions) goes through Netlify Forms, not a custom backend or external service. Each of the three forms has a hidden, honeypot-protected `<form data-netlify="true">` skeleton near the end of `<body>` so Netlify's build bot registers the form; the visible in-app forms submit to it via `fetch('/', ...)` with `application/x-www-form-urlencoded` body (see `submitToNetlifyForm()`).

## Conventions

- Keep new data-collecting forms consistent with the existing pattern: add a hidden skeleton form with a unique `name`, a `bot-field` honeypot, and every field name the JS will submit — Netlify validates field names against the registered form.
- Don't introduce Formspree or other third-party form services; persistence/data collection should stay on Netlify Forms per project convention.
- Styling relies on Tailwind's CDN build plus a handful of custom classes in the `<style>` block (`btn-gold`, `btn-pilar`, `card-shadow`, `garuda-glow-image`, `keyboard-open`). Reuse these rather than adding new ad hoc styles where they fit.
