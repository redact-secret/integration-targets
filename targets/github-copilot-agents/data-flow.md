# GitHub Copilot cloud agent: observed data flow

Observation date: 2026-10-07. Scope and citations are in [findings](findings.md).

### COPILOT-001

```text
Agents secrets → runtime environment or MCP-only scope
```

See [COPILOT-001](findings.md#copilot-001) for conditions and evidence.

### COPILOT-002

```text
configured credentials → MCP authentication; MCP results → agent
```

See [COPILOT-002](findings.md#copilot-002) for conditions and evidence.

These paths establish movement, not that a particular run contained a secret or that every downstream representation is sanitized. Product proposals are in [product-fit](product-fit.md).
