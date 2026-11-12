# launch-check

A Claude skill that runs 20 read-only pre-launch checks on a live website and reports PASS / FAIL / CAN'T TELL with evidence and copy-paste fixes. Not legal advice.

## Install (Claude Code)

```bash
git clone https://github.com/ekcheungAI/launch-check-skill.git
mkdir -p ~/.claude/skills
cp -R launch-check-skill/launch-check ~/.claude/skills/
```

## Use

In Claude Code: `Use the launch-check skill on https://example.com`

Needs only `curl`; no accounts, no keys. It never edits your site.

## What it checks

HTTPS redirect, custom 404, sitemap, robots, title and description, share tags, favicon, viewport, privacy page, personal-data notice, tracking notice, terms, leaked keys, security headers, alt text, image weight, links, contact, third-party loads, canonical/noindex. See `launch-check/references/checklist.md`.

## Limits

It reads the homepage and what it links to. It cannot see behind a login, cannot judge legal compliance, and marks anything it cannot verify as CAN'T TELL.
