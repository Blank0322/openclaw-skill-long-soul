---
name: long-soul
version: 0.1.0
description: A long-horizon companion skill: daily ingestion → reflection → low-noise proactive pings.
---

# Long-Soul (OpenClaw Skill)

This is a starter skill concept for an "evolving companion" that:

- runs **low-frequency** background ingestion (1–3 items/day)
- maintains a **small, auditable memory** (preferences + weekly deltas)
- sends **non-spammy** proactive messages (opt-in windows)

## Design principles

- Silent-by-default; user controls frequency and allowed sources
- Evidence-linked: any "new belief" references a source card + a user log
- Budgeted: hard caps on requests/tokens per day

## Proposed commands

- `long-soul setup` — set time window + sources + tone
- `long-soul mood <text>` — append a mood log
- `long-soul digest` — generate a short digest + 1 question
- `long-soul reflect` — weekly reflection + belief delta

## Data model (minimal)

- `UserLog(ts, mood, topic, note)`
- `IngestCard(ts, url, quote, summary, tags)`
- `BeliefDelta(ts, claim, evidence=[card_id, log_id], style_change)`

## Implementation notes

This repo currently contains scaffolding only. Next steps:
- implement a small local store (JSONL or SQLite)
- implement 1 ingestion source (RSS) + 1 LLM summarizer
- implement proactive scheduling (OpenClaw cron)
