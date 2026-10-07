# Persisted debug evidence

Status: supported. Reviewed 2026-10-07.

## Problem

A diagnostic collected for one execution can become a retained run artifact. Filtering what is displayed later cannot undo the original storage event.

## Evidence and admission

[Baton proof/history](../targets/baton/findings.md#baton-004), [Cursor retention](../targets/cursor-cloud-agents/findings.md#cursor-002) and [SDK event files](../targets/autonomous-coding-sandboxes/findings.md#sandbox-002) independently demonstrate evidence persistence. The admission rule is met. Formats and lifecycle differ; no uniform retention period is asserted.

## Common data flow

```text
live evidence → history / proof / event artifact → later readers and exports
```

## Security consequence (inference)

Retention expands the time and audience in which sensitive content could be encountered. A retry may collect a new copy even after a prior artifact was sanitized.

## Product opportunity and ownership

Apply [irreversible sanitization](../capabilities/irreversible-sanitization.md) before each intended storage sink. Hosts own artifact composition, retention and export. [Reversible capture](../capabilities/reversible-capture.md) needs a separate mapping lifecycle and authenticated destination; an artifact should not carry its own release authority.

## Counterexamples and product boundary

A network snapshot is not necessarily a body capture. Text and image copies require separate coverage. Native vendor masking may already apply to some stored surfaces; this study does not demonstrate otherwise.

Hosts retain authentication, runtime isolation, permissions, process/workspace lifecycle and retention. No pattern establishes that an external runtime is secured or that every sensitive value can be detected.

## Open questions

Where are raw spill files or intermediate traces created? Can retries reuse sanitized evidence? Which storage deletion and visual exclusion controls are enforceable?

## Supporting targets

Finding links above are the authoritative support set. See the [cross-target comparison](../research/comparisons/agent-runtime-boundaries.md) for source, consumer, hook and retention differences.
