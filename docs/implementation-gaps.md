# Whitepaper Implementation Gaps (as of 2026-03-13)

This document summarizes the remaining work between the shipped `core` / `sdk` / `contracts` surface and the whitepaper target state.
It is intentionally narrower than `docs/whitepaper-implementation-matrix.md`: this file tracks what is still missing, not what already shipped.

## Current Milestone

PACT has shipped the core protocol/runtime surface, SDK parity surface, and Appendix B on-chain contracts.
The main remaining gaps are production integrations, operational durability, and builder enablement.

## Gap Tracks

### 1) Runtime Durability + Managed Backends

Current shipped state:

- local-first persistence and replayable journals
- managed-backend inventory/profile loading
- health contracts for data/compute/dev backends
- queue/store/observability skeleton adapters
- SDK parity for backend health and credential metadata

Remaining gap:

- managed database, queue, store, and observability providers
- operational runbooks and production durability defaults

Exit signal:

- production deployments no longer depend on repo-local storage or skeleton adapters for core data paths

### 2) Settlement + Valuation Integrations

Current shipped state:

- stablecoin routing and split execution
- non-stablecoin settlement connector contracts
- provider-profile loading, auth-aware HTTP transport contracts, digest validation, idempotency, retries, and circuit-breaker state
- settlement record and reconciliation APIs
- stage-1 valuation registry and reference-quote API

Remaining gap:

- live external metering/billing/quota providers
- audited rate/source integrations beyond the current reference-quote stage
- production secret rotation for settlement providers

Exit signal:

- settlement rails run against live providers with audited upstream rate/source inputs and operator-grade credential rotation

### 3) On-Chain Operations

Current shipped state:

- Appendix B escrow, pay-router, identity, staking, governance, and rewards contracts
- governance/rewards bridge wiring in `core`
- validated contract addresses and pending-nonce synchronization
- reorg-aware finality and live onchain indexer SDK types

Remaining gap:

- persistent finality/indexer storage
- signer custody or HSM-backed operations
- multi-network deployment and operational hardening

Exit signal:

- production on-chain bridges run with persistent indexing, custody controls, and network-specific deployment/runbook coverage

### 4) Appendix C Prover Operations

Current shipped state:

- bridge runtime metadata and artifact manifests
- deterministic local prover integration
- remote HTTP prove/verify and artifact-fetch validation
- SDK parity for runtime, manifest, adapter-health, and receipts

Remaining gap:

- externally operated prover services
- production secret rotation
- artifact distribution hardening

Exit signal:

- proving infrastructure is externally operated, secret-managed, and resilient across artifact distribution paths

### 5) Builder Enablement

Current shipped state:

- typed SDK parity for missions, economics, managed backends, on-chain bridges, and Appendix C
- protocol/runtime documents and implementation matrix in `meta`

Remaining gap:

- `examples` repo with reference integrations
- framework adapters such as Next.js, NestJS, or Workers
- higher-level builder onboarding flows

Exit signal:

- new builders can integrate PACT through maintained examples and framework-native adapters rather than protocol-only primitives

### 6) Research / Simulation Domains

Current shipped state:

- simulation coverage for game-theoretic, matching, and security-analysis domains

Remaining gap:

- promotion of selected simulation tracks into production-grade runtime or ops surfaces

Exit signal:

- a simulation track gains a concrete protocol/runtime interface with durability, validation, and SDK parity expectations

## What Is Not Blocked

The current blocker set is not a missing protocol skeleton.
PACT already ships the main protocol/runtime, SDK, and contract surfaces described in the whitepaper.
The remaining work is concentrated in operational backends, live external integrations, and adoption tooling.
