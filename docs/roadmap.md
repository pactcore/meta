# PACT Ecosystem Roadmap

## Batch 36 Status (2026-03-10)

- Synced `meta` against `core` commit `146a81f`, `sdk` commit `d4834f4`, `contracts` commit `15e84d0`, and `landing-and-whitepaper` commit `d30f8c3`.
- `production-hardening` shipped in the latest core delta: env-configured live settlement adapters, provider-profile loaders, fetch-backed settlement transports, signer abstractions, RPC/indexer finality sync with reorg hooks, managed-backend health contracts for data/compute/dev, and Appendix C manifest/runtime/receipt APIs.
- `implemented` in the current contracts delta: Appendix B escrow, pay-router, identity, staking, governance, and rewards contracts remain the landed on-chain surface; no newer contracts commit changed matrix status in this sync.
- `implemented` in SDK parity: on-chain finality queries, Appendix C receipt accessors, managed-backend health endpoints, reconciliation queue/summary helpers, and idempotency-aware settlement execution.
- Remaining `production-hardening` blockers: real managed queue/store/observability providers, production signer custody + persistent indexer backends, live external billing/quota providers beyond env-backed transports, non-skeleton remote prover operations, and developer-facing examples/framework adapters.

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

- `production-hardening`: production adapters for storage, queues, and observability
  Shipped local managed-backend contracts and health summaries for data/compute/dev plus a remote queue skeleton path.
  Blocker: real managed queue/store/observability providers and persistent operational backends.
- `implemented`: on-chain contract integration (`contracts` repo)
- `implemented`: protocol-level challenge/appeal and dispute pathways for validator disagreement
- `production-hardening`: multi-asset settlement connectors (stablecoin + token budgets + credits + quotas)
  Shipped stablecoin routing/splits plus provider-authenticated live-facing connectors for `llm_metering`, `cloud_billing`, and `api_quota`, including retries, circuit-breaker state, idempotency, and provider-profile loading.
  Blocker: production provider rollout, secret management, and audited upstream integrations.
- `production-hardening`: cross-asset valuation adapters (reference quote + source-of-truth rates)
  Shipped stage-1 valuation registry + reference quote API.
  Blocker: live source-of-truth rate providers.
- `implemented`: deterministic settlement-rail planning by asset class
  Shipped stage-1 settlement-plan rail mapping API.
- `production-hardening`: chain reconciliation and settlement audit pipelines
  Shipped settlement record APIs, economics settlement events, reconciliation queue/summary views, signer abstractions, RPC finality/indexer sync, and reorg hooks.
  Blocker: persistent indexer storage, production signer custody, and multi-network operations hardening.

## Phase 3 — Agent Developer Growth

- `future work`: launch `examples` with worker/validator agent templates
- `implemented`: SDK modules for mission/events/policy/evidence/agent runtime, plus economics/data/compute/dev parity, managed-backend health endpoints, and on-chain finality/Appendix C parity
- `future work`: framework adapters (Next.js, NestJS, Workers)
- `future work`: multi-language SDK strategy planning

## Appendix C Track

- `production-hardening`: zk bridge/runtime APIs, artifact manifests, and verification receipts
  Shipped bridge runtime metadata, manifest versioning, deterministic local prover integration, remote HTTP skeleton coverage, and SDK receipt accessors.
  Blocker: externally operated prover services and production artifact distribution.

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
