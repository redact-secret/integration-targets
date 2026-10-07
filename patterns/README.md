# Patterns

Patterns name evidenced boundaries, not vendor-specific integration plans. Admission follows [CONVENTIONS.md](../CONVENTIONS.md); each document links its supporting findings and counterexamples.

- [Agent evidence and observation](agent-evidence-boundary.md), supported: runtime observations become agent input.
- [Secret materialization](secret-materialization.md), supported: copies/snapshots create additional storage lifetimes.
- [Persisted debug evidence](persisted-debug-evidence.md), supported: live evidence becomes a durable artifact.
- [Runtime use and release](runtime-secret-release.md), emerging: runtime access, model visibility and authority remain distinct.

Supported describes evidence for recurrence, not proven mitigation. Observation is consolidated into agent evidence; remote development remains a context in the [comparison](../research/comparisons/agent-runtime-boundaries.md), avoiding duplicate placeholder patterns.
