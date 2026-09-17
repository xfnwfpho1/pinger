# pinger

The FSM heartbeat of last resort (rung 4) — a 15-min cron that dispatches
`fsm-tick {reason: 'pinger'}` to [claudecode-headless/fsm-lab](https://github.com/claudecode-headless/fsm-lab).

**Why a separate account's repo** (T46/W-C3 design F-3): cross-repo dispatch needs a PAT;
quiet-lab is zero-secrets by constraint; same-org cron is the correlated failure class.
A user-account public repo = free minutes + a de-correlated schedule + the mirror-runner
secret posture. The chain's own self-tick (GITHUB_TOKEN) stays the LIVING heartbeat —
this is the backstop that revives a dead one.

**Honest physics**: GHA schedules fire sparsely (nominal 15min ≈ effective 15min–2h).
The watch-the-watcher duty on the executor side reports this pinger's liveness (a
missing pinger for 45min = a comment on the ops issue — visible, not fatal).

Secrets: `PINGER_PAT` (the dispatch token for fsm-lab). Nothing else. This repo holds
no code beyond the workflow.
