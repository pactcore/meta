# PACT Runtime Specification (Draft v0.2 Stage-2)

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

## 4) Settlement Audit Contract

For each executed non-stablecoin leg, runtime must persist a settlement record containing:

- `id`, `settlementId`, `legId`
- `assetId`, `amount`, `unit`
- `payerId`, `payeeId`
- `rail`, `connector`
- `status`, `externalReference`, `createdAt`
- optional `connectorMetadata`

Runtime must emit:

- `economics.settlement_record_created` per record
- `economics.settlement_executed` per execution batch

## 5) Interop Contract (core <-> sdk)

- SDK settlement helpers must generate valid execute payloads for core APIs
- SDK runtime must support settlement record query by filter (`settlementId`, `assetId`, `rail`, `payerId`, `payeeId`)
- additive fields are minor-compatible; semantic breaks require major coordination
