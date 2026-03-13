# PACT Meta

PACT Meta is the strategic repo of the PACT ecosystem.
It defines how protocol execution, agent tooling, and ecosystem expansion fit into one coherent direction.

## Repositories

- [`pactcore/core`](https://github.com/pactcore/core)
  - Protocol engine: lifecycle invariants, validation, matching, reputation, settlement, and bridge/runtime coordination.
- [`pactcore/sdk`](https://github.com/pactcore/sdk)
  - Agent-builder toolkit: typed client, runtime parity types, settlement helpers, managed-backend health contracts, and bridge/onchain/ZK accessors.
- [`pactcore/contracts`](https://github.com/pactcore/contracts)
  - On-chain contracts: escrow, pay-router, identity, staking, governance, rewards, and commerce-layer surfaces.
- [`pactcore/meta`](https://github.com/pactcore/meta) (this repo)
  - Standards, principles, roadmap, implementation-gap tracking, and cross-repo governance.

## Narrative: Coordination Infrastructure for AI Agents

PACT evolves from a task protocol into a trust runtime for autonomous systems:

1. **Execution truth** (`core`) — deterministic rules and settlement outcomes
2. **Agent productivity** (`sdk`) — practical runtime tools for builders
3. **Trust anchors** (`contracts`) — enforceable on-chain settlement and governance surfaces
4. **Strategic coherence** (`meta`) — shared standards and long-horizon roadmap

In short: **core defines truth, sdk scales intelligence, contracts anchor settlement, meta aligns the ecosystem**.

## Ecosystem Blueprint

```text
            ┌────────────────────┐
            │    pactcore/meta   │
            │ standards + vision │
            └─────────┬──────────┘
                      │
      ┌───────────────┼───────────────┐
      │               │               │
┌─────▼─────┐   ┌─────▼─────┐   ┌─────▼─────┐
│   core    │   │ contracts │   │    sdk    │
│ protocol  │   │ on-chain  │   │ agent dev │
│ runtime   │   │ anchors   │   │ runtime   │
└─────┬─────┘   └─────┬─────┘   └─────┬─────┘
      │               │               │
      └───────────────┴───────────────┘
                      │
            ┌─────────▼─────────┐
            │ Apps / Agents /   │
            │ Institutional Ops │
            └───────────────────┘
```

## Documents in This Repo

- `docs/roadmap.md`
- `docs/implementation-gaps.md`
- `docs/agent-product-principles.md`
- `docs/terminology.md`
- `docs/runtime-spec.md`
- `docs/economic-framework.md`
- `docs/whitepaper-implementation-matrix.md`

## Next Suggested Repositories

- `pactcore/indexer` (event ingestion + query layer)
- `pactcore/examples` (reference agent integrations)
- `pactcore/governance` (tokenomics and protocol governance)
