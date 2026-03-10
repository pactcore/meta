# PACT Ecosystem Roadmap

## Current Status (2026-03-10)

- Synced `meta` against latest code-bearing commits `core` `8d33fad`, `sdk` `8d280c6`, `contracts` `15e84d0`, and `landing-and-whitepaper` branch `docs/batch-34-traceability-sync` at `644dcb4`.
- `production-hardening` shipped in the latest core delta: env/profile-driven remote prover config loading, explicit remote endpoint and credential health errors, and manifest-catalog validation plus health classification for the required Appendix C proof types.
- `implemented` in the current contracts delta: Appendix B escrow, pay-router, identity, staking, governance, and rewards contracts remain the landed on-chain surface; no newer contracts commit changed matrix status in this sync.
- `implemented` in SDK parity: on-chain finality queries plus async transaction tracking/inclusion/canonical-block writes, async signer contracts, widened managed-backend and settlement-connector health/profile contracts, stablecoin-bridge settlement request/result types, reconciliation queue/summary helpers, and Appendix C bridge runtime/manifest accessors with external prover request/verify types.
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
  Shipped env-configured managed-backend inventory loading, local managed-backend contracts and health summaries for data/compute/dev, lifecycle mirroring of data publications/integrity proofs, compute job/checkpoint outcomes, and dev integration/template/policy events into managed queue/store/observability surfaces, remote queue/store/observability skeleton adapters, and SDK parity for live-backend health payloads and adapter contracts.
  Blocker: real managed queue/store/observability providers and persistent operational backends.
- `implemented`: on-chain contract integration (`contracts` repo)
- `production-hardening`: on-chain bridge configuration and nonce management
  Shipped normalized non-zero unique contract-address validation and RPC-backed pending-nonce synchronization in `core`, plus SDK helpers to track transactions, record transaction inclusion, record canonical blocks, and model async finality-provider/signer contracts.
  Blocker: live deployment registries, persistent finality indexer operations, and signer custody.
- `implemented`: protocol-level challenge/appeal and dispute pathways for validator disagreement
- `production-hardening`: multi-asset settlement connectors (stablecoin + token budgets + credits + quotas)
  Shipped stablecoin routing/splits plus provider-authenticated live-facing connectors for `llm_metering`, `cloud_billing`, and `api_quota`, including request digests, idempotency headers, retries, circuit-breaker state, idempotency, provider-profile loading, and SDK parity for richer connector health/runtime metadata.
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
- `implemented`: SDK modules for mission/events/policy/evidence/agent runtime, plus economics/data/compute/dev parity, managed-backend health endpoints and adapter contracts, settlement runtime helpers, stablecoin-bridge connector contracts and reconciliation filters, richer health/runtime metadata parity, and on-chain finality/Appendix C runtime-manifest parity
- `future work`: framework adapters (Next.js, NestJS, Workers)
- `future work`: multi-language SDK strategy planning

## Appendix C Track

- `production-hardening`: zk bridge/runtime APIs, artifact manifests, and verification receipts
  Shipped bridge runtime metadata, manifest versioning, manifest-catalog health classification across required proof types, env/profile-backed remote prover config loading, deterministic local prover integration, remote HTTP skeleton coverage, SDK receipt/runtime/manifest accessors, and external prover request/verify contract types.
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
