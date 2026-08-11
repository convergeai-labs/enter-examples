# PULSE — AI 实时观测站 (AI Real-Time Observatory)

> 🌐 **中文版** → [README.md](README.md)

**Live preview**: https://d41c8754b3a14836980c67b0acfcddfa.live-preview.enterapp.pro/ (Enter preview link; may be replaced by a prod URL later)

A "24-hours-alive" tech-radar dashboard, built entirely on [Enter](https://enter.converge.ai) by an AI agent driving the Enter agent. Zero input — the first fold is the content: AI interpreting what the tech world is discussing **right now**, with every visitor sharing the same "current moment".

![first load](screenshots/01-first-load.png)

## What it does

- **Live AI narrative** — PULSE Observer streams a four-section Chinese interpretation of the current signals (headlines → theme clusters → editorial take → "what changed since the last snapshot")
- **Three-source radar** — Hacker News front page, GitHub's new high-star repos, Lobste.rs; grouped with per-source badges, and cross-source resonance called out when a topic genuinely appears on multiple sources
- **Rank momentum** — every item carries ↑n / ↓n / NEW badges computed server-side against the previous snapshot
- **One-line summaries** — the LLM annotates all 25 items in the same generation pass (title-only inference, no fabrication)
- **Observer deep-dives** — a real tool-use agent loop: the Observer *selects* up to 3 items worth a closer look, the backend *fetches* their HN comments / GitHub README, then it *writes* grounded commentary — each card labeled with where the content came from
- **Weekly tech report** — every week, the week's snapshots are aggregated into a structured report (hot themes by frequency, star projects with real star-growth deltas, cross-source review, outlook) with a one-click **Copy Markdown** button for sharing into a team's weekly-report channel
- **Shared world state** — snapshots are public-read / service-role-write; refresh the page, switch browsers, you see the same moment. A global 15-minute atomic lock keeps generation cost bounded with no cron

![deep dive cards](screenshots/06-agent-deep-dive.png)

## How it was made (agent + skill)

Built by Claude Code driving Enter, following the [enter-project-ops](https://github.com/convergeai-labs/enter-skills) skill. The division of labor: **Claude plans and verifies, Enter executes.**

1. **Contract first** — a local goal file fixed the concept, the capability-showcase list, the guardrails (no publish without authorization, keys server-side, public data only, 15-min lock), and became the run log.
2. **One rich creation prompt** ([prompts/](prompts/)) — concept, data source, lazy-refresh cost model, storage + RLS semantics, page structure, constraints. Enter planned, asked model/cloud/AI gates, then built: edge function + two tables + streaming UI.
3. **Six bounded batches, one theme each** — content enrichment → radar-ization (summaries + momentum) → multi-source → weekly report → agent tool-use deep-dives. Each batch prompt carried the previous round's *verified* baseline as its invariants, plus explicit exclusions (tomorrow's scope is excluded today).
4. **Independent verification after every batch** — Enter's receipt is a claim. Each round was proven from outside: fresh preview loads at 3 viewports, console/network health, and the strongest lane — **direct database reads via the public anon key** (row counts, new columns, computed deltas). Copy-Markdown was verified by reading the OS clipboard (`pbpaste`) and diffing against the DB narrative. Momentum badges and cross-source resonance were witnessed live the next morning when the real rankings moved overnight.
5. **Platform quirks survived** — stale task streams (reload the editor URL to resync), edge-function deploy propagation lag (debug markers, then cleaned), a real PostgREST `.or()` claim-readback bug that Enter diagnosed and fixed mid-build.

### The honest bits (why it's trustworthy)

- One source (Lobste.rs) is unreachable from the edge function's network. The site says so in every affected narrative and ships with the remaining sources — degradation by design, witnessed in production.
- When a week had no cross-source overlap, the weekly report said "各来源信号相对独立" instead of inventing resonance.
- Rank deltas of 0 render no badge — the absence of noise is the correct behavior.

## Gallery

| | |
|---|---|
| ![item summaries](screenshots/02-item-summaries.png) | ![multi-source](screenshots/03-multi-source.png) |
| per-item one-line summaries (batch A) | three-source grouping + badges (batch B) |
| ![momentum live](screenshots/04-momentum-live.png) | ![weekly report](screenshots/05-weekly-report.png) |
| ↑/NEW badges witnessed live (batch A proof) | weekly report + copy Markdown (batch C) |

Mobile (327–390px, zero horizontal overflow): [07-mobile.png](screenshots/07-mobile.png)

## Provenance

Full round-by-round record with verification evidence: [provenance.md](provenance.md). Representative prompts: [prompts/](prompts/).
