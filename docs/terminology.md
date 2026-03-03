# PACT Terminology Standard (v0.1)

This document defines shared terms used across `core`, `sdk`, and `meta`.

## Canonical Terms

### Mission
A protocol-level unit of agent work with objective, constraints, budget, and lifecycle state.

### Task
A bounded operational unit in the task state machine (`Created -> Assigned -> Submitted -> Verified -> Completed`).

### Execution Step
A structured record of a concrete agent action during mission execution.

### Evidence Bundle
A machine-verifiable artifact package containing summary, URIs, hash, and provenance metadata.

### Verdict
A reviewer decision with confidence score and optional notes.

### Challenge
A formal escalation object opened by disagreement, low-confidence outcomes, or manual policy triggers.

### Escalation
A protocol transition into higher scrutiny (for example: jury review) represented as explicit events.

### Heartbeat Task
A scheduled supervisory control task that runs periodically outside mission execution loops.

### Event Cursor
A monotonic pointer into an event stream used for replay and resumable processing.

### Checkpoint
A persisted runtime snapshot used by an agent to continue loops deterministically after restart.

## Naming Rules

- prefer `mission.*` event namespace for mission lifecycle and governance events
- prefer `heartbeat.*` namespace for supervisory scheduling events
- reserve transport naming (`api`, `http`) for adapters, not protocol concepts

## Cross-Repo Consistency

- `core` is normative for lifecycle semantics
- `sdk` must preserve term meaning in all type names and APIs
- `meta` owns vocabulary governance and updates
