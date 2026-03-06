---
name: competitor-changelog-spy
description: >
  Monitors and analyses competitor product changelogs to surface competitive intelligence for Product Managers. Use this skill whenever the user wants to track competitor updates, spy on what rivals are shipping, understand competitive moves, analyse a competitor's changelog, get a digest of recent competitor releases, or asks anything like "what has [competitor] shipped lately?", "what are my competitors building?", "summarise recent changes at X", or "give me a competitive update". Works for any number of competitors — one, five, or a whole market. Always use this skill — don't attempt competitor research or changelog analysis without it.
---

# Competitor Changelog Spy

A skill for PM competitive intelligence. Given one or more competitor names, it finds their changelogs, fetches the most recent updates, and delivers a structured briefing with strategic insight.

Supports any number of competitors. Process all of them in parallel where possible.

---

## Workflow

### Step 1 — Clarify scope (if not already provided)

Ask the user:
- Which competitors to monitor (any number — names are enough, you'll find the URLs)
- Time window: last 7 days / 30 days / 90 days / all available (default: 30 days)
- Their own product / what they're competing on (optional — sharpens the so-what analysis)

If the user has already provided this, skip ahead.

---

### Step 2 — Discover changelog URLs (run for ALL competitors)

For each competitor, search for their changelog using **date-aware queries** to surface the most recent content:

1. `[competitor name] changelog [current year]`
2. `[competitor name] release notes [current month] [current year]`
3. `[competitor name] what's new [current year]`
4. `[competitor name] product updates [current year]`

Also check these common URL patterns directly via web_fetch if search results are thin:
- `/changelog`, `/changelog/[year]`, `/changelog/[year]/[month]`
- `/releases`, `/release-notes`, `/whats-new`, `/updates`
- GitHub Releases page (essential for open source / dev tools)
- Docs site "What's New" section (common for enterprise SaaS)
- Official product blog filtered to `release` or `product` tag

**Recency rule**: Always prioritise the most recent page/entry. If a changelog is paginated by month or year, fetch the current month/year page first — not the annual index. If a fetched page has no entries within the past 90 days, re-search for a more recent URL before concluding nothing has shipped.

**Fallback sources for gated or missing changelogs:**
- Recent press releases / newsroom
- G2 or Capterra reviews mentioning new features (filter by recent dates)
- LinkedIn posts from their product team
- Twitter/X product account
- Job postings as proxy signals (hiring for X = investing in X)

Record the best URL found for each competitor. If no public changelog exists at all, note it explicitly.

---

### Step 3 — Fetch current changelog content (run for ALL competitors)

Use web_fetch on each discovered changelog URL.

**Always fetch the most recent content first:**
- If organised by year/month, fetch the current month's page, then previous month if more coverage is needed
- If a single long page, focus on the top (most recent) entries
- Check for "last updated" dates and confirm content is current before using it

---

### Step 4 — Parse and structure the changes (for ALL competitors)

For each competitor, extract a structured list of changes:

```
Competitor: [Name]
Changelog URL: [URL]
Most recent entry date: [Date]
Period covered: [Date range of fetched content]

Changes found:
- [Date] [Feature/fix title] — [brief description]
- ...
```

Group changes by type where possible:
- **New features** — net-new capabilities
- **Improvements** — enhancements to existing features
- **Integrations** — new connectors, APIs, partnerships
- **Pricing / packaging** — plan changes, new tiers
- **Infrastructure / performance** — speed, reliability, scale
- **Deprecations / removals**
- **Acquisitions / strategic moves**

---

### Step 5 — Competitive insight analysis (for ALL competitors)

For each competitor, write a 3–5 bullet "so-what" analysis:

- **Strategic direction**: What do these changes reveal about where they're heading?
- **Target customer signals**: Which persona or segment do these changes seem aimed at?
- **Threat assessment**: Does anything here directly threaten your product's differentiation?
- **Opportunity signals**: Does anything reveal a gap they haven't addressed that you could exploit?
- **Velocity signal**: Are they shipping fast/slow? Focused or scattered?

If the user provided their own product context, tailor the threat/opportunity analysis to their situation.

At the end, add a **Cross-competitor view**: 1–3 bullets on themes or patterns visible across multiple competitors (e.g. everyone is investing in AI, two are moving upmarket, one is cutting features).

---

### Step 6 — Produce all four outputs

All outputs cover ALL competitors provided.

---

#### Output A: Structured Summary

Clean, scannable breakdown per competitor (from Step 4). One section per competitor.

---

#### Output B: Competitive Insight / So-What Analysis

Strategic bullets from Step 5 in plain language a PM can paste into a strategy doc. Include the cross-competitor view at the end.

---

#### Output C: Raw Changelog Diff

Condensed, literal list of every change found per competitor, with dates where available. No editorialising — just the facts.

```
== [Competitor Name] ==
[Date] [Entry title]: [Entry description]
...
```

---

#### Output D: Slack / Email Digest

Short, human-friendly briefing ready to paste into Slack or send as an email. Max ~250 words regardless of number of competitors.

```
📡 Competitor Update — [Date range]

[Competitor 1]: [1-2 sentence highlight of biggest move]
[Competitor 2]: [1-2 sentence highlight]
[Competitor N]: [1-2 sentence highlight]
...

🔑 Key watch item: [The single most strategically significant thing across all competitors]

Full changelogs:
• [Competitor 1]: [URL]
• [Competitor 2]: [URL]
```

---

## Tips for best results

- **Always fetch the current year/month first** — changelog pages often have year/month navigation; go straight to the most recent page rather than the index
- **Dev tools / open source**: GitHub Releases is usually the most complete and current source
- **Enterprise SaaS**: Look for a "What's New" section in docs rather than the marketing blog — updated more frequently
- **Gated changelogs**: Some enterprise vendors require login to see feature details. Note this explicitly, fall back to press releases and analyst coverage, and flag to the user that the picture may be incomplete
- **No changelog found**: State this explicitly and suggest G2 reviews, LinkedIn product posts, or job listings as proxy signals
- **Historical tracking**: Web fetch reflects current page state only. For ongoing monitoring, suggest running this skill on a weekly cadence via n8n and saving outputs to Notion or a shared doc

---

## Pairing with automation

This skill is designed for on-demand use, but pairs naturally with:
- **n8n**: Schedule a weekly workflow that runs this skill and posts the digest to Slack
- **Notion**: Save the structured summary to a Competitor Intelligence database, one page per competitor
- **Clay**: Enrich competitor records with recent changelog activity as a signal layer
- **HubSpot / Attio**: Tag deals or accounts where a competitor's recent move is directly relevant
