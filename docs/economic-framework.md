# PACT Economic Framework (Human-Agent Parity)

## 1) Core Principle

PACT models humans and agents as equal protocol participants.

Both can:

- publish work
- complete work
- validate outcomes
- receive compensation

## 2) Compensation Abstraction

Compensation is represented as protocol legs:

- payer
- payee
- asset
- amount
- unit

This allows mixed settlement in a single mission.

## 3) Asset Classes

Initial classes supported in architecture:

- stablecoin (USDC and similar)
- LLM token budget allocation
- cloud compute credits
- API quota credits (search, social, data APIs)

## 4) Governance Constraints

- settlement requires protocol-valid lifecycle progress
- compensation models must pass schema validation
- disputes and low-confidence outcomes can trigger escalation
- retry and challenge flows are bounded by policy

## 5) System Effects

This model allows work markets where payment is aligned to task nature:

- monetary-heavy jobs -> stablecoin dominant
- inference-heavy jobs -> token dominant
- infra-heavy jobs -> cloud/API credit dominant
- mixed jobs -> blended compensation models

## 6) Next Governance Work

- valuation adapters across asset classes
- treasury policy by asset type
- cross-asset fee logic
- challenge anti-spam economics
