# PACT Ecosystem Roadmap

## Batch 34 Status (2026-03-10)

- Synced `meta` against `core` commit `a6bdfb3` and `sdk` commit `811f4ff`.
- Shipped in the latest core/sdk delta: settlement connector idempotency + health/reset APIs, reconciliation run/pending views, compute checkpoint/retry/cancel runtime contracts, file-backed data-asset metadata, and adapter health summaries for data/compute/dev.
- Shipped in SDK parity: economics reconciliation/connector helpers plus compute/data/dev runtime and health endpoints.
- Remaining blockers: provider-authenticated live settlement connectors, live signer/RPC finality + reorg-safe on-chain execution, managed storage/queue/observability backends, production zk circuits/provers, and developer-facing examples/framework adapters.

## Phase 0 — Foundation (Now)

- Establish `core`, `sdk`, and `meta`
- Lock naming, architectural boundaries, and invariant definitions
- Ship first protocol-safe runtime + baseline SDK

## Phase 1 — Agent Runtime Hardening

- Shipped mission envelopes and context persistence in `core`
- Shipped event inbox/outbox semantics and replayable journals
- Shipped capability policy model for autonomous action control
- Shipped compatibility matrix and parity surface (`core` <-> `sdk`)

## Phase 2 — Trust and Settlement Expansion

- In progress: production adapters for storage, queues, and observability
- Shipped on-chain contract integration (`contracts` repo)
- Shipped protocol-level challenge/appeal and dispute pathways for validator disagreement
- In progress: multi-asset settlement connectors (stablecoin + token budgets + credits + quotas)
  - Shipped stablecoin routing/splits plus stage-2 in-memory connectors for `llm_metering`, `cloud_billing`, `api_quota`
  - Blocker: provider-authenticated live billing, quota, and credit connectors
- In progress: cross-asset valuation adapters (reference quote + source-of-truth rates)
  - Shipped stage-1 valuation registry + reference quote API
  - Blocker: live source-of-truth rate providers
- In progress: deterministic settlement-rail planning by asset class
  - Shipped stage-1 settlement-plan rail mapping API
- In progress: chain reconciliation and settlement audit pipelines
  - Shipped stage-2 settlement record API, economics settlement events, reconciliation run/pending views, and connector health/reset flows
  - Blocker: live signer, RPC confirmation/finality, and reorg-safe indexer handling

## Phase 3 — Agent Developer Growth

- In progress: launch `examples` with worker/validator agent templates
- Shipped SDK modules for mission/events/policy/evidence/agent runtime, plus economics/data/compute/dev parity
- Future work: framework adapters (Next.js, NestJS, Workers)
- Future work: multi-language SDK strategy planning

## Phase 4 — Network Effects and Governance

- Multi-tenant validator market and quality scoring
- Reputation graph analytics and fraud intelligence
- Governance process and upgrade pipeline
- Institutional onboarding standards and compliance profiles

## Guiding Principle

PACT should evolve from an app feature set into agent-era infrastructure:

- **Reliable enough for institutions**
- **Simple enough for independent builders**
- **Programmable enough for autonomous agents**
