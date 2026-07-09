# Decision Ledger

Permanent product memory. Every important decision receives a numbered entry. The purpose is to preserve **why** the product evolved — implementation lives in git; reasoning lives here.

Entry format: Problem · Evidence · Alternatives Considered · Decision · Reasoning · Tradeoffs · Date · Related Linear Issue · GitHub Commit · Release · Status.

---

## Decision #1 — Single-file application

**Problem:** How should a shareable, fast-iterating experimental app be packaged?
**Evidence:** Day-one requirement: "an app I can quickly share with a friend"; game-day testing same afternoon left no room for build tooling.
**Alternatives considered:** Multi-file static site; bundler (Vite/esbuild); framework app with hosting pipeline.
**Decision:** One self-contained `index.html` — inline CSS/JS, zero dependencies, zero build.
**Reasoning:** Portability is the killer property at this stage: double-click, email attachment, artifact, any static host. Iteration speed beats code organization while the product is an experiment.
**Tradeoffs:** An ~80KB file with three languages in it; structural discipline must substitute for module boundaries; revisit when file size hurts more than a build step would.
**Date:** 2026-07-06 · **Linear:** pre-Linear (baseline) · **Commit:** a30eac3 · **Release:** v0.1.0 · **Status:** Active

## Decision #2 — Every engine produces facts; only the Decision Orchestrator produces advice

**Problem:** Recommendation logic was interleaved with probability math, making both hard to test, calibrate, or trust independently.
**Evidence:** Founder architecture directive 2026-07-07; anticipated calibration work (TEC-99) requires swappable, testable math.
**Alternatives considered:** Each engine emits its own recommendation; a rules layer per panel.
**Decision:** Hard boundary — engines return numbers with definitions; a single orchestrator turns facts into ranked, explained advice.
**Reasoning:** Models can be recalibrated without rewording advice; advice can be re-toned without touching math; the boundary keeps "what is true" separate from "what to do," which is the product's core integrity claim.
**Tradeoffs:** Slight indirection; the orchestrator is a chokepoint by design.
**Date:** 2026-07-07 · **Linear:** TEC-96 (operating model) · **Commit:** a30eac3 · **Release:** v0.1.0 · **Status:** Active — non-negotiable

## Decision #3 — MarketAdapter architecture, football first

**Problem:** Product direction oscillated between football-only, multi-sport platform, and experiment-first minimalism — the code needed to survive all three.
**Evidence:** Three founder scope changes within 24 hours (2026-07-06 → 07); long-term vision names multi-market support.
**Alternatives considered:** Hard-coded football app (cheapest now); full plugin system with dynamic loading (heaviest).
**Decision:** Market-agnostic core + a `MarketAdapter` contract (model, market catalog, events, clock, inputs, demos); `FootballAdapter` is the only implementation; registry holds one entry.
**Reasoning:** The adapter seam let strategy change three times while code changed once. Architecture should absorb product changes cheaply.
**Tradeoffs:** ~15% more code than hard-coding; the contract is unproven until a second adapter exists (deliberately deferred).
**Date:** 2026-07-07 · **Linear:** pre-Linear (baseline) · **Commit:** a30eac3 · **Release:** v0.1.0 · **Status:** Active

## Decision #4 — Experiment-first scope: validate before scaling

**Problem:** Feature ambition (multi-sport, live data, integrations) competed with the unproven core premise.
**Evidence:** Founder recalibration 2026-07-07: "Our goal is to determine whether BETS→GO measurably improves live sports trading decisions."
**Alternatives considered:** Build toward the platform vision immediately; split effort between validation and features.
**Decision:** Everything gates on the hypothesis. Deferred explicitly: live data, additional adapters, notifications, backtesting, accounts. Milestones are evidence quantities (10 matches, 20 matches), not feature bundles.
**Reasoning:** An unvalidated decision-support tool that grows features grows liability, not value. The journal + DQS is the measurement instrument; recommendation tracking (TEC-97) makes the hypothesis directly answerable.
**Tradeoffs:** The product looks "small" for a while; some momentum sacrificed for learning.
**Date:** 2026-07-07 · **Linear:** BETS→GO project charter · **Commit:** a30eac3 · **Release:** v0.1.0 · **Status:** Active

## Decision #5 — Netlify is canonical production

**Problem:** The app shipped via a claude.ai artifact first; after a deploy, the artifact rendered blank while the identical file verified perfect locally.
**Evidence:** 2026-07-07 verification session: balanced markup, zero console errors locally; blank at the artifact host across refreshes. Sandbox had also blocked localStorage earlier (fixed by graceful degradation).
**Alternatives considered:** Debug the artifact platform; dual-canonical URLs.
**Decision:** https://betstogo.netlify.app is the production URL; the artifact is a courtesy mirror, never load-bearing.
**Reasoning:** Production must be a host we can verify (readable console, charset control, deploy logs). "Netlify answers: what is currently live."
**Tradeoffs:** Friend-share links migrate to the Netlify URL.
**Date:** 2026-07-07 · **Linear:** pre-Linear (baseline) · **Commit:** a30eac3 · **Release:** v0.1.0 · **Status:** Active

## Decision #6 — Linear is the product brain; evidence-gated backlog

**Problem:** Reasoning behind changes lived in chat history; features risked accumulating without justification.
**Evidence:** Founder operating model 2026-07-07; week-one pivots already hard to reconstruct.
**Alternatives considered:** GitHub issues; docs-only; no tracker (chat-driven).
**Decision:** Linear project **BETS→GO** in TechEdge labs (TEC namespace, `[BGO]` title prefix). Every issue carries Problem/Observation/Experiment/Hypothesis/Decision/AC/Links. Evidence label group (`live-session`, `tester`, `hypothesis`, `none`) — `evidence: none` may exist but may not start. Team workflows untouched (shared with other projects).
**Reasoning:** GitHub answers *what changed*, Netlify answers *what's live*, Linear answers *why it exists*. The evidence gate operationalizes "protect the experiment" without ceremony.
**Tradeoffs:** TEC prefix is shared with other TechEdge projects (mitigated by `[BGO]`); label-based gating relies on discipline rather than workflow enforcement.
**Date:** 2026-07-07 · **Linear:** TEC-96, TEC-103 · **Commit:** (this commit) · **Release:** post-v0.1.0 · **Status:** Active

## Decision #7 — Case studies as product memory; the 15-Year-Old Test as UI bar

**Problem:** Day-1 live-session learning (Spain vs Portugal; USA vs Belgium) lived only in the operator's head, and the UI didn't reflect what the sessions taught.
**Evidence:** Operator-reported lessons from 2026-07-06 live sessions (see docs/CASE_STUDIES/): dollars beat probabilities under pressure; the cost of inaction was invisible; the operator is a field observer whose observations the app never prompted; recommendations must survive a 10-second comprehension test.
**Alternatives considered:** Journal-only capture (loses narrative context); building bigger features first (violates experiment-first).
**Decision:** Create `docs/CASE_STUDIES/` as a first-class product-memory format. Adopt the **15-Year-Old Test** as the permanent comprehension bar (manifesto). Ship only the small UI changes the cases justify: Pulse Questions panel, Cost of Doing Nothing line, Devil's Advocate copy, explicit No-Action labeling.
**Reasoning:** Preserve learning before scaling features; every shipped change traces to a named lesson; devil's-advocate copy adds the trust-through-friction the sessions showed was missing.
**Tradeoffs:** More vertical space in the Live Console; more advice text per verdict (kept to one sentence each); case studies contain "Unknown / needs operator input" gaps by policy rather than invented detail.
**Date:** 2026-07-07 · **Linear:** TEC-104 · **Commit:** (this commit) · **Release:** v0.1.1 · **Status:** Active

## Decision #8 — Canonical ownership: one owner per knowledge object

**Problem:** Product knowledge was growing in three places (repo docs, Linear issues, Decision Ledger) with no rule preventing drift or conflicting truth.
**Evidence:** Founder observation 2026-07-07 after TEC-105–110 created full narratives inside Linear that overlap with `docs/CASE_STUDIES/`.
**Alternatives considered:** Linear as permanent archive (fast but unversioned, drifts from git); docs-only (loses fast capture and discussability); accept duplication (guarantees eventual conflict).
**Decision:** Every knowledge object has exactly one canonical owner (table in OPERATING_MODEL.md). Lifecycle: Observe → Capture (Linear) → Distill (Ledger) → Archive (GitHub docs) → Build → Ship. Graduation rule: Linear holds raw narratives temporarily; reviewed knowledge graduates to docs; the issue keeps summary + links. Weekly anti-drift ritual.
**Reasoning:** Capture needs speed; archives need permanence and version history. Splitting the roles gets both; the graduation step is the bridge. Duplication is temporary; conflicting truth is never permanent.
**Tradeoffs:** Graduation is a manual step that relies on the weekly ritual; TEC-105–110 remain intentionally un-graduated until David reviews and fills the unknowns.
**Date:** 2026-07-07 · **Linear:** TEC-96 · **Commit:** (this commit) · **Release:** post-v0.1.1 · **Status:** Active

## Decision #9 — Decision-companion redesign; Apple/Linear/Arc/TradingView design language

**Problem:** The v0.2 terminal read like an admin dashboard that happened to know football — borders on everything, uppercase mono headers, five KPI tiles before the verdict, neon semantics on blue-black. A first-time viewer's reaction: "too many fields and numbers."
**Evidence:** Founder brief 2026-07-07 with a reference mock; the explicit target feelings were "Apple, Linear, Arc, TradingView — premium, calm, trustworthy, expensive, and easy for a 15-year-old." Direction was presented as an Artifact and approved before any code.
**Alternatives considered:** Incremental polish of the existing terminal; copy the reference pixel-for-pixel.
**Decision:** Extract a design *language* rather than copy artwork. Six laws: speak don't label · one decision per screen · depth from light not lines · gold is for action (scarce) · dollars in mono / words in prose · calm is trust. Ship as v0.2.1 (polish) then v0.3.0 (full system): warm-metal tokens, gradient-lit cards with a top-edge light catch, true gold accent, sage/coral semantics, engine panels demoted to disclosures, five-tile money strip merged into the decision card.
**Reasoning:** The intelligence was never the problem; the vocabulary and density were. A calm, one-decision-per-screen surface serves the 15-Year-Old Test and the "read in 10 seconds under pressure" requirement directly.
**Tradeoffs:** Larger CSS surface; a design system to maintain; system-font-only (no webfont) to preserve the single-file, no-build constraint.
**Date:** 2026-07-07 · **Linear:** TEC-113 · **Commit:** ef13391, e9c354d · **Release:** v0.2.1, v0.3.0 · **Status:** Active

## Decision #10 — Dark-only theme

**Problem:** The app followed the device's light/dark setting, so the same operator saw gold-on-black on desktop (dark) and warm-paper on iPhone (light, default in daytime) — "why does my phone look different?"
**Evidence:** Founder observation 2026-07-08 during setup; matches are watched at night / on a phone at low brightness where the dark theatre is the real one.
**Alternatives considered:** Keep both themes and add an in-app toggle; hard-lock light.
**Decision:** Remove the light theme. Warm-dark renders on every device regardless of OS appearance. Light-theme tokens deleted; the `prefers-color-scheme` split collapsed to one palette.
**Reasoning:** One theatre, one look — the design direction already named dark "the primary theatre." Eliminates a whole class of "looks different / looks broken" confusion.
**Tradeoffs:** No daylight-optimized reading mode; revisit only if field use demands it.
**Date:** 2026-07-08 · **Linear:** TEC-114 · **Commit:** 33371db · **Release:** v0.3.2 · **Status:** Active

## Decision #11 — The fundamental unit of analysis is the PORTFOLIO, not the wager

**Problem:** The app managed a single bet. Real live trading on Hard Rock is a *portfolio* — multiple simultaneous positions (Winner, Spread, Total, SGP, props) whose combined exposure to each game outcome is what actually matters. "Every ticket is simply another position contributing to the portfolio's overall exposure."
**Evidence:** Founder thesis 2026-07-08: manage live bets as a dynamic portfolio; every new bet must raise EV, cut downside, or create asymmetric upside — never just add action. Approved as the v0.4 design direction ("The Translator").
**Alternatives considered:** Bolt a second bet onto the single-bet model; keep bets independent and sum naively (ignores correlation).
**Decision:** State `S.bet` → `S.positions[]`. Each score-determined bet becomes a payoff rule over the model's existing joint final-score grid (`cellWins` + `buildMat`); portfolio EV / worst / best, net exposure per result (Home/Draw/Away), and correlated-risk coverage all derive from one aggregation. Path-dependent (next goal) and manual-probability bets contribute expected value flatly, labeled as such. v0.3 single-bet states migrate to one-bet portfolios.
**Reasoning:** The joint grid the Poisson model already produces *is* the portfolio engine — a bet is a payoff map over it, and correlation (e.g. two goal-market SGP legs) prices exactly, better than the books' own fudge. No new math; new bookkeeping. This is the largest state-shape change since Day 1 and the moment the app matched how the operator actually trades.
**Tradeoffs:** First migration of the state shape (guarded: unmigratable legacy states are discarded, not crashed on — TEC-112, v0.4.1); player props need an operator-supplied probability; the file crossed ~110KB.
**Date:** 2026-07-08 · **Linear:** TEC-112 · **Commit:** 582264b, 37e366c · **Release:** v0.4.0, v0.4.1 · **Status:** Active

## Decision #12 — The Translator: the interface speaks Hard Rock or plain English; engine vocabulary never reaches the screen

**Problem:** The UI still spoke *model* — "Hold EV", "Edge −7 pts", "AI Win Prob", "Home Moneyline", "ticket". The operator has to translate that against Hard Rock in their head, which defeats a companion meant to be used mid-match beside the sportsbook.
**Evidence:** Founder principle 2026-07-08: "BETS→GO should never force the user to learn BETS→GO. It should speak Hard Rock's language. The intelligence should be invisible. Hard Rock → Portfolio Decision — that's the entire product."
**Alternatives considered:** A glossary/help layer; keep engine terms with tooltips.
**Decision:** Every on-screen word must appear on a Hard Rock screen or be a plain-English verdict. Verdicts become portfolio verbs: HOLD · ADD · REDUCE · HEDGE · REBALANCE · CASH OUT. Markets read in Hard Rock terms ("Winner — Argentina", "Total Goals — Over", "Both Teams to Score — Yes"); team names substitute live into every dropdown; "ticket" → "bet" / "My Bets" everywhere; neutral-venue labels ("First team / Second team", no home-field assumption in the model). The xG/edge/EV math still runs — it just stops being the interface (engine room disclosures).
**Reasoning:** Zero-translation is the differentiator. The model is a second opinion; Hard Rock is the market; the operator is the only actor. Keeping engine vocabulary off the cabin surface is what makes the tool feel like an extension of Hard Rock rather than a separate system to learn.
**Tradeoffs:** A string-vocabulary discipline to maintain; verdict/tracking strings remain load-bearing (compared in `followed()` and stored in journals) so they change carefully.
**Date:** 2026-07-08 · **Linear:** TEC-115 · **Commit:** 1e45bd3, 24150fd, f63b197, 96d84c4, 7078e69 · **Release:** v0.4.2–v0.4.6 · **Status:** Active

## Decision #13 — Derive expected goals from the Winner odds

**Problem:** Setup asked for pre-match xG per side — the two most intimidating fields on the screen, and unanswerable for a non-modeler even with a helper tip. Contributed to the "too many fields" reaction.
**Evidence:** Field-test finding #1 (2026-07-07 Argentina–Egypt) and the friend's first-look reaction; the operator already types the Winner odds, which encode team strength (and venue).
**Alternatives considered:** Keep xG with better copy; hide xG behind an "advanced" toggle only.
**Decision:** A small solver derives the xG pair from the three Winner prices (implied probabilities → best-fit λ pair, ~10ms). xG fields survive behind a "More options" disclosure as an override; if left at defaults, odds win.
**Reasoning:** Kills the scariest inputs, keeps the model honest (the odds are the market's own strength estimate, venue already priced), and shrinks setup toward "teams + what's on your bet slip."
**Tradeoffs:** The derived pair is only as good as the entered odds; a manual override remains for anyone who wants it.
**Date:** 2026-07-08 · **Linear:** TEC-116 · **Commit:** 5355624 · **Release:** v0.5.0 · **Status:** Active

## Decision #14 — The 10-Second Loop and Law #0 (Hard Rock is the only source of truth)

**Problem:** The screenshot-to-ChatGPT ritual worked because a screenshot is a zero-typing input device and ChatGPT already knew the operator's philosophy. BETS→GO replaced the counselor but still made the operator transcribe numbers into a form.
**Evidence:** Founder workflow brief 2026-07-08 ("during a live match, BETS→GO becomes the companion that replaces my screenshot-to-ChatGPT workflow… minimize typing, immediate recommendation… surprise me with the best UX"). Presented as the v0.5 design direction ("The 10-Second Loop") and approved.
**Alternatives considered:** A faster form; voice input (parked — iPhone browser support too unreliable).
**Decision:** Flip the update from "tell me the numbers" to "here's what I predict — confirm." The sheet opens *event-first* (⚽ GOAL <team> / 🟥 RED CARD / 👀 CHECK); an event sets score and re-prices everything; every Cash Out and board price appears as **predicted chips** (the model's guess ±1 notch) to tap. The Translate button previews the verdict live ("Translate → HEDGE"). **Law #0:** predicted chips are labeled guesses, nothing persists until the operator taps, skipped numbers keep the last confirmed value with a visible age, and a model guess can never become data. The **CHECK trigger is recorded with every pulse** (event / time / domination / gut) and lands in the journal — the operator's instincts join the decision-quality experiment.
**Reasoning:** Prediction makes agreement one tap and, crucially, makes *disagreement loud* — a real number far from every chip is itself the mispricing signal, so input and analysis become the same step. Law #0 keeps the app from grading its own homework: the model is a second opinion, Hard Rock is the market.
**Tradeoffs:** Predictions can anchor; mitigated by clearly marking them guesses and by the divergence-is-signal framing. Recording check triggers adds one field to the pulse snapshot.
**Date:** 2026-07-08 · **Linear:** TEC-117 · **Commit:** 5355624 · **Release:** v0.5.0 · **Status:** Active

## Decision #15 — What-if previews and mid-match add/cash-out recording

**Problem:** The other half of the ChatGPT ritual was "what would my portfolio look like if I added this?" — and the app could only set up bets before kickoff, so mid-match adds and cash-outs left the portfolio and the tracking record untruthful until the review screen.
**Evidence:** Founder workflow brief 2026-07-08 (the portfolio "what-if" conversation) and the REBALANCE/ADD verdicts, which already assumed the operator could act mid-match.
**Alternatives considered:** Leave mid-match reality to the post-match review only; auto-settle on the model's guess (violates Law #0).
**Decision:** Every watched-market row and the recommendation card open a **what-if**: portfolio EV / worst / best / "covers your losing results" before → after, stake editable. "I placed it on Hard Rock" adds the bet live; "I cashed this on Hard Rock" settles any bet mid-match with realized P/L. Both auto-record advice-followed; the review prefills from what actually happened.
**Reasoning:** Makes the discipline visible (the preview shows the *portfolio* delta, not the wager's appeal) and keeps the portfolio and the experiment's data truthful in real time — the operator declares reality; the app never fabricates it.
**Tradeoffs:** Partial cash-outs (REDUCE) still trust the operator to execute on Hard Rock rather than tracking partial fills (TEC-121).
**Date:** 2026-07-08 · **Linear:** TEC-117 · **Commit:** 5355624 · **Release:** v0.5.0 · **Status:** Active

## Decision #16 — The screenshot lane: on-device OCR, self-hosted (the single-file rule bends)

**Problem:** The fastest possible input is the screenshot the operator already takes. Reading it requires an OCR engine — which is ~27MB of library, WASM cores, and a language model that cannot live inside `index.html`.
**Evidence:** Founder request 2026-07-08 to keep the exact screenshot habit but redirect it from ChatGPT to BETS→GO; screenshot-assisted entry was the long-parked "most realistic input upgrade" (TEC-111 scope note).
**Alternatives considered:** Third-party OCR CDN at runtime (fails on stadium wifi, and a 45s cold-load hung the tab in testing); a cloud OCR API (breaks the privacy promise — the image would leave the phone); no screenshot lane.
**Decision:** Add tesseract.js + cores + the English model under `vendor/`, served from the app's own origin, lazy-loaded on first use of the lane. OCR is **assistive, never trusted**: extracted dollar amounts and odds appear as **📷 chips** beside the predicted chips; nothing persists until the operator taps one (Law #0 holds). Watchdog timeouts fall back to a plain message; the tap lane is unaffected if OCR fails. Decision #1 (single-file) is formally amended: `index.html` stays the whole *application*; `vendor/` holds only third-party static assets that physically cannot be inlined.
**Reasoning:** Self-hosting is the only option that satisfies all three constraints at once — works offline-ish on bad wifi, keeps the image on the device (nothing uploaded, no account, no scraping), and stays deployable to a static host. The image never leaving the phone is the whole point.
**Tradeoffs:** Repo grows ~27MB; first-use load is slow (cached after); OCR accuracy on the real Hard Rock layout is unverified until the next field test produces genuine screenshots to tune against (TEC-118).
**Date:** 2026-07-08 · **Linear:** TEC-118 · **Commit:** 7d53046 · **Release:** v0.5.1 · **Status:** Active

---

*Next entry: #17. Append only; never rewrite history — supersede with a new entry and update the old entry's Status.*
