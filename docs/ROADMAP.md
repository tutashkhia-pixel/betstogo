# Roadmap

Milestones are gated by the experiment (see EXPERIMENT_LOG.md), not by feature ambition.

## v0.1.0 — First Public MVP ✅ (current)

Single-file terminal: manual live inputs, Poisson football model, cash-out/hedge/recovery engines, dollars-first risk strip, ranked Action Board, pulse alerts, decision-quality journal, MarketAdapter architecture.

## Next milestone — make it feel like a professional terminal, and validate

- **Recommendation tracking**: journal what the orchestrator advised at each pulse vs. what the operator did — the direct measurement of the hypothesis.
- Sample size: 10–20 real matches in the journal; review DQS trend and advice-followed vs. outcome deltas.
- Polish from real use: whatever friction the live sessions expose (input speed, screenshot entry, mobile ergonomics).

## Deferred (explicitly — do not build until the hypothesis is validated)

- Live data feeds / odds APIs
- Additional market adapters (NBA, NFL, tennis, …)
- Push notifications
- Strategy backtesting, portfolio analytics
- Accounts, sync, multi-device
- Multi-file build tooling

## Branches

- `main` — stable, deployable.
- `feature/live-data` — prepared for the (deferred) live-data milestone; empty by design.
