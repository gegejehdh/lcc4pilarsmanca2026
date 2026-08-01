# Tim LCC 4 Pilar MPR RI - SMANCA

A public single-page site for SMANCA's 4 Pilar MPR RI (Pancasila, UUD 1945, NKRI, Bhinneka Tunggal Ika) team. It presents study material for each pillar, a 10-question quiz per pillar, a voting page for team advisors, and a way for visitors to leave impressions/messages for the team.

## Key technologies

- Static HTML, Tailwind CSS (via CDN), Font Awesome, and vanilla JavaScript — no build step required.
- Netlify Forms handles the three data-collecting forms (registration, advisor votes, and impressions/messages) with spam protection via honeypot fields.

## Running locally

Serve `index.html` with any static file server, or use the Netlify CLI for full local emulation including Netlify Forms:

```bash
netlify dev
```

Then open the printed local URL in your browser.

## Structure

- `index.html` — the entire application (markup, styles, and logic in one file).
- Hidden `<form>` elements near the end of the body register the three forms with Netlify's build-time form detection; the visible in-app forms submit to them via AJAX.
