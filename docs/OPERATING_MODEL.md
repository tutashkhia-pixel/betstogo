# Operating Model

The canonical operating model for BETS→GO. If a process question isn't answered here, the answer gets added here — nowhere else.

---

## Principle #0 — CANONICAL OWNERSHIP

Every knowledge object has exactly one canonical owner.

**Capture quickly. Distill carefully. Archive permanently. Everywhere else links.**

Duplication is temporary. Conflicting truth is never permanent.

## The knowledge lifecycle

**Observe → Capture → Distill → Archive → Build → Ship**

| Stage | What it is |
|---|---|
| **Observe** | Raw conversations, screenshots, game-day notes, emotional reactions, and unstructured founder thinking. |
| **Capture** | Linear issues. Fast, messy, incomplete, discussable. Unknowns are allowed. |
| **Distill** | Decision Ledger. Only what survives review becomes a product decision. |
| **Archive** | GitHub docs. Durable product knowledge, case studies, architecture, principles, manifesto. |
| **Build** | GitHub commits and branches. |
| **Ship** | Netlify production deploys and GitHub releases. |

## Canonical ownership table

| Knowledge | Canonical owner |
|---|---|
| Active work | Linear |
| Product thinking / raw lessons | Linear capture issues |
| Product decisions | `docs/DECISION_LEDGER.md` |
| Case studies | `docs/CASE_STUDIES/` |
| Experiment results | `docs/EXPERIMENT_LOG.md` |
| Architecture | `docs/ARCHITECTURE.md` |
| Beliefs / principles | `docs/FOUNDER_MANIFESTO.md` |
| Code | GitHub repository |
| Releases | Git tags + GitHub Releases |
| Production | Netlify |

## The graduation rule

Linear may temporarily hold full narratives while they are raw. Once reviewed, durable knowledge **graduates** into GitHub docs. The Linear issue then keeps only summary, links, and status.

**Capture in Linear. Archive in Git.**

Applied to the existing Founder Memory container (TEC-105 and children TEC-106–110): these are **capture buffers, not permanent archives**. After David reviews and fills the unknowns, durable case-study content graduates into `docs/CASE_STUDIES/` and the Linear issues link back to it.

## The anti-drift ritual

During the weekly 30-minute review, ask:

> "Is the same knowledge written in more than one place?"

If yes, choose the canonical owner and replace duplicates with links.

---

## Roles of the three systems

- **GitHub answers: "What changed?"** — source code, docs, releases, branches, version history.
- **Netlify answers: "What is currently live?"** — production deployment only. https://betstogo.netlify.app
- **Linear answers: "Why does this exist?"** — the product brain. Every feature begins life as a Linear issue.

## The evidence gate

Every meaningful change must trace to a real **observation**, **experiment**, **hypothesis**, or **validated user pain**.

- The `evidence` label group marks the source: `live-session` · `tester` · `hypothesis` · `none`.
- An issue labeled `evidence: none` may exist in the backlog but **may not start**.
- **If David requests a feature that cannot be tied to an observation, experiment, hypothesis, or validated user pain — challenge him before implementing.** This is a standing instruction, not a suggestion.

## Issue template

Every BETS→GO issue (titles prefixed `[BGO]`, TEC namespace):

```
Problem:
Observation:            (what real event triggered this)
Experiment:             (what we'll measure to know it worked)
Hypothesis:
Decision:               (one line at close + "→ Ledger #n" when applicable)
Acceptance Criteria:
Links:                  (commit · release · deploy URL)
```

## Cross-referencing convention

- Branches: Linear-generated names (e.g. `davidakirtava/tec-97-...`).
- Commits: issue key in subject — `feat: recommendation tracking [TEC-97]`; `Fixes TEC-97` to auto-close via the GitHub integration.
- Releases: notes list shipped issue keys; shipped issues get the release + deploy URL in Links.
- The triangle: any of GitHub / Linear / Netlify reaches the other two in one click.

## Cadence

- **Per session:** close with the product-historian recap — what changed · what was learned · architecture decisions · product decisions · assumptions · risks · recommended Linear issues · documentation updates · whether the work strengthened or weakened the core hypothesis.
- **Weekly (30 min):** journal DQS trend → pick the one next experiment → prune `evidence: none` issues untouched for two weeks → run the anti-drift ritual.
- **Per release:** tag → release notes with issue keys → verify production → close issues with deploy links.
- **Monthly:** North Star check — is the hypothesis progressing? Persevere, pivot, or kill.

## Definition of Done

Verified live on production **+** historian entry **+** issue linked both ways (commit ↔ issue ↔ deploy).

## Engineering and product principles (constant)

- Every engine produces **facts**. Only the Decision Orchestrator produces **advice**. Never violate this boundary.
- Every release must improve at least one of: **decision quality · trust · explainability · operator speed · capital preservation** — never feature count.
- Architecture absorbs product change cheaply: optimize for adaptability over today's requirements.
- The comprehension bar is the **15-Year-Old Test** (see FOUNDER_MANIFESTO.md).
- The success metric: **"Would I refuse to trade without BETS→GO open?"** Indispensable, not larger.
