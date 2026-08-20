# enter-examples

> 🌐 **中文版** → [README.md](README.md)

<p align="center">
  <img src="assets/banner-enter-examples.png" width="760" alt="enter-examples — works an agent shipped on Enter">
</p>

<p align="center">
  <strong>Live, playable Enter builds — every entry ships its prompts, screenshots, and round-by-round verification record</strong>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-22ff88" alt="MIT"></a>
  <a href="https://d41c8754b3a14836980c67b0acfcddfa.prod.enterapp.pro/"><img src="https://img.shields.io/badge/🔴_live-PULSE_observatory-22ff88" alt="live demo"></a>
  <a href="https://github.com/convergeai-labs/enter-skills"><img src="https://img.shields.io/badge/method-enter--skills-22d3ee" alt="skills"></a>
</p>

Example works built on [Enter](https://enter.converge.ai) — the AI app builder — by an agent driving Enter with the [enter-skills](https://github.com/convergeai-labs/enter-skills) playbook. Every entry ships the story, the screenshots, the prompts, and full provenance.

---

## 🛰️ PULSE — AI 实时观测站 (AI real-time observatory)

<p align="center">
  <img src="entries/2026-08-pulse-ai-observatory/screenshots/06-agent-deep-dive.png" width="720" alt="PULSE — AI real-time observatory">
</p>

A "24-hours-alive" tech radar: AI streams an interpretation of what's happening on Hacker News / GitHub **right now**, every visitor shares the same "current moment", rank-momentum badges track the movement, an agent autonomously picks 3 stories and deep-dives them with real fetched content, and a weekly tech report ships with one-click Markdown copy for team sharing.

**▶ Live preview**: [pulse — ai 实时观测站](https://d41c8754b3a14836980c67b0acfcddfa.prod.enterapp.pro/) (published on prod; loads the current shared snapshot, regenerates at most every 15 min)

Zero input. First fold is the content. Built in 7 bounded batches over 3 days, each batch independently verified from outside Enter — including direct database reads and OS-clipboard read-back.

| | |
|---|---|
| <img src="entries/2026-08-pulse-ai-observatory/screenshots/03-multi-source.png" width="340" alt="multi-source radar"> | <img src="entries/2026-08-pulse-ai-observatory/screenshots/05-weekly-report.png" width="340" alt="weekly report"> |
| three-source radar with momentum | weekly tech report + copy Markdown |

### How an agent built it

<p align="center">
  <img src="assets/agent-builds-living-site.png" width="720" alt="From prompt to living website: an agent driving the Enter build">
</p>

Contract first → one rich creation prompt → six cohesive batches (each carrying the last round's verified baseline as invariants) → independent re-verification per batch. Enter executes; the agent plans and verifies — Enter's receipt is a claim, and all evidence comes from lanes outside Enter.

📖 **Full story + how it was made with an agent**: [entries/2026-08-pulse-ai-observatory/](entries/2026-08-pulse-ai-observatory/)
🛠 **The method**: [enter-project-ops](https://github.com/convergeai-labs/enter-skills/blob/main/skills/enter-project-ops/SKILL.md)

---

## Entries

| Entry | What | One line |
|---|---|---|
| [2026-08-pulse-ai-observatory](entries/2026-08-pulse-ai-observatory/) | Live AI tech radar | Zero-input observatory: streaming narrative, 3-source radar, momentum, agent deep-dives, weekly report — 7 verified batches |

More entries coming — each new Enter build lands here with its prompts and provenance.
