# Architecture

## The rule

**Every engine produces facts. Only the Decision Orchestrator produces advice.**

Facts are numbers with definitions (probabilities, expected values, ratios, scenario P/Ls). Advice is a recommendation with reasoning ("HOLD — you're holding +12.6 pts of edge"). Keeping the boundary hard means models can be swapped, tested, and calibrated without touching how recommendations are phrased or ranked — and vice versa.

## Layers

```
┌──────────────────────────────────────────────────────┐
│ UI (Trade Desk · Journal · Model & Method)           │
├──────────────────────────────────────────────────────┤
│ DECISION ORCHESTRATOR — the only producer of advice  │
│   verdict + reasoning · trade score · confidence ·   │
│   risk rating · cash-out recommendation · action     │
│   board ranking (🥇 EV / 🛡 protection / ⚖ risk-adj)  │
├──────────────────────────────────────────────────────┤
│ CORE ENGINES — market-agnostic, facts only           │
│   Position · Probability · Cash-Out · Hedge ·        │
│   Recovery · Alert · Journal                         │
├──────────────────────────────────────────────────────┤
│ MARKET ADAPTERS — everything sport-specific          │
│   FootballAdapter (first implementation)             │
└──────────────────────────────────────────────────────┘
```

## MarketAdapter contract

An adapter supplies: identity, clock (`max`, axis ticks, minute formatting), score labels, pre-match model params, extra live inputs (e.g. red cards), momentum config, pulse checkpoints, the in-play `model(state)` (opaque to the core), a serializable probability snapshot for the timeline chart, chart/bar/stat descriptors, a **market catalog** (`id → {option, forBet, forRecovery, needsLine, prob(M,st,line,manual), label(st,line)}`), dropdown orderings, `detectEvents(prev, live, st)` for goal/red-card–style alerts, and scripted demo scenarios.

The core never references a sport concept. Adding a market = writing one adapter object and registering it in `ADAPTERS`. Registered adapters: `football`.

## Core engine responsibilities (facts)

- **Position** — open/close lifecycle, stake, payout, exposure, state persistence + schema migration.
- **Probability** — delegates to the adapter model; prices any catalog market; computes edge vs. book-implied probability.
- **Cash-Out** — Expected Hold Value (`p × payout`), offer/EHV ratio, rating.
- **Hedge** — equal-profit stake and scenario P/Ls; activation gate (25–80% win probability).
- **Recovery** — independent EV per live market, quarter-Kelly stake capped at 50% of original stake.
- **Alert** — event diffs (via adapter), checkpoint crossings, probability swings, fair-value cash-out, +EV recovery found.
- **Journal** — decision-quality scoring (0–100 rubric), history, aggregates, export.

## Deliberate constraint: one file

v0.1.0 ships as a single self-contained `index.html` (no build step, no dependencies, CSP-safe). This maximizes portability — double-click, email, artifact, any static host — and keeps the experiment loop fast. The layering above is enforced structurally within the file; splitting into modules later is mechanical because the seams already exist. Revisit when the file's size hurts more than a build step would.

## Storage

`localStorage`: `betstogo_state_v1` (active position), `betstogo_journal_v1` (journal). Legacy pre-v0.1.0 keys (`ftos_*`) are read as a migration fallback. All storage access goes through a wrapper that degrades to in-memory in sandboxed iframes.
