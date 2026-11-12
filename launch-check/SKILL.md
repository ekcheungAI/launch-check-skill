---
name: launch-check
description: Audit a live website with 20 read-only pre-launch checks (HTTPS, 404, sitemap, privacy page, tracking notice, secrets, security headers, image weight, links and more) and report PASS / FAIL / CAN'T TELL with evidence plus copy-paste fixes. Use when someone says "check my site before launch", "launch check", "pre-launch audit", or gives a URL and asks what is missing.
---

# launch-check

Run 20 read-only checks on a live URL and report honestly. This is a technical checklist, not legal advice.

## Rules

- READ-ONLY. Only GET/HEAD requests (curl, WebFetch). Never submit forms, log in, edit files or deploy.
- Every result is PASS, FAIL or CAN'T TELL, with one line of evidence you actually saw (URL, header, text, number). No evidence means CAN'T TELL, never PASS.
- Say what you did not check (for example: only the homepage and its scripts were scanned).
- Reply in the language the user wrote in.
- Do not claim anything is legally required or compliant. For privacy and cookie items, report what the page says and does, and use the wording in `references/hk-privacy-notes.md`.

## Steps

1. Get the URL from the user (ask once if missing). Normalise to `https://host`.
2. Read `references/checklist.md` and run the 20 items in order. Reuse one fetched copy of the homepage HTML for items 5–8, 11, 13, 15, 19, 20.
3. Output, in this order:
   1. A 20-row table: `# | item | PASS/FAIL/CAN'T TELL | evidence`.
   2. Counts, for example "18 PASS, 2 FAIL, 2 CAN'T TELL" (rows must add up to 20).
   3. FAIL items ordered by effort (smallest first), each with a copy-paste fix.
   4. A short "Could not verify" list.
4. Offer, do not do, the fixes. Edit the user's site only if they ask.

## Cost note

A full run is about 10 tool calls and a couple of minutes on a normal site.
