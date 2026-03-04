# PACT Runtime Specification (Draft v0.2 Stage-3)

This document defines the minimum runtime behavior for `core` and SDK-integrated workers.

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
5. event-linked auditability for mission/economic side effects

## 2) Mission Governance Contract

- conflicting verdicts must open challenge/escalation flow
- low-confidence approvals may be escalated by policy
- retries are bounded by mission `maxRetries`
- challenge resolution decides terminal state (`Settled` or `Failed`)

## 3) Economic Runtime Contract

- compensation models must be schema-valid before execution
- stage-1 supports valuation registration, reference quoting, and settlement rail planning
- stage-2 executes non-stablecoin legs through dedicated settlement connectors

Connector mapping:

- `llm_metering` -> metering credits
- `cloud_billing` -> billing credits
- `api_quota` -> quota allocation

## 4) Settlement Audit + Reconciliation Contract

For each executed non-stablecoin leg, runtime must persist a settlement record in a durable record repository abstraction.

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

## 5) Interop Contract (core <-> sdk)

- SDK settlement helpers must generate valid execute payloads for core APIs
- SDK runtime must support settlement/audit query helpers with filters:
  - `settlementId`, `assetId`, `rail`, `payerId`, `payeeId`
  - reconciliation filters: `status`, `reconciledBy`
  - pagination fields: `cursor`, `limit`
- SDK runtime must support settlement lifecycle replay querying (`fromOffset`, `limit`)
- additive fields are minor-compatible; semantic breaks require major coordination
