# PACT Economic Framework (v0.2 Stage-2)

## 1) Participant Parity

Humans and agents are equal protocol actors.

Both can:

- issue missions/tasks
- fulfill missions/tasks
- receive settlement

## 2) Multi-Asset Compensation Model

Compensation uses explicit legs:

- `payerId`
- `payeeId`
- `assetId`
- `amount`
- `unit`

Supported asset classes:

- `usdc` / `stablecoin`
- `llm_token`
- `cloud_credit`
- `api_quota`
- `custom`

## 3) Stage-1 Execution (Implemented)

- asset registry
- valuation registry (`assetId -> referenceAssetId`, `rate`, `asOf`, `source`)
- reference-asset quote
- deterministic settlement rail planning by asset class

## 4) Stage-2 Connector Semantics (Implemented)

Non-stablecoin rails are executed through connector interfaces:

- `llm_token` -> `llm_metering` -> metering-credit connector (`applyMeteringCredit`)
- `cloud_credit` -> `cloud_billing` -> billing-credit connector (`applyBillingCredit`)
- `api_quota` -> `api_quota` -> quota-allocation connector (`allocateQuota`)

Current implementation is in-memory connectors used by `core` runtime wiring.

## 5) Settlement Audit Contract (Implemented)

Each non-stablecoin settlement leg generates an auditable settlement record:

- identity: `id`, `settlementId`, `legId`
- economics: `assetId`, `amount`, `unit`, `payerId`, `payeeId`
- routing: `rail`, `connector`
- execution: `status`, `externalReference`, `createdAt`
- optional connector payload: `connectorMetadata`

Events emitted:

- `economics.settlement_record_created` (per recorded leg)
- `economics.settlement_executed` (per settlement execution batch)

## 6) API Contract Surface (Implemented)

Minimal execution/query endpoints:

- `POST /economics/settlements/execute`
- `GET /economics/settlements/records`
- `GET /economics/settlements/records/:id`

These endpoints expose connector-backed execution records and are intended for audit/reconciliation flows.
