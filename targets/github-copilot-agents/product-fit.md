# GitHub Copilot cloud agent: product fit

Status: hypothesis for every target-specific application below. This is research, not implemented integration or qualified support.

## Finding-to-capability mapping

[COPILOT-001](findings.md#copilot-001) establishes native secret scope and masking; retain those controls. [COPILOT-002](findings.md#copilot-002) supports a narrow [irreversible evidence sanitizer](../../capabilities/irreversible-sanitization.md) at a host-controlled MCP server's result/error boundary. A platform-wide sanitizer has not been established.

An organization/repository grant determines eligibility but does not itself bind a future release to a particular session, structural path and purpose. [Scoped runtime release](../../capabilities/scoped-runtime-release.md) therefore requires an additional trusted broker/launcher contract before it can be proposed as usable here.

No need for routine reversible capture is established. Keep build/test errors, status and sanitized field structure; retain originals only for a specific authenticated debugging destination with current authorization.

## Minimum host hooks

The controlled MCP service must enforce tool authorization and sanitize results/errors before returning or logging them. The host must authenticate repository and session provenance; model-supplied repository names or purpose strings are requests, not proof. A generic platform pre-persistence hook remains unconfirmed.

## Residual risk and non-goals

GitHub owns Agents secrets, repository permissions and runner lifecycle; MCP servers own their service authorization. Redaction does not stop a permitted tool from performing a harmful action. Session log masking is not a tested guarantee for every external result or generated file.

## Qualification

Use the [qualification gates](../../research/open-questions/qualification-gates.md) before any support claim. Reversible release, runtime injection and visual handling need additional security review under [SECURITY.md](../../SECURITY.md). No such implementation is approved by this case study.
