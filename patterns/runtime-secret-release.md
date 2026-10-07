# Runtime use and plaintext release boundary

Status: emerging. Reviewed 2026-10-07.

## Problem

A process or credential consumer may need a value that does not need to appear in model-visible text. Request eligibility, delivery, evidence filtering and lifetime are separate decisions.

## Evidence and admission

[Cursor secret classes](../targets/cursor-cloud-agents/findings.md#cursor-001), [Copilot scopes](../targets/github-copilot-agents/findings.md#copilot-001), [DevPod helper responses](../targets/devpod/findings.md#devpod-001) and [SDK terminal export](../targets/autonomous-coding-sandboxes/findings.md#sandbox-001) independently establish different runtime-access mechanisms. Admission is met, but status is emerging because a common trusted release/delivery contract is not qualified.

## Common data flow

```text
authorized source → runtime consumer → use; separate policy → model evidence
```

## Security consequence (inference)

A model that can control a consumer with plaintext access may cause further copies. A purpose string or a token supplied by the model does not establish permission. Revocation prevents future authorized release; it cannot retrieve a value already consumed.

## Product opportunity and ownership

Keep [scoped runtime release](../capabilities/scoped-runtime-release.md) a hypothesis. Vault owns capture/authority/lifecycle; restore reconstructs only after current authorization; host identity, isolation and injection remain external. Prefer existing platform secret or delegation mechanisms where adequate.

## Counterexamples and product boundary

Provider credentials do not necessarily enter workspaces. SSH agent forwarding is capability delegation, not plaintext-key release. Terminal lazy export may persist for a session. One generic authority vocabulary need not imply one transport or one vault profile.

Hosts retain authentication, runtime isolation, permissions, process/workspace lifecycle and retention. No pattern establishes that an external runtime is secured or that every sensitive value can be detected.

## Open questions

Can the host attest the actual destination outside agent control? What is the transaction boundary between consume, delivery and process launch? Which profiles support source/session binding without inventing fields?

## Supporting targets

Finding links above are the authoritative support set. See the [cross-target comparison](../research/comparisons/agent-runtime-boundaries.md) for source, consumer, hook and retention differences.
