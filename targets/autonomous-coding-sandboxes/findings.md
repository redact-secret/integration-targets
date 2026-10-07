# Autonomous coding sandbox findings

Scope: bounded category illustrated by the OpenHands Software Agent SDK, commit `69e26889401fe69157fff536e6a69049e6644cb3`, inspected 2026-10-07. This is one implementation sample, not a claim about every sandbox or deployed OpenHands Cloud version. No runtime executed.

<a id="sandbox-001"></a>

## SANDBOX-001 — Terminal execution combines lazy secrets and output masking

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

The registry resolves secret names referenced in a command. The terminal tool exports them into its session and masks the returned observation using the registry. The export is intentionally session-persistent, so name-based selection is not proof of single-command lifetime.

### Evidence

- [Registry selection and masking](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-sdk/openhands/sdk/conversation/secret_registry.py#L204-L310).
- [Session exports and observation masking](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-tools/openhands/tools/terminal/impl.py#L320-L384).
- [Execution ordering](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-tools/openhands/tools/terminal/impl.py#L434-L470).

### Sensitive-data boundary

Secret source → terminal session → execution → masked text observation.

### Potential impact (inference)

Existing masking supports the observation-boundary concept. A release design must separately constrain who can use values after export.

### Notes / uncertainty

This is the terminal path, not a universal claim about every tool. No proof of detection of unknown PII, visual redaction or host/process isolation. No adversarial bypass tested.

### Related patterns

[agent-evidence-boundary](../../patterns/agent-evidence-boundary.md); [runtime-secret-release](../../patterns/runtime-secret-release.md)

<a id="sandbox-002"></a>

## SANDBOX-002 — Tool observations become retained events

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

The agent wraps tool results in `ObservationEvent`. The local conversation default callback appends events to state. EventLog serializes events to files, providing a concrete artifact surface alongside live observations.

### Evidence

- [Tool result to event](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-sdk/openhands/sdk/agent/agent.py#L1487-L1530).
- [Default callback](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-sdk/openhands/sdk/conversation/impl/local_conversation.py#L424-L431).
- [Event serialization](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-sdk/openhands/sdk/conversation/event_store.py#L188-L238).

### Sensitive-data boundary

Tool execution → observation event → conversation state/event file.

### Potential impact (inference)

Repeated tool execution can retain multiple evidence records. Filtering only later model requests cannot remove prior storage writes.

### Notes / uncertainty

Retry amplification is a structural inference; no frequency or real-data exposure was measured. Tool-owned files, full-output spill files, telemetry, browser images and deployment retention remain separately unqualified.

### Related patterns

[persisted-debug-evidence](../../patterns/persisted-debug-evidence.md); [agent-evidence-boundary](../../patterns/agent-evidence-boundary.md)

<a id="sandbox-003"></a>

## SANDBOX-003 — An observation callback is not automatically an enforcing filter

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

The built-in PostToolUse manager runs hooks with `stop_on_block=False`. Its observation branch invokes post-tool handlers and forwards the event; it does not replace the observation with a sanitized response from that hook.

### Evidence

- [Post-tool manager](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-sdk/openhands/sdk/hooks/manager.py#L104-L123).
- [Observation callback](https://github.com/OpenHands/software-agent-sdk/blob/69e26889401fe69157fff536e6a69049e6644cb3/openhands-sdk/openhands/sdk/hooks/conversation_hooks.py#L106-L125).

### Sensitive-data boundary

Observation → audit/extension hook → original callback.

### Potential impact (inference)

A host-controlled tool wrapper or earlier transformation point is needed for enforceable filtering. Merely subscribing to evidence does not establish interception before model exposure or storage.

### Notes / uncertainty

This qualifies the inspected built-in hook, not every SDK extension mechanism. Tool wrappers still need review for earlier tracing and artifact writes.

### Related patterns

[agent-evidence-boundary](../../patterns/agent-evidence-boundary.md)
