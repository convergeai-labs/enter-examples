# Daily Verse — AI Poetry Reading Site

> 🌐 **中文版** → [README.md](README.md)

**Live site**: https://92346ae03f4c440fb435995a5c68f861.prod.enterapp.pro/ (published prod URL)

An editorial/print-aesthetic AI poetry-reading site, built entirely on [Enter](https://enter.converge.ai) — deliberately styled as the **opposite** of the neon-electronic PULSE entry in this series, proving the same agent workflow produces radically different site personalities. Zero input, poem on first paint: one real classical Chinese poem per day, read with you by AI, shared by every visitor.

![Desktop full page](screenshots/01-desktop.png)

## What it does

- **One poem per day, shared by all visitors** — today's poem card (vertical title, dynasty & author, full text) on first paint; the day's first visitor (UTC+8) triggers generation, everyone after reads the same one
- **Three-part AI reading** — plain-language translation (faithful) / imagery appreciation (only what's in the text, no invented history) / "one thought for today" (explicitly labeled subjective). When context is unknown, it says less — never fabricates
- **Day-idempotent, no cron** — a unique `day_key` constraint guarantees one generation per day; concurrent triggers lose to the constraint and read the winner's row; at most one LLM call per day
- **Real source + honest fallback** — a public daily-poem API primary, 30 public-domain poems as backup; when the API is unreachable the site switches and honestly labels the source
- **Copy poem card** — one click copies a Markdown card (title / author / lines / one reading excerpt)
- **Archive** — a timeline of past cards, click to read any day, return to today

## Visual spec (anti-PULSE)

Rice-paper warm white `#f7f3ea` / ink `#2b2b2f` / cinnabar `#c93b2e`; serif-first (Noto Serif SC); vertical poem titles via `writing-mode: vertical-rl`; pure-CSS paper texture; seal-style cinnabar badges; generous whitespace. No dark backgrounds, neon, glow, radar/grid motifs. Zero horizontal overflow at 1440×900 / 390×844 / 327×603.

## How it was built with agent + skill

Driven by Claude Code using the [enter-project-ops](https://github.com/convergeai-labs/enter-skills) skill. The split: **Claude plans and verifies, Enter executes.**

1. **Style written into the contract as negation** — a local goal file pins the visual spec (colors / fonts / explicit ban list) and the data contract (day-idempotency, honest degradation, no fabrication) so the agent can't drift back to a default "AI dashboard" look.
2. **One rich creation prompt** ([prompts/00-creation.txt](prompts/00-creation.txt)) — concept, visual spec, sources + fallback, idempotency model, table + RLS, page structure, constraints. Enter planned, passed three gates (model choice, cloud, AI key), then built: edge function + unique-constraint table + streaming UI.
3. **Independent verification at every step** — receipts are claims. Three-viewport screenshots, console audits, copy-button verified via OS clipboard read-back, and the strongest lane: **direct database reads with the public anon key** — rows, constraints, and source labels all countable.
4. **Day-boundary behavior witnessed in production** — the publish happened minutes before midnight: at 00:00:52 (+8) the first visitor triggered the next day's generation while yesterday's card stayed archived. Idempotent lazy refresh, proven live.

### Honesty (why it's credible)

- The poem API returns no dynasty field: the DB stores `null` and the page shows only the author — no invented dynasty.
- Day one's archive renders an honest empty state ("no past cards yet — tomorrow's will be the first").
- The "one thought for today" section is explicitly labeled as subjective musing, separate from translation and analysis.

## Gallery

| | |
|---|---|
| ![Desktop](screenshots/01-desktop.png) | ![Mobile](screenshots/02-mobile.png) |
| Desktop 1440: vertical title + three-part reading | Mobile 390: vertical gracefully degrades to horizontal, zero overflow |

## Provenance

Full creation record (including the platform-automation battle and per-round verification evidence): [provenance.md](provenance.md). Original creation prompt: [prompts/00-creation.txt](prompts/00-creation.txt).
