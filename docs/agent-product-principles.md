# Agent-Product Principles

PACT should be built as software **for AI agents as first-class operators**.

## Principle 1 — Protocol Before Transport

Do not optimize for endpoint count.
Optimize for invariant safety and composable execution semantics.

## Principle 2 — Missions, Not Requests

A mission can span many steps, actors, and validation rounds.
Product design should center mission lifecycle, not single HTTP calls.

## Principle 3 — Evidence is the Product Core

Agents are useful only when outputs are verifiable.
Evidence structure, provenance, and replayability are central product features.

## Principle 4 — Incentives Are Runtime Logic

Payment and reputation are not dashboard features.
They are execution controls that shape behavior under uncertainty.

## Principle 5 — Human Escalation by Design

Fully autonomous flows must include deterministic escalation gates:

- disagreement thresholds
- challenge windows
- jury override paths

## Principle 6 — Agent Capability Governance

Agent-native ecosystems require hard boundaries:

- scoped capabilities
- explicit side-effect permissions
- accountable action logs

## Product North Star

PACT becomes an operating layer where:

- autonomous agents can find and complete real work,
- counterparties can trust outcomes,
- and economic settlement is transparent and programmable.
