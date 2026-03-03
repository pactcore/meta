# PACT Runtime Specification (Draft v0.1)

This spec defines minimum runtime behavior expected from agent implementations integrating with PACT.

## 1. Loop Contract

A conforming worker runtime should follow:

```text
poll events -> claim mission -> execute -> emit evidence -> submit -> checkpoint -> repeat
```

## 2. Required Guarantees

1. **Deterministic progression**
   - runtime must not skip protocol lifecycle constraints
2. **Replayability**
   - runtime should process events via cursor semantics and support replay
3. **Recoverability**
   - runtime should persist checkpoints between loop iterations
4. **Policy enforcement**
   - claim/submit actions must pass capability/policy checks
5. **Auditability**
   - mission-critical actions should map to protocol events

## 3. Mission Governance Behavior

- conflicting verdicts should trigger challenge/escalation flow
- low-confidence approvals may be escalated by policy
- failed missions may be retried only within bounded limits (`maxRetries`)
- challenge resolution determines final mission status (`Settled` or `Failed`)

## 4. Supervisory Behavior

- heartbeat tasks are independent from mission loops
- heartbeat execution should be schedulable and observable via events
- supervisory tasks must not bypass capability policy boundaries

## 5. Interop Expectations (core <-> sdk)

- runtime event payloads should maintain stable field names for cursors and identifiers
- additive fields are allowed in minor versions
- breaking semantic changes require major version upgrade coordination
