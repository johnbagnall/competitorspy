# 🕵️ Competitor Changelog Spy

A Claude Skill for Product Managers that automatically finds, fetches, and analyses competitor product changelogs — turning raw release notes into structured competitive intelligence.

---

## What it does

Give it a list of competitors (just their names — no URLs needed) and it will:

1. **Find** their public changelogs, release notes, or "what's new" pages
2. **Fetch** the most recent entries within your chosen time window
3. **Analyse** what each change signals strategically
4. **Deliver** four ready-to-use outputs:
   - 📋 Structured summary per competitor
   - 🧠 "So-what" competitive insight analysis
   - 📄 Raw changelog diff (dates + facts, no editorialising)
   - 📣 Slack/email digest (~250 words, ready to paste)

Works for **any number of competitors** — one, five, or an entire market.

---

## Example prompt

```
Run the competitor changelog spy on Notion, Linear, and Asana for the last 30 days.
We're a project management tool targeting product teams.
```

---

## Installation

### Option 1: Install via `.skill` file
1. Download `competitor-changelog-spy.skill` from this repo
2. Open Claude
3. Go to **Settings → Skills → Install from file**
4. Select the `.skill` file

### Option 2: Manual install
1. Copy the contents of `SKILL.md`
2. In Claude, go to **Settings → Skills → Create new skill**
3. Paste the content and save

---

## Outputs explained

| Output | Best for |
|--------|----------|
| **Structured Summary** | Pasting into a strategy doc or competitive wiki |
| **So-What Analysis** | Sharing with your leadership team or in a roadmap review |
| **Raw Changelog Diff** | Archiving in Notion or a competitive tracker |
| **Slack/Email Digest** | Sending to your team on a weekly cadence |

---

## Tips

- **Works best when you tell it your own product** — the so-what analysis gets much sharper when it can compare against your positioning
- **Enterprise SaaS vendors** often gate their changelogs behind login — the skill flags this and falls back to press releases, G2 reviews, and LinkedIn posts
- **Open source / dev tools** — GitHub Releases pages are fetched directly and tend to be the most complete source
- **No changelog found** — the skill will say so explicitly and suggest proxy signals like job postings or community posts

---

## Pairing with automation

This skill is designed for on-demand use but pairs naturally with:

- **n8n** — schedule a weekly HTTP → Claude workflow to run the skill and post the digest to Slack automatically
- **Notion** — save the structured summary output to a Competitor Intelligence database
- **Clay** — use changelog activity as a signal layer when enriching competitor records
- **HubSpot / Attio** — tag deals where a competitor's recent move is directly relevant

---

## Changelog

| Version | Notes |
|---------|-------|
| v1.0 | Initial release — unlimited competitors, recency-first fetching, four output formats |

---

## Contributing

PRs welcome. If you find a competitor type that doesn't work well (e.g. a specific changelog format the skill misses), open an issue with the URL and I'll update the discovery logic.

---

## Licence

MIT — use freely, attribution appreciated.
