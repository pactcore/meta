# PACT Meta

PACT Meta is the strategic repo of the PACT ecosystem.
It defines how protocol execution, agent tooling, and ecosystem expansion fit into one coherent direction.

## Repositories

- [`pactcore/core`](https://github.com/pactcore/core)
  - Protocol engine: lifecycle invariants, validation, matching, reputation, settlement.
- [`pactcore/sdk`](https://github.com/pactcore/sdk)
  - Agent-builder toolkit: typed client plus future mission/event/policy runtimes.
- [`pactcore/meta`](https://github.com/pactcore/meta) (this repo)
  - Standards, principles, roadmap, and cross-repo governance.

## Narrative: Coordination Infrastructure for AI Agents

PACT evolves from a task protocol into a trust runtime for autonomous systems:

1. **Execution truth** (`core`) — deterministic rules and settlement outcomes
2. **Agent productivity** (`sdk`) — practical runtime tools for builders
3. **Strategic coherence** (`meta`) — shared standards and long-horizon roadmap

In short: **core defines truth, sdk scales intelligence, meta aligns the ecosystem**.

## Ecosystem Blueprint

```text
            ┌────────────────────┐
            │    pactcore/meta   │
            │ standards + vision │
            └─────────┬──────────┘
                      │
      ┌───────────────┴───────────────┐
      │                               │
┌─────▼─────┐                   ┌─────▼─────┐
│   core    │                   │    sdk    │
│ protocol  │                   │ agent dev │
│ runtime   │                   │ runtime   │
└─────┬─────┘                   └─────┬─────┘
      │                               │
      └───────────────┬───────────────┘
                      │
            ┌─────────▼─────────┐
            │ Apps / Agents /   │
            │ Institutional Ops │
            └───────────────────┘
```

## Documents in This Repo

- `docs/roadmap.md`
- `docs/agent-product-principles.md`
- `docs/terminology.md`
- `docs/runtime-spec.md`

## Next Suggested Repositories

- `pactcore/contracts` (on-chain contracts)
- `pactcore/indexer` (event ingestion + query layer)
- `pactcore/examples` (reference agent integrations)
- `pactcore/governance` (tokenomics and protocol governance)
