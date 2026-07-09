# Architecture

*Current as of v0.5.1 ("The 10-Second Loop"). For the reasoning behind each layer, see the Decision Ledger entries referenced inline.*

## The two rules

**1. Every engine produces facts. Only the Decision Orchestrator produces advice.** (Ledger #2)

Facts are numbers with definitions (probabilities, expected values, ratios, scenario P/Ls, per-outcome exposure). Advice is a recommendation with reasoning ("HEDGE — it pays where your portfolio loses most"). Keeping the boundary hard means the model can be swapped, tested, and calibrated without touching how recommendations are phrased or ranked — and vice versa.

**2. The interface speaks Hard Rock or plain English. Engine vocabulary never reaches the screen.** (Ledger #12 — "The Translator")

The xG / edge / EV / EHV math all runs, but it lives in the *engine room* (collapsible disclosures). Every word on the primary surface either appears on a Hard Rock screen (Winner, Spread, Total Goals, Both Teams to Score, Cash Out, My Bets) or is a plain-English verdict. This is why the tool feels like an extension of Hard Rock rather than a separate system to learn.

## The unit of analysis is the PORTFOLIO (Ledger #11)

Since v0.4 the fundamental object is not a wager — it is the portfolio. The in-play model produces a **joint distribution over final scores** (an 11×11 Poisson grid). Each score-determined bet is a **payoff rule over that grid**: it maps every possible final score to a profit or loss. Summing those maps gives, for free:

- **Portfolio EV / worst case / best case** — over the whole grid
- **Net exposure by result** — expected P/L conditional on Home win / Draw / Away win
- **Correlated risk** — bets that win in the same cells stack; two goal-market SGP legs price *exactly*, better than the books' own correlation fudge
- **Coverage** — for a candidate add, what fraction of the portfolio's losing cells it wins in

Path-dependent markets (next goal) and manual-probability bets (player props, exotic SGP legs) contribute expected value flatly, without a per-score map, and are labeled as such.

## Layers

```
┌────────────────────────────────────────────────────────────┐
│ INTERFACE — speaks Hard Rock / plain English (Rule 2)      │
│   The Read (verdict · My Bets net · what moved · rec card) │
│   The Update (event-first pulse · predicted chips · 📷)    │
│   What-if previews · engine-room disclosures · Journal     │
├────────────────────────────────────────────────────────────┤
│ DECISION ORCHESTRATOR — the only producer of advice        │
│   portfolio verbs: HOLD · ADD · REDUCE · HEDGE ·          │
│   REBALANCE · CASH OUT — each justified only by the       │
│   portfolio delta · mission (BUILD/PROTECT/PRESERVE) ·     │
│   action-board ranking (🥇 EV / 🛡 protection / ⚖ risk-adj)│
├────────────────────────────────────────────────────────────┤
│ PORTFOLIO ENGINE — facts, aggregation over the score grid  │
│   buildMat (joint grid) · cellWins (bet → payoff map) ·   │
│   per-outcome exposure · correlated coverage · pfEV/worst │
├────────────────────────────────────────────────────────────┤
│ CORE ENGINES — market-agnostic, facts only                 │
│   Position · Probability · Cash-Out · Hedge ·             │
│   Watch/Add (was Recovery) · Alert · Journal              │
├────────────────────────────────────────────────────────────┤
│ MARKET ADAPTERS — everything sport-specific                │
│   FootballAdapter (first) — model + market catalog +      │
│   cellWins payoff predicates                              │
└────────────────────────────────────────────────────────────┘
```

## The three input lanes (Ledger #14, #16)

The Update sheet offers three ways to feed live data, cheapest-first — all governed by **Law #0: Hard Rock is the only source of truth.** A prediction never becomes data; nothing persists until the operator taps it.

1. **Tap (~8s, no keyboard)** — event-first: tap ⚽ GOAL / 🟥 RED CARD / 👀 CHECK (which sets score and re-prices), then confirm predicted chips (model's guess ±1 notch, clearly marked). The CHECK trigger is recorded with every pulse.
2. **Screenshot (~12s)** — 📷 reads the operator's Hard Rock screenshot with on-device OCR (`vendor/` tesseract.js, self-hosted); found numbers become 📷 chips to confirm. The image never leaves the phone.
3. **Type** — the ⌨ chip reveals an exact-entry field; always available, never required.

The Translate button previews the verdict live as numbers are confirmed ("Translate → HEDGE").

## MarketAdapter contract

An adapter supplies: identity, clock (`max`, axis ticks, minute formatting), score labels, pre-match model params, extra live inputs (e.g. red cards), momentum config, pulse checkpoints, the in-play `model(state)` returning rates + market probabilities, a serializable probability snapshot for the timeline chart, chart/bar/stat descriptors, a **market catalog** (`id → {option, forBet, forRecovery, needsLine, prob(M,st,line,manual), label(st,line)}`), a **`cellWins` map** (`id → (cell, line, st) → boolean` payoff predicate for score-determined markets; `null` for path-dependent/manual), dropdown orderings, `detectEvents(prev, live, st)` for goal/red-card–style alerts, and scripted demo scenarios.

Display names are Hard Rock terms with team names substituted live ("Winner — Argentina"). The core never references a sport concept. Adding a market = writing one adapter object and registering it in `ADAPTERS`. Registered adapters: `football`.

## Core engine responsibilities (facts)

- **Position** — portfolio lifecycle (`S.positions[]`): open/cash/settle per bet, stake, payout, per-bet Cash Out with a staleness timestamp, state persistence + schema migration (v0.3 single-bet → v0.4 portfolio; unmigratable legacy states discarded, not crashed on).
- **Probability** — delegates to the adapter model; prices any catalog market; computes edge vs. Hard Rock's implied probability; derives pre-match xG from the Winner odds when not overridden.
- **Portfolio** — `buildMat` (joint score grid), per-bet payoff maps via `cellWins`, portfolio EV/worst/best, per-outcome exposure, correlated coverage.
- **Cash-Out** — Expected Hold Value (`p × payout`) per bet, offer/EHV ratio, plain-English read (Take it / Fair / Low / Keep).
- **Hedge** — value-locking against the portfolio's dominant exposure; only when it improves the whole portfolio, never to soothe nerves.
- **Watch/Add** — independent EV per live market, quarter-Kelly stake capped at 50% of committed capital, coverage of the portfolio's losing cells; **only ever recommends adding on merit, never because a position is losing.** A decided market (prob ≥0.99 / ≤0.01) can never generate an ADD.
- **Alert** — event diffs (via adapter), checkpoint crossings, portfolio win-strength swings, fair-value Cash Out per bet, +EV add found.
- **Journal** — decision-quality scoring (0–100 rubric), per-bet outcomes, recommendation-tracking trail (advice vs. action per pulse, incl. the CHECK trigger), aggregates, export.

## Deliberate constraint: one file, one exception (Ledger #1, amended by #16)

`index.html` is the whole **application** — inline CSS/JS, no build step, no framework, CSP-safe, deployable by double-click / email / any static host. Structural discipline substitutes for module boundaries; the layer seams above are real even though everything is one file.

**The one exception:** `vendor/` holds third-party static assets that physically cannot be inlined — the OCR engine (tesseract.js), its WASM cores, and the English model (~27MB), served from the app's own origin and lazy-loaded on first use of the screenshot lane. No third-party host is contacted at runtime; the operator's screenshot never leaves the device.

## Storage

`localStorage`: `betstogo_state_v1` (active portfolio), `betstogo_journal_v1` (journal). Legacy pre-v0.1.0 keys (`ftos_*`) are read as a migration fallback and discarded if unmigratable. All storage access goes through a wrapper that degrades to in-memory in sandboxed iframes. `/?reset` clears the active portfolio from any device (escape hatch, Ledger via v0.3.1); `/?reset=all` also clears the journal.
