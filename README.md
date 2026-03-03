# PACT Meta

PACT Meta is the strategic entrypoint of the PACT ecosystem.
It explains how protocol execution, developer tooling, and future network components fit together.

## Repositories

- [`pactcore/core`](https://github.com/pactcore/core)
  - Protocol engine: domain rules, lifecycle orchestration, validation, settlement.
- [`pactcore/sdk`](https://github.com/pactcore/sdk)
  - Developer integration layer: typed client, app/agent tooling, integration abstractions.
- `pactcore/meta` (this repo)
  - Vision, architecture narrative, ecosystem roadmap, cross-repo standards.

## Narrative: From Tasks to Trust Infrastructure

PACT starts as a task marketplace protocol and evolves into a trust coordination network:

1. **Execution** (`core`): deterministic protocol behavior
2. **Adoption** (`sdk`): low-friction integrations for builders
3. **Expansion** (future repos): indexers, contracts, governance, analytics, agent frameworks

In short: **core defines truth, sdk scales reach, meta defines direction**.

## Ecosystem Blueprint

```text
            ┌────────────────────┐
            │    pactcore/meta   │
            │ vision + standards │
            └─────────┬──────────┘
                      │
      ┌───────────────┴───────────────┐
      │                               │
┌─────▼─────┐                   ┌─────▼─────┐
│   core    │                   │    sdk    │
│ protocol  │                   │ developer │
│ runtime   │                   │ surface   │
└─────┬─────┘                   └─────┬─────┘
      │                               │
      └───────────────┬───────────────┘
                      │
            ┌─────────▼─────────┐
            │ Ecosystem Apps &  │
            │ Agent Integrators │
            └───────────────────┘
```

## Standards in This Repo

- Naming conventions
- Cross-repo version compatibility policy
- Documentation and release standards
- Long-term roadmap and milestones

## Next Suggested Repositories

- `pactcore/contracts` (on-chain contracts)
- `pactcore/indexer` (event ingestion and query layer)
- `pactcore/examples` (reference integrations)
- `pactcore/governance` (tokenomics and protocol governance specs)

See [`docs/roadmap.md`](./docs/roadmap.md) for phased milestones.
