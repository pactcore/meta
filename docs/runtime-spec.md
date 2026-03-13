# PACT Runtime Specification (Current Implementation Snapshot)

This document defines the minimum runtime behavior for `core` and SDK-integrated workers.
It reflects the currently shipped protocol/runtime surface and its remaining production gaps.

## 1) Worker Loop Contract

Conforming runtimes follow:

```text
poll events -> claim mission -> execute -> submit evidence -> checkpoint -> repeat
```

Required guarantees:

1. deterministic state progression
2. replayable event cursor handling
3. persisted checkpoints for recovery
4. capability policy enforcement on mission actions
5. event-linked auditability for mission and economic side effects

## 2) Mission Governance Contract

- conflicting verdicts must open challenge/escalation flow
- low-confidence approvals may be escalated by policy
- retries are bounded by mission `maxRetries`
- challenge resolution decides terminal state (`Settled` or `Failed`)

## 3) Economic Runtime Contract

Runtime must support:

- schema-valid compensation models before execution
- deterministic settlement rail planning by asset class
- stablecoin routing/splits through the shipped on-chain surface
- non-stablecoin execution through dedicated settlement connectors
- settlement-record creation and explicit reconciliation lifecycle

Connector mapping:

- `llm_metering` -> metering credits
- `cloud_billing` -> billing credits
- `api_quota` -> quota allocation

Current shipped connector behavior includes provider-profile loading, auth-aware HTTP transport contracts, request/response digest validation, idempotency, retries, and circuit-breaker state.

## 4) Settlement Audit + Reconciliation Contract

For each executed non-stablecoin leg, runtime must persist a settlement record through a durable repository abstraction.

Record schema (minimum):

- `id`, `settlementId`, `legId`
- `assetId`, `amount`, `unit`
- `payerId`, `payeeId`
- `rail`, `connector`
- `status`, `externalReference`, `createdAt`
- optional `connectorMetadata`
- optional reconciliation fields: `reconciledAt`, `reconciledBy`, `reconciliationNote`

Runtime must emit:

- `economics.settlement_record_created` per record
- `economics.settlement_record_reconciled` when record lifecycle moves to reconciled
- `economics.settlement_executed` per execution batch

Lifecycle replay + query pagination requirements:

- query must support filter + cursor pagination (`cursor`, `limit`)
- lifecycle replay must support offset pagination (`fromOffset`, `limit`)
- replay entries include `offset`, `action`, `recordId`, `settlementId`, `status`, `occurredAt`

Required reconciliation endpoint contract:

- `POST /economics/settlements/records/:id/reconcile`
  - marks record lifecycle state from `applied` -> `reconciled`
  - accepts optional operator metadata (`reconciledBy`, `note`, `reconciledAt`)
  - returns updated settlement record

Recommended query/replay transport endpoints:

- `GET /economics/settlements/records/page`
- `GET /economics/settlements/records/replay`

## 5) Managed Backend Contract

Data, compute, and dev runtime modules must expose managed-backend health and profile summaries.

Current shipped behavior includes:

- env-configured backend inventory loading
- JSON + env profile merging
- normalized required/configured credential field summaries
- queue/store/observability skeleton adapter contracts
- SDK parity for health payloads and credential metadata

Remaining production gap:

- real managed queue, store, and observability providers replacing local-first and skeleton defaults

## 6) On-Chain Bridge + Finality Contract

Runtime bridge surfaces must support:

- validated non-zero unique contract addresses
- signer abstractions
- pending-nonce synchronization
- transaction tracking, inclusion recording, and canonical block recording
- finality summaries and reorg-aware indexer hooks

SDK parity must expose typed transaction, finality-provider, signer, and live onchain indexer contracts.

Remaining production gap:

- persistent indexer storage, live deployment registries, and signer custody/HSM integration

## 7) Appendix C Prover Bridge Contract

The prover bridge surface must support:

- runtime metadata and manifest access
- manifest versioning and health classification
- deterministic local proving
- remote HTTP prove/verify flows
- request/response digest validation
- remote artifact fetch integrity validation
- verification receipts exposed through SDK parity

Remaining production gap:

- externally operated prover services, production secret rotation, and artifact distribution hardening

## 8) Interop Contract (`core` <-> `sdk`)

- SDK helpers must generate valid payloads for core APIs
- SDK runtime must support settlement, managed-backend, on-chain, and prover query helpers
- additive fields are minor-compatible; semantic breaks require major coordination

## 9) Current Whitepaper Implementation Gaps

The main remaining gaps are operational, not protocol-structure gaps:

- managed durability backends beyond file-backed/SQLite defaults
- live external settlement and valuation providers
- production on-chain operations and custody
- externally operated prover infrastructure
- examples and framework adapters for wider builder adoption
