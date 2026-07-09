# Roadmap

Milestones are gated by the experiment (see EXPERIMENT_LOG.md), not by feature ambition. The success metric remains: **"Would I refuse to trade without BETS→GO open?"**

## Shipped

- **v0.1.0 — First MVP.** Single-file terminal: manual live inputs, Poisson football model, cash-out/hedge/recovery engines, dollars-first risk strip, ranked Action Board, pulse alerts, decision-quality journal, MarketAdapter architecture.
- **v0.1.1 — Day-1 lessons.** Pulse Questions panel, Cost of Doing Nothing line, Devil's Advocate copy, explicit No-Action labeling. [TEC-104]
- **v0.2.0 — Recommendation tracking + mobile-first cockpit.** Journal records advice-vs-action per pulse (the hypothesis instrument); phone becomes the primary surface. [TEC-97, TEC-111]
- **v0.2.1 → v0.3.x — Decision-companion redesign.** Apple/Linear/Arc/TradingView design language; warm-metal system; dark-only; "Live Manager" branding; `/?reset` escape hatch. [TEC-113, TEC-114]
- **v0.4.x — The Translator (portfolio pivot).** The unit of analysis becomes the portfolio; portfolio verbs; interface speaks Hard Rock; team-name markets; "My Bets" vocabulary. [TEC-112, TEC-115]
- **v0.5.0 — The 10-Second Loop.** Event-first pulse, predicted chips (Law #0), verdict-preview Translate button, what-if previews, mid-match add/cash-out recording, xG derived from odds, CHECK-trigger recording. [TEC-116, TEC-117]
- **v0.5.1 — The screenshot lane.** On-device, self-hosted OCR reads the operator's Hard Rock screenshot into 📷 chips; nothing uploaded. [TEC-118]

## Now — validate the loop in the field

The build has raced ahead of the evidence. The next milestone is **evidence, not features**:

- **10–20 real matches journaled** on the v0.5 loop. Review the DQS trend and, now that recommendation tracking is live, the **followed-vs-overridden outcome delta** — the direct test of the hypothesis. [TEC-97 instrument; TEC-99 calibration]
- **OCR tuning on real Hard Rock screenshots.** v0.5.1 was validated against a synthetic slip; the real layout is unverified. The next field test produces the tuning data. [TEC-118]
- **Comprehension bar for all UI work:** the **15-Year-Old Test** — a recommendation understood in 10 seconds, in real dollars, without hype.

## Backlog (evidence-gated — see Linear for full acceptance criteria)

- **Player props / non-goal SGP legs** priced properly (currently manual-probability only). [TEC-119]
- **Partial cash-out / REDUCE tracking** — record partial fills instead of trusting the operator to execute on Hard Rock. [TEC-120]
- **Check-trigger analytics** — does the operator's intuition (the CHECK trigger) actually catch things the schedule wouldn't? [TEC-121]
- **Strip vig from implied probabilities** — edge is overstated by the book's margin. [TEC-98]
- **Model calibration report** from journaled outcomes (reliability curve). [TEC-99]
- **Journal backup / export nudge** — the whole dataset lives in one browser. [TEC-100]

## Deferred (explicitly — do not build until the hypothesis is validated)

- Voice input (parked — iPhone browser support too unreliable to bet a match on).
- PWA install + push reminders (needs home-screen install; separate discussion).
- Live data feeds / odds APIs · additional market adapters (NBA, NFL, tennis) · strategy backtesting, portfolio analytics · accounts, sync, multi-device.
- **Never:** any scraping of or login to the operator's Hard Rock account. The operator is the sensor; the app makes sensing nearly free. Advisory only.

## Branches

- `main` — stable, deployable; production is https://betstogo.netlify.app.
