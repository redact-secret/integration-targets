# Autonomous coding sandboxes: observed data flow

Observation date: 2026-10-07. Scope and citations are in [findings](findings.md).

### SANDBOX-001

```text
registered secret → terminal session → masked observation
```

See [SANDBOX-001](findings.md#sandbox-001) for conditions and evidence.

### SANDBOX-002

```text
tool result → observation event → persisted event
```

See [SANDBOX-002](findings.md#sandbox-002) for conditions and evidence.

### SANDBOX-003

```text
observation → non-blocking post-tool hook → callback
```

See [SANDBOX-003](findings.md#sandbox-003) for conditions and evidence.

These paths establish movement, not that a particular run contained a secret or that every downstream representation is sanitized. Product proposals are in [product-fit](product-fit.md).
