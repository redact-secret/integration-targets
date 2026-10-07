# Autonomous coding sandboxes: product fit

Status: hypothesis for every target-specific application below. This is research, not implemented integration or qualified support.

## Finding-to-capability mapping

[SANDBOX-001](findings.md#sandbox-001) credits native terminal secret masking. [SANDBOX-002](findings.md#sandbox-002) and [SANDBOX-003](findings.md#sandbox-003) support a vendor-neutral [evidence contract](../../capabilities/irreversible-sanitization.md) around tool execution and event creation.

Use a small envelope with channel-specific text/structure handling, rather than a universal opaque Observation object that implicitly covers images. A host-controlled tool implementation/wrapper can be an enforcement candidate; the inspected PostToolUse hook alone cannot replace the observation.

[Composed transformation](../../capabilities/composed-transformation.md) is optional when independent detectors produce overlapping findings. Core remains sufficient for a single supported detector/policy path. No reversible retention is needed merely to preserve debugging usefulness.

## Minimum host hooks

Inventory terminal, file read, MCP, browser text/image, error, trace and artifact paths. Sanitize before any intended model or storage boundary, including tool-owned spill files and tracing. A wrapper after a tool returns may be too late for tool-internal persistence. Carry retry identity without storing raw previews; reapply policy to each newly collected observation.

## Residual risk and non-goals

The SDK sample does not qualify every autonomous sandbox. Hosts own process isolation, permissions, networking, browser sessions and event retention. Text coverage does not include rendered PII. Repeated observations can multiply artifacts, but this study measured no leak frequency or cross-vendor prevalence.

## Qualification

Use the [qualification gates](../../research/open-questions/qualification-gates.md) before any support claim. Reversible release, runtime injection and visual handling need additional security review under [SECURITY.md](../../SECURITY.md). No such implementation is approved by this case study.
