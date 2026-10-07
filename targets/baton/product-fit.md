# Baton: product fit

Status: hypothesis for every target-specific application below. This is research, not implemented integration or qualified support.

## Finding-to-capability mapping

[BATON-002](findings.md#baton-002), [BATON-003](findings.md#baton-003) and [BATON-004](findings.md#baton-004) support [irreversible evidence sanitization](../../capabilities/irreversible-sanitization.md). Proposed owner: core, with host extraction and serialization. Apply it before log events fan out, before network-result serialization, and before history/proof writes. These are inspected source locations, not an existing supported plugin API.

[BATON-001](findings.md#baton-001) supports investigating [scoped runtime release](../../capabilities/scoped-runtime-release.md). A concrete need is application authentication during an approved development run. A host-controlled launcher, outside model-writable authority, would receive only approved environment fields. Replacing file copies is conditional: applications requiring files still need narrowly scoped materialization and host cleanup.

For an authenticated developer who must compare a selected original diagnostic field, [capture](../../capabilities/reversible-capture.md) plus [authorized restore](../../capabilities/authorized-restore.md) is an exceptional option. Restore output must go directly to that developer's trusted viewer, not back to MCP/model output. If inspection of the original value is unnecessary, do not retain a mapping.

## Minimum host hooks

The host must own canonical project/checkout identity, target and session binding, a non-bypassable launch point, live and persisted output interception, file permissions and termination. Filtering only `read_logs` misses history and proof. Images require the separate [visual boundary review](../../research/open-questions/qualification-gates.md#visual-evidence).

## Residual risk and non-goals

Baton remains responsible for daemon/MCP authentication, process trees, worktree ownership, simulator/device isolation and artifact cleanup. A process allowed to read a value can copy it; release expiry cannot erase prior copies. The comparison with Cursor, Copilot and DevPod is recorded in the [cross-target study](../../research/comparisons/agent-runtime-boundaries.md#baton-comparison).

## Qualification

Use the [qualification gates](../../research/open-questions/qualification-gates.md) before any support claim. Reversible release, runtime injection and visual handling need additional security review under [SECURITY.md](../../SECURITY.md). No such implementation is approved by this case study.
