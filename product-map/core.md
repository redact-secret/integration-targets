# Core ownership

Core owns detection, its policy evaluation, irreversible replacement and safe finding metadata. It remains usable alone; the optional anonymizer must not turn it into a scan-only dependency.

The [pinned core README](https://github.com/redact-secret/redact-secret/blob/f6f481b168b000ac27e8d60598cd2cb5c0265d59/README.md), inspected 2026-10-07, documents existing scan/redact and incremental operations. It also states that supported formats are bounded and PII is opt-in with qualification limits. This review did not run the product's tests, and it makes no new runtime, detector or PII support claim.

Research input: [agent evidence](../patterns/agent-evidence-boundary.md) and [persisted evidence](../patterns/persisted-debug-evidence.md) motivate the [host evidence contract](../capabilities/irreversible-sanitization.md). The contract remains a hypothesis even where core primitives exist.

The host acts on block decisions, extracts structured fields and prevents raw fallback. Core must not own capture mappings, identity, release authorization, persistence, process injection or screenshot handling. A detector miss remains possible; safe metadata must not include original values.
