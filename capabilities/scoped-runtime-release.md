# Scoped runtime secret release

Status: hypothesis. Security review required before implementation or qualification: new release path, runtime injection and any remote authority. No new supported security profile is established.

## Problem and concrete need

[Runtime use](../patterns/runtime-secret-release.md) and [materialization](../patterns/secret-materialization.md) show why a designated application or Git/Docker consumer can need credentials without giving the model their plaintext. Prefer the platform's existing secret/delegation facility; a vault-backed path is warranted only if it adds a demonstrable scope or lifecycle benefit.

A candidate destination is a host-controlled development process environment field, such as `env.SYNTHETIC_SERVICE_TOKEN`. This is an illustrative field name, not a supported runtime API. Applications requiring files need a separately authorized narrow file destination and cleanup contract.

## Proposed request and trusted context

The host produces the following context from authenticated configuration and runtime state. Model-supplied requests can nominate a task, never attest these facts.

| Context | Trusted producer | Relationship to current vault |
| --- | --- | --- |
| Source/capture, exact sink and field path | Host capture registry and destination registry | `captures`, `release.sink`, `release.paths`, restore `sink` and `fields`; no inferred wildcard |
| Principal, tenant, purpose, session | Authenticated host/server policy | Server context and policy; a session label alone does not prove a process identity |
| Project, checkout, target and process instance | Host launcher and canonical workspace registry | Candidate policy inputs/host bindings, not newly invented core vault API fields |
| Expiry, revocation, use limit and current policy | Vault authority plus host lifecycle signal | Existing lifecycle concepts; a runtime delivery transaction still needs design |

References: [in-memory vault](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/docs/reference/vault.md), [server authority](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/docs/reference/vault-server.md), pinned and reviewed 2026-10-07. Their documented sink/path/capture and server policy model is evidence for reuse; it is not proof of runtime isolation or a generic launch contract.

## Ownership and flow

1. The host verifies the intended workload and destination outside the agent's writable control. It restricts inherited environment, descriptors, logs and temporary files.
2. Vault authorizes the entire requested field set under current policy. In reversible flows it owns retained mappings, grants, expiry/revocation and use budgets.
3. Restore, if reconstruction is needed, plans all occurrences and obtains an all-or-nothing result through the authority contract. Plain credential delegation need not invoke a token reconstruction engine.
4. The host delivers directly to the approved process or service. It does not return plaintext to the model, tool transcript or proof artifact.
5. The host reports end/cancellation and cleans up its resources; vault revokes future use according to policy.

The output is a delivery result and safe metadata to the caller, not a plaintext environment map returned to the model. The trusted delivery component necessarily handles plaintext when the consumer requires it.

## Failure and residual risk

Do not launch on partial authorization, use a broader grant on retry, or fallback to copying the source secret file. Define how retries are deduplicated and how authority consumption relates to delivery before prototyping. A crash after consumption but before delivery may spend a use without successful launch; do not promise rollback or exactly-once delivery without a proven transaction.

No plaintext file is needed only when the consumer accepts environment or another controlled channel. Environment delivery is not confidentiality from an agent that controls that same process or can inspect its state. Revocation/expiry cannot retract values, child-process inheritance, dumps or copies already made. A file fallback is not secure erasure.

DevPod helper lookup, SSH signing delegation, Baton worktree copying and cloud-agent secrets use different transports and trust boundaries. Reuse an authority vocabulary where justified; do not force them into one credential store or one implementation.

## Qualification needed

A disposable synthetic host must demonstrate an actual trust boundary separating the model from the authorized consumer, authenticated source/sink binding, atomic denial, no raw logs/artifacts, fail-closed launch behavior and cancellation handling. Test wrong project/checkout/session/target/path, changed policy, expiry, revocation, concurrent budgets and ambiguous delivery. Process isolation and attestation are host prerequisites, not vault tests.

Open decisions: target identity representation, use-consumption point, persistent/remote profile selection, file fallback lifecycle and trusted-host enforcement. Until those close, this document is research input, not a release-ready contract.
