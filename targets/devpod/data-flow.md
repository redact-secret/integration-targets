# DevPod: observed data flow

Observation date: 2026-10-07. Scope and citations are in [findings](findings.md).

### DEVPOD-001

```text
workspace helper → tunnel lookup → credential response
```

See [DEVPOD-001](findings.md#devpod-001) for conditions and evidence.

### DEVPOD-002

```text
local option → provider-command environment
```

See [DEVPOD-002](findings.md#devpod-002) for conditions and evidence.

### DEVPOD-003

```text
context cancellation → credential-server close
```

See [DEVPOD-003](findings.md#devpod-003) for conditions and evidence.

These paths establish movement, not that a particular run contained a secret or that every downstream representation is sanitized. Product proposals are in [product-fit](product-fit.md).
