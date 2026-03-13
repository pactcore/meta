# PACT Economic Framework (Current Implementation Snapshot)

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

## 3) Stablecoin Settlement (`implemented`)

The shipped stablecoin surface covers:

- deterministic routing and split execution
- escrow + pay-router contract flows
- staking and rewards settlement touchpoints
- SDK economics helpers aligned to the on-chain surface

## 4) Non-Stablecoin Settlement (`production-hardening`)

Non-stablecoin rails execute through dedicated connector contracts:

- `llm_token` -> `llm_metering` -> metering-credit connector (`applyMeteringCredit`)
- `cloud_credit` -> `cloud_billing` -> billing-credit connector (`applyBillingCredit`)
- `api_quota` -> `api_quota` -> quota-allocation connector (`allocateQuota`)

Current shipped behavior includes:

- merged JSON + env provider-profile loading
- credential alias normalization
- authenticated HTTP transport contracts
- request/response digest validation
- idempotency headers, retries, and circuit-breaker state
- reconciliation-ready settlement record generation

Remaining gap:

- live provider deployments, secret rotation, and audited upstream integrations

## 5) Valuation + Rail Planning

Current shipped valuation/planning surface includes:

- asset registry
- valuation registry (`assetId -> referenceAssetId`, `rate`, `asOf`, `source`)
- reference-asset quote API
- deterministic settlement rail planning by asset class

Remaining gap:

- live source-of-truth rate providers beyond the current reference-quote stage

## 6) Settlement Audit + Reconciliation (`production-hardening`)

Each non-stablecoin settlement leg generates an auditable settlement record:

- identity: `id`, `settlementId`, `legId`
- economics: `assetId`, `amount`, `unit`, `payerId`, `payeeId`
- routing: `rail`, `connector`
- execution: `status`, `externalReference`, `createdAt`
- optional connector payload: `connectorMetadata`

Settlement records follow explicit lifecycle:

- `applied`
- `reconciled`

Current shipped reconciliation surface includes:

- repository-backed durable settlement record contracts
- filter + cursor pagination for queries
- offset-based lifecycle replay
- explicit reconciliation metadata (`reconciledAt`, `reconciledBy`, `reconciliationNote`)
- economics settlement events plus reorg-aware on-chain bridge hooks

Remaining gap:

- persistent production indexer storage and operator-grade multi-network operations

## 7) API Contract Surface

Current execution/query endpoints:

- `POST /economics/settlements/execute`
- `GET /economics/settlements/records`
- `GET /economics/settlements/records/page`
- `GET /economics/settlements/records/replay`
- `GET /economics/settlements/records/:id`
- `POST /economics/settlements/records/:id/reconcile`

These endpoints expose connector-backed execution records for audit and reconciliation flows.

## 8) Current Whitepaper Implementation Gaps

The economic model is no longer blocked on protocol shape.
The remaining gaps are productionization work:

- managed database, queue, and observability backends
- live external billing/quota integrations
- production signer custody and finality/indexer operations
- examples and framework adapters for builder adoption
