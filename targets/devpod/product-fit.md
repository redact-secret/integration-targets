# DevPod: product fit

Status: hypothesis for every target-specific application below. This is research, not implemented integration or qualified support.

## Finding-to-capability mapping

[DEVPOD-001](findings.md#devpod-001) shows an existing on-demand credential path. Preserve that distinction: adding another persistent credential store is not justified by this study. [DEVPOD-002](findings.md#devpod-002) separates provisioning credentials from workspace consumers.

[Scoped runtime release](../../capabilities/scoped-runtime-release.md) is a hypothesis only where a trusted host can narrow a real credential request to a designated consumer. Git/Docker authentication is a concrete runtime need; the model does not need the response value. A common authority envelope may fit both DevPod and Baton, but the delivery mechanisms differ.

[DEVPOD-003](findings.md#devpod-003) requires distinguishing revocation of future lookups from cleanup of past responses. [Irreversible sanitization](../../capabilities/irreversible-sanitization.md) could cover host-controlled diagnostics; no universal DevPod-to-model evidence hook is claimed.

## Minimum host hooks

Required hooks: trusted workspace/connection identity, authentication at the credential broker, explicit consumer and destination binding, current-policy checks for each release, cancellation and downstream output control. A forwarded socket or credential-helper protocol alone does not supply all of them. Adding an agent later requires reevaluating access, not assuming the original human-only trust remains.

## Residual risk and non-goals

DevPod/providers retain SSH, VM/container isolation, Git/Docker/AWS issuance and workspace lifecycle. Plaintext consumers may cache values, and signing delegation can broaden effective authority without copying a key. No cleanup or malicious-workspace resistance is qualified.

## Qualification

Use the [qualification gates](../../research/open-questions/qualification-gates.md) before any support claim. Reversible release, runtime injection and visual handling need additional security review under [SECURITY.md](../../SECURITY.md). No such implementation is approved by this case study.
