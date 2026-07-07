# BETS→GO

**A live football trading terminal that grades decisions, not outcomes.**

BETS→GO is an experimental decision-support workstation for live sports trading. You tell it what you see — score, minute, live odds, the cash-out offer — and it prices every available action in dollars: hold, cash out, partial, hedge, or an independent recovery trade. **"No Action" is always a valid recommendation.**

> BETS→GO does not predict the future. It continuously evaluates the quality of every available decision as new information arrives.

**Advisory only.** It analyzes data, quantifies trade-offs, and explains its reasoning; it does not guarantee outcomes, and the final wagering decision is always yours. If gambling stops being fun, call or text 1-800-GAMBLER (US). 21+.

## The experiment

This project exists to answer one question:

> **Does BETS→GO measurably improve live sports trading decisions?**

Every feature serves that hypothesis; anything else is deferred. The measurement instrument is the built-in **Match Journal**: every closed position is graded with a **Decision Quality Score (0–100)** based on process — positive-edge entry, stake discipline, following the cash-out engine, no negative-EV recovery trades, no chasing. See [docs/EXPERIMENT_LOG.md](docs/EXPERIMENT_LOG.md).

## Features

- **Live Trading Cockpit** — primary decision verdict with plain-English reasoning, Trade Score, confidence, and a dollars-first Risk & Exposure strip (exposure, max loss, lockable-now, expected value).
- **Action Board** — every option priced as Expected / Worst / Best net P/L and ranked: 🥇 best EV · 🛡 best capital protection · ⚖ best risk-adjusted.
- **Probability Engine** — explainable Poisson in-play model driven by pre-match xG, red cards, momentum, and game state; prices 1X2, totals, team totals, spreads, BTTS, next-goal.
- **Cash-Out Engine** — judges the book's offer against Expected Hold Value (HOLD / WAIT / PARTIAL / FULL).
- **Hedge Engine (protection simulator)** — equal-profit hedge stake with net P/L in every scenario; arms only at 25–80% win probability.
- **Recovery Opportunity Engine** — when a position is effectively dead, prices every live market independently; happily rules **NO RECOVERY TRADE** when nothing clears the EV bar.
- **Pulse checks** — automatic alerts at halftime, 70', 80', 85', 88', plus goals, red cards, probability swings, and fair-value cash-out offers.
- **Match Journal** — decision-quality-graded history with aggregates and JSON export.
- **Model & Method tab** — every formula documented in the app itself; nothing is a black box.

## Architecture

Market-agnostic **core engines** produce *facts*; a single **Decision Orchestrator** produces *advice*; sport-specific logic lives in **market adapters** (Football is the first). The app is deliberately a **single self-contained HTML file** — no build step, no dependencies, works from a double-click, an email attachment, or any static host. See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

## Local setup

None needed:

```
open index.html
```

Or serve it (avoids browser charset quirks with the file:// protocol):

```
python3 -m http.server 8765
# → http://localhost:8765/
```

State persists in `localStorage` (`betstogo_*` keys).

## Deployment

Any static host. For Netlify (config in `netlify.toml`):

```
netlify deploy --prod --dir .
```

## Roadmap

See [docs/ROADMAP.md](docs/ROADMAP.md). Current milestone: validate the hypothesis with real matches — not more features.

## Docs

- [North Star](docs/NORTH_STAR.md) · [Product Vision](docs/PRODUCT_VISION.md) · [Architecture](docs/ARCHITECTURE.md) · [Roadmap](docs/ROADMAP.md) · [Experiment Log](docs/EXPERIMENT_LOG.md)

## Screenshot

*(placeholder — add a capture of the Trade Desk with an active position)*
