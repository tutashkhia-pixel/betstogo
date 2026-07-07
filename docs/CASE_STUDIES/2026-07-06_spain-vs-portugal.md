# Case Study — Spain vs Portugal (2026-07-06)

*Product-learning case study, not a match recap. Sections marked "Unknown / needs operator input" await the operator's memory — do not fill them by invention.*

## Match context

UEFA Nations League final window. This match doubled as BETS→GO's build-day proving ground: the in-app walkthrough scenario was modeled on it, and the operator watched the real match the same day the terminal went live. Some learning happened away from the terminal.

## Original position (if known)

- In-app walkthrough position: **Spain ML +120, $100 stake** (this is the demo configuration and the journaled dry-run; preserved in the app's demo scripts).
- Real-money position on the live match: **Unknown / needs operator input.**

## Key pulse moments

From the in-app walkthrough (real pulse mechanics, scripted match state):
- **31' — GOAL Spain (1-0).** Win probability jumped ~25 points; live odds flipped from +130 to −160. The recalculation felt like the product's core moment: one input change, whole board reprices.
- **68' — Cash-out decision.** Book offered **$148** against a model hold value of **$179** (82% of fair). Terminal said **HOLD**; the pull to "take the money" was real even in a dry run.
- **Recovery variant (0-3 down at 80').** Engine armed, priced three live markets, and ruled **NO RECOVERY TRADE** — the correct answer was to do nothing while losing, which is emotionally the hardest output the product makes.
- Real-match pulse moments: **Unknown / needs operator input.**

## What BETS→GO helped clarify

- The **$148 vs $179** framing settled the cash-out question in seconds — the same question as "82% of EHV" left the operator computing in his head.
- The Action Board's side-by-side dollars (hold / cash out / partial) made the *shape* of the decision visible: what's locked, what's at risk, what's possible.
- The recovery engine's refusal ("nothing clears the EV bar") reframed standing down as a decision made, not a decision avoided.

## What was confusing

- Probability-first panels read slower than dollar-first panels under time pressure (Lesson 2).
- The cost of **not** acting was invisible: holding past a fair cash-out silently risks the whole offer, and nothing on screen said so (Lesson 4).
- Whether "the model disagrees with the book" meant *opportunity* or *warning* wasn't obvious — no counterargument was shown (led to Devil's Advocate copy).

## What the operator felt under pressure

- The urge to lock $148 despite a HOLD verdict — loss-aversion in real time.
- In the losing variant: the pull to "win it back" on the next-goal market. The NO RECOVERY TRADE banner functioned as an emotional circuit breaker.
- Relief when the screen said what he already suspected — the terminal as confirmation is comfortable; the terminal as *challenger* is where the value is.

## Cash-out / hedge / recovery lessons

- **Cash-out:** an offer at ~80% of hold value is a leak, not a gift. Rule of thumb the terminal teaches: the book prices your fear.
- **Hedge:** at 81% win probability the hedge engine correctly refused to arm — hedging a heavy favorite buys calm with EV.
- **Recovery:** independent pricing or nothing. Being down is not evidence.

## Product gaps exposed

1. No "cost of doing nothing" line (Lesson 4).
2. No prompt to look **up from the screen** — the operator is a field observer with information the model lacks (Lesson 5, 6).
3. No counterargument to the current verdict — trust needs friction (Lesson 1, "are we emotionally reacting?").
4. Side-by-side outcomes exist (Action Board) but must survive mobile pressure — ties to TEC-101.

## UI changes suggested

- Pulse Questions panel in the Live Console (who looks better / dangerous, momentum, emotion, thesis).
- "Cost of doing nothing" line under the Action Board.
- Devil's Advocate line under every primary verdict.
- Keep "Hold / No action" explicitly labeled as a valid, ranked option.

## What a disciplined 15-year-old trader should learn from this match

You had $100 on Spain. Spain scored, and someone offered you $148 to walk away — but the math said staying was worth $179. Taking the sure thing *feels* smart; over a season it quietly costs you money. And when the other scenario went 0-3, the smartest bet on the board was no bet at all. Patience is a position. Money you don't lose counts the same as money you win.

## Open questions

- Real-money entry, stake, and exit on the live match: **Unknown / needs operator input.**
- Did the operator follow the terminal's dry-run verdicts while watching live? **Unknown / needs operator input.**
- At what offer/EHV ratio does the operator *actually* start taking cash-outs? (Data arrives via TEC-97.)

## Product decisions created from this case

- Decision Ledger **#7** (case studies as product memory; 15-Year-Old Test as UI bar).
- Shipped in TEC-104: Pulse Questions panel, Cost of Doing Nothing line, Devil's Advocate copy, No-Action labeling.
- Reinforced priority of TEC-97 (recommendation tracking) and TEC-101 (mobile ergonomics).
