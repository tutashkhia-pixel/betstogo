# Experiment Log

## Hypothesis

> Using BETS→GO during live football trading measurably improves decision quality compared to trading without it.

## Method

- Trade real matches with the terminal open; commit pulse updates at events and checkpoints.
- Close every position through the post-match review; the journal records P/L **and** Decision Quality Score (0–100, process-based).
- DQS is the primary metric; P/L is tracked but noisy at small samples.
- Success signal after 10–20 matches: DQS trending up, fewer negative-EV actions (chasing, bad cash-outs), and subjective "would not trade without it."

## Sessions

### 2026-07-06 — Session 1 (game-day pilot)
- First real-world use planned around a live match; app validated same-day with demo walkthroughs and one journaled position.
- Outcome: prototype passed first real-world validation (operator's assessment). Friction noted: needed spread/handicap support mid-day (shipped), needed a way to discard a test position (shipped).

### Template
```
### YYYY-MM-DD — Session N (match)
- Position:
- Pulses committed:
- Advice followed / overridden (and why):
- DQS:  P/L:
- Lessons:
```
