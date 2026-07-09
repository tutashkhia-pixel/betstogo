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

### 2026-07-07 — Session 3 (field test: Argentina vs Egypt, World Cup R16)
- First field test of the mobile-first cockpit (v0.2–v0.3 era). Operator placed a real bet on Hard Rock and drove the app on the phone during the match.
- **Friction findings (drove the roadmap):** (1) too many setup fields — a friend's first reaction to the live link was "too many fields and numbers"; (2) no discoverable way out of a stuck open position on iPhone (shipped `/?reset`, v0.3.1); (3) setup placeholders ("Spain/Portugal") read as saved data.
- **Meta-finding:** the operator's actual workflow was screenshot-to-ChatGPT for portfolio management. This reframed the entire product thesis from single-bet manager to **live portfolio manager that replaces ChatGPT** — the v0.4 (Translator) and v0.5 (10-Second Loop) arcs are the direct response.
- Fixes shipped mid-session: `/?reset` escape hatch; team-name / neutral-venue language; Hard Rock market vocabulary; dark-only theme.

### 2026-07-08 — Session 4 (field test: France vs Morocco) — *planned*
- First run of the full v0.5 loop: event-first pulse, predicted chips, what-if, mid-match recording, and the screenshot lane (v0.5.1).
- **Data this session must produce:** real Hard Rock screenshots to tune OCR against (TEC-119); time-to-commit a pulse on a real device (target < 10s); whether predicted chips help or anchor; whether the what-if preview changed a decision.
- Journal entry + export required at close (dataset lives only in the browser).

### Template
```
### YYYY-MM-DD — Session N (match)
- Portfolio (bets on Hard Rock):
- Pulses committed (and lane used: tap / screenshot / type):
- Advice followed / overridden (and why):
- Mid-match actions (adds / cash-outs recorded):
- DQS:  P/L:
- Lessons:
```
