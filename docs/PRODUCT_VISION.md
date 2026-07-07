# Product Vision

Imagine sitting beside a world-class trader who watches every match, monitors every betting market, understands risk, explains every decision in plain English, shows every outcome in real dollars, never panics, never chases losses, and updates their advice every minute as new information arrives.

That is BETS→GO. Not an AI that predicts sports — an AI that helps humans make better trading decisions.

## What it is

A professional trading workstation (think Bloomberg Terminal + F1 race strategy + sports analytics) that answers one question continuously:

> "What is the highest-quality decision I can make RIGHT NOW based on all available information?"

Possible answers: Place Bet · Hold · Wait · Cash Out · Partial Cash Out · Hedge · Recovery Trade · **No Action**. The system never feels obligated to recommend a wager.

## What it is not

- Not a betting picker.
- Not a gambling bot.
- Not a system that promises profits.

## Core philosophy

Trade the match. Protect capital. Never chase losses. Every recommendation supported by objective evidence and explainable. The quality of the decision matters more than the outcome of a single match.

## The signature feature: Recovery Opportunity Engine

Recovery trades are **not** hedges. When the original position is effectively dead, the engine scans available live markets and prices each **independently on its own merit** — model probability vs. implied probability, EV, quarter-Kelly stake. If no positive-EV trade exists, the verdict is **NO RECOVERY TRADE**. Being down is never a reason to bet.

## v0.1.0 scope (manual MVP)

The operator types in what they see (score, minute, live odds, cash-out offer, available markets); the system computes probabilities, edge, EV, ranked actions, alerts, and journals every closed position with a Decision Quality Score. Football is the first supported market; the primary sportsbook context is Hard Rock Bet (American odds).

## Long-term direction (all deferred until the hypothesis is validated)

Licensed live data feeds and odds providers · additional market adapters (other sports) · push notifications · strategy backtesting · portfolio analytics · Kelly staking options. The application always remains advisory: it analyzes, quantifies, and explains — the final wagering decision belongs to the user.
