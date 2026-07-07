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

---

*Next entry: #9. Append only; never rewrite history — supersede with a new entry and update the old entry's Status.*
