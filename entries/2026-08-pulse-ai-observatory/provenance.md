# Provenance — PULSE AI Real-Time Observatory

> 2026-08 · Enter (greenfield) · driven by Claude Code with the enter-project-ops skill

## Brief

Build a valuable Enter project for **external demonstration** — visually striking and capability-showcasing. Chosen direction (of three proposed): an AI real-time observatory. Concept: a "24-hours-alive" dashboard where visitors watch AI interpret the tech world's current signals; every visitor shares the same current moment.

Constraints from the contract: no publish/share without explicit authorization; keys server-side only; public data only; global 15-minute minimum refresh interval; independent verification of every round.

## Rounds

| Round | Batch | What shipped | Independent verification |
|---|---|---|---|
| 0 | Creation prompt | Edge function + `pulse_snapshots`/`pulse_items` + streaming UI; HN Algolia source; lazy refresh with atomic 15-min lock; PULSE Observer persona (3-section narrative) | Isolated browser: real HN data, reload triggered fresh generation, history switching, 3 viewports overflow 0, console 0/0 |
| 1 | — | (initial build completed through plan + cloud/AI gates) | as above |
| 2 | 内容丰富化 | 4th narrative section "与上一刻相比" (previous snapshot as context), `themes text[]` chips, stats bar (total points/comments/top domains), how-it-works section | DB read-back: themes populated; stats hand-recomputed (3120/1531) matching UI; backward compat with pre-themes rows; 15-min lock not regressed |
| 3 | 榜单雷达化 | Per-item one-line summaries (`summary`), rank momentum (`hn_id`, `rank_delta`, `is_new`), structured LLM output with parse-failure degradation | DB: 15/15 items with summaries + hn_id; deltas correctly all-0 during a static window (no false badges); old snapshots render clean; console 0/0 |
| 4 | 多数据源雷达 | +Lobste.rs +GitHub new-high-star; `source` column with backfill; grouped UI + source badges; per-source independent degradation; cross-source resonance in narrative | DB: 25 items (15 HN + 10 GitHub); GitHub rules verified (first gen all `is_new`, second gen matched); Lobste.rs unreachable from edge network — degradation note rendered honestly; resonance claim matched real data; console 0/0 |
| 5 | 每周技术周报 | `pulse_weekly_reports` + weekly lock table; lazy once-a-week generation; 5-section report; copy-Markdown button | First report landed with real aggregates (14 snapshots, 210/0/20 per-source counts exact, star growth 8467→8477); copy button verified via OS clipboard read-back, byte-identical head/tail vs DB narrative; honest "no resonance" reporting. Enter self-diagnosed and fixed a PostgREST `.or()` claim-readback bug mid-batch |
| 6 | Observer 工具化深潜 | Agent loop: selection call → tool fetch (HN comments / GitHub README) → writing call; `deep_dive`/`deep_dive_reason` columns; deep-dive card section | Whole loop live-witnessed: 3 cards (2 HN + 1 GitHub), reasons matching real items, dive content matching real sources (Kimi README details, HN comment threads); 327px single-column clean; console clean |
| 7 | 换源 DEV.to | Lobste.rs (unreachable from the edge network all week) replaced by DEV.to daily top; `devto` source enum, badges, momentum rules, deep-dive comment tool (`/api/comments?a_id=`); all 3 sources live: 35 items/snapshot | Direct DB read: latest snapshot 15 HN + 10 devto + 10 github; agent picked a DEV.to article for deep-dive grounded in real comments; fresh-load audit 3 viewports overflow 0, console 0 errors; **published to prod** (post-publish audit green) |

## Platform notes worth remembering

- Edge-function deploys propagate with lag; debug markers settled "is the new code live" questions and were removed before final deploys (twice).
- The editor task stream stalls every ~10–15 min; reloading the editor URL resyncs it (builds continue server-side).
- Login sessions survive via saved storage state; four browser crashes in one day cost ~30s each to recover.
- The strongest verification lane is the database: with public-read RLS, the anon key turns every UI claim into a countable query.

## Outcome

A zero-input, always-live, honestly-degrading, agent-driven observatory — plus a reusable weekly-report artifact for a team's sharing channel. Published to prod 2026-08-12 after round 7 (user-authorized): https://d41c8754b3a14836980c67b0acfcddfa.prod.enterapp.pro/
