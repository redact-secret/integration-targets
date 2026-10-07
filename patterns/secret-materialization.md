# Secret materialization

Status: supported. Reviewed 2026-10-07.

## Problem

Configuration can be duplicated into a new checkout or retained in an environment snapshot. The extra copy has a different owner and lifetime from its source.

## Evidence and admission

[BATON-001](../targets/baton/findings.md#baton-001) and [CURSOR-002](../targets/cursor-cloud-agents/findings.md#cursor-002) are independent evidence for additional configuration storage. The multiple-target admission rule is met, though copying at launch and snapshotting are different mechanisms. No incident rate is inferred.

## Common data flow

```text
original configuration → copy or snapshot → additional storage lifetime
```

## Security consequence (inference)

Removing a checkout or stopping a process does not establish removal of backups, snapshots or downstream copies. Matching a filename does not prove its contents are sensitive.

## Product opportunity and ownership

Prefer avoiding unnecessary copies and the host/platform credential mechanism. Investigate [scoped runtime release](../capabilities/scoped-runtime-release.md) only when a concrete runtime consumer needs a value. Vault could authorize recovery; the host must deliver and clean up. Core cannot substitute a placeholder for a credential an application must actually use.

## Counterexamples and product boundary

[DevPod helpers](../targets/devpod/findings.md#devpod-001) are a counterexample to treating every remote credential path as whole-file copying. Environment delivery also leaves plaintext in processes. No universal disk-free guarantee follows.

Hosts retain authentication, runtime isolation, permissions, process/workspace lifecycle and retention. No pattern establishes that an external runtime is secured or that every sensitive value can be detected.

## Open questions

Which consumers can accept a narrowly delivered value or delegated operation? Which require a file? What evidence proves cleanup across failed starts and attached checkouts?

## Supporting targets

Finding links above are the authoritative support set. See the [cross-target comparison](../research/comparisons/agent-runtime-boundaries.md) for source, consumer, hook and retention differences.
