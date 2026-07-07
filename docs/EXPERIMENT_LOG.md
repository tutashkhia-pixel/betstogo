# Experiment Log

## Hypothesis

> Using BETS→GO during live football trading measurably improves decision quality compared to trading without it.

## Method

- Trade real matches with the terminal open; commit pulse updates at events and checkpoints.
- Close every position through the post-match review; the journal records P/L **and** Decision Quality Score (0–100, process-based).
- DQS is the primary metric; P/L is tracked but noisy at small samples.
- Success signal after 10–20 matches: DQS trending up, fewer negative-EV actions (chasing, bad cash-outs), and subjective "would not trade without it."

## Sessions

### 2026-07-06 — Session 1 (game-day pilot: Spain vs Portugal)
- First real-world use planned around a live match; app validated same-day with demo walkthroughs and one journaled position.
- Outcome: prototype passed first real-world validation (operator's assessment). Friction noted: needed spread/handicap support mid-day (shipped), needed a way to discard a test position (shipped).
- Full product-learning write-up: [CASE_STUDIES/2026-07-06_spain-vs-portugal.md](CASE_STUDIES/2026-07-06_spain-vs-portugal.md)

### 2026-07-06 — Session 2 (live viewing: USA vs Belgium)
- Watched live outside the terminal; betting specifics Unknown / needs operator input (policy: never invented).
- Distilled lessons: dollars beat probabilities under pressure; cost of inaction invisible; operator = field observer; pulse checks should ask observational questions; the 15-Year-Old Test born here.
- Product response shipped in v0.1.1 (TEC-104): Pulse Questions panel, Cost of Doing Nothing line, Devil's Advocate copy.
- Full product-learning write-up: [CASE_STUDIES/2026-07-06_usa-vs-belgium.md](CASE_STUDIES/2026-07-06_usa-vs-belgium.md)

### Template
```
### YYYY-MM-DD — Session N (match)
- Position:
- Pulses committed:
- Advice followed / overridden (and why):
- DQS:  P/L:
- Lessons:
```
