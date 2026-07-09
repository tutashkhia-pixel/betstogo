# BETS→GO

**A live sports-bet portfolio manager that grades decisions, not outcomes.**

BETS→GO is an experimental decision companion for live sports trading. It sits beside Hard Rock during a match: you tell it what Hard Rock shows — the score, the odds, your Cash Out values — and it evaluates your **whole portfolio of bets** as one thing, then names the smartest move in plain English and real dollars: HOLD · ADD · REDUCE · HEDGE · REBALANCE · CASH OUT. **Doing nothing is always a valid call.**

The interface speaks **Hard Rock's language, not the model's** — every word on screen either appears on a Hard Rock screen or is a plain-English verdict. The xG/edge/EV math runs underneath, in the engine room. Updating takes seconds: tap the event and confirm predicted numbers, or hand it your Hard Rock screenshot (read on-device — nothing is uploaded).

> BETS→GO does not predict the future. It continuously evaluates the quality of every available decision as new information arrives. **Hard Rock is always the source of truth.**

**Advisory only.** It analyzes data, quantifies trade-offs, and explains its reasoning; it does not guarantee outcomes, and the final wagering decision is always yours. It never logs into or scrapes your sportsbook. If gambling stops being fun, call or text 1-800-GAMBLER (US). 21+.

## The experiment

This project exists to answer one question:

> **Does BETS→GO measurably improve live sports trading decisions?**

Every feature serves that hypothesis; anything else is deferred. The measurement instrument is the built-in **Match Journal**: every closed match is graded with a **Decision Quality Score (0–100)** based on process — positive-edge entries, stake discipline, following the Cash Out reads, no negative-EV adds, no chasing — and **recommendation tracking** records what the app advised versus what the operator did at every pulse. See [docs/EXPERIMENT_LOG.md](docs/EXPERIMENT_LOG.md).

## Features

- **The Read** — the 10-second surface: a status verb (🟢 HOLD / CASH OUT / …), one plain sentence, your bets with net-if-held in dollars, what moved since your last check, and a single recommendation card.
- **Portfolio engine** — every bet is a payoff rule over the model's joint final-score grid; the app nets your exposure to every outcome, prices correlated risk exactly (e.g. SGP goal legs), and justifies each verdict by the **portfolio delta**, never by whether one bet looks good in isolation.
- **The Update** — three input lanes, all under Law #0 (Hard Rock is the source of truth): **tap** an event and confirm predicted chips (~8s, no keyboard); hand it a **screenshot** (on-device OCR → 📷 chips); or **type**. The Translate button previews the verdict live.
- **What-if** — tap any market to see the portfolio before → after adding it (EV / worst / best / coverage); "I placed it" / "I cashed this" record mid-match reality so the portfolio stays truthful.
- **Cash Out reads** — judges each Hard Rock Cash Out against what the bet is really worth (Take it / Fair / Low / Keep).
- **Watch / Add engine** — prices any live market on its own merit; only ever suggests adding when the numbers favor it, **never because you're down**.
- **Probability engine** — explainable Poisson in-play model; pre-match strength derived from the Winner odds you enter; prices 1X2, totals, team totals, spreads, BTTS, next-goal.
- **Objective shifts** — BUILD → PROTECT → PRESERVE re-light the cockpit so the change in mission is felt, not just read.
- **Match Journal + Model & Method** — decision-quality-graded history with JSON export; every formula documented in the app itself.

## Architecture

Market-agnostic **core engines** produce *facts*; a single **Decision Orchestrator** produces *advice*; sport-specific logic lives in **market adapters** (Football is the first). Since v0.4 the fundamental unit is the **portfolio** — bets as payoff maps over a joint score grid. The interface speaks Hard Rock or plain English; engine vocabulary stays in the engine room. The app is a **single self-contained `index.html`** (no build, no framework, any static host); the one exception is `vendor/`, third-party static assets (the on-device OCR engine) that can't be inlined. See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md).

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

- [North Star](docs/NORTH_STAR.md) · [Product Vision](docs/PRODUCT_VISION.md) · [Architecture](docs/ARCHITECTURE.md) · [Operating Model](docs/OPERATING_MODEL.md) · [Founder Manifesto](docs/FOUNDER_MANIFESTO.md) · [Decision Ledger](docs/DECISION_LEDGER.md) · [Roadmap](docs/ROADMAP.md) · [Experiment Log](docs/EXPERIMENT_LOG.md) · [Case Studies](docs/CASE_STUDIES/)

## Screenshot

*(placeholder — add a capture of the Trade Desk with an active position)*
