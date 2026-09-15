# Provenance — Daily Verse (一日一诗)

> 2026-09 · Enter (greenfield) · driven by Claude Code with the enter-project-ops skill

## Brief

Build a second Enter demonstration site with a **radically different style** from the neon-electronic PULSE observatory — proving style range, not just capability range. Chosen direction: an editorial/print-aesthetic AI poetry-reading site ("one poem a day, AI reads with you"). Contract: no publish without explicit authorization; keys server-side only; public-domain/public-API content only; at most one LLM call per day; independent verification of every claim.

## Rounds

| Round | What shipped / happened | Independent verification |
|---|---|---|
| 0.5 | Local design prototype (single-file HTML) to de-risk the style while the platform was unreachable: rice-paper/ink/cinnabar, vertical title, real API poem, 4-poem archive, copy-card | Headless QA: 3 viewports overflow 0, console 0 errors, clipboard read-back |
| 0.6–0.8 | Platform automation battle (see notes below): Cloudflare, Google OAuth passkey, a zero-credit wall on the first workspace | Login chain proven end-to-end once a Pro workspace was selected |
| 1.0 | Creation: one prompt → plan → model question (chose the best-Chinese-writing tier) → Cloud gate (new Supabase) → AI key gate → build: `daily-verse` edge function + `verse_snapshots` (unique `day_key`) + streaming UI | Full independent QA on preview: 1440/390/327 overflow 0, console 0 errors, paper color `#f7f3e9`, copy button → OS clipboard byte-checked, **direct DB read**: today's row with real poem + `source` label + honest `dynasty: null`, RLS public-read working, honest empty archive |
| 2.0 | Published to prod (user-authorized) | Prod re-QA green; **day-boundary witnessed**: at 00:00:52 (+8) the first visitor after midnight triggered day-2's generation (`day_key=2026-09-15`), day-1 row preserved — idempotent lazy refresh proven in production |

## Platform notes worth remembering

- **Playwright's default `--use-mock-keychain` silently breaks Touch ID passkeys.** Google's passkey page never fires the ceremony until you launch with `ignoreDefaultArgs: ['--use-mock-keychain', '--password-store=basic']` — then it auto-triggers.
- **A zero-credit workspace swallows submits silently** (no error, no toast) — detect the "out of credits" banner text; a 60-second sentinel re-submits automatically once credits return.
- **Completion signals get contaminated**: the creation prompt itself echoes into the chat (so keyword checks like "files changed" must run on a tail slice only); "thought for N seconds" text persists in history (detect active work via spinner DOM, not text).
- **Gate dialogs vs. generic modal dismissal**: a blanket "close every dialog" routine closes the very gate you need to act on — check for gate buttons first. In the AI-key dialog, 「新建」 is a *tab*, not a submit; the real action is 「连接」 (and its disabled state may be `aria-disabled`, not `disabled`).
- The strongest verification lane is again the database: with public-read RLS, the anon key (captured from the app's own REST request headers) turns every UI claim into a countable query.

## Known gaps

- The editor's final build receipt was not captured (the chat stream showed a stale-view artifact after completion); verification rests entirely on external evidence (live site + DB + clipboard), which is the stronger lane anyway.
