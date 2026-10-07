# GitHub Copilot cloud agent findings

Scope: GitHub.com cloud agent documentation accessed 2026-10-07, not IDE agent mode, CLI or arbitrary GitHub Actions jobs. Unversioned documentation can change; controls were not executed.

<a id="copilot-001"></a>

## COPILOT-001 — Agents secrets are distinct from other platform secrets

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Organization/repository Agents secrets feed the agent environment. `COPILOT_MCP_` values are restricted to MCP servers. Session logs mask secret values. Ordinary Actions, Codespaces and Dependabot secrets are unavailable; the legacy `copilot` environment secrets were migrated.

### Evidence

[Configure secrets and variables, scope and usage](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/configure-secrets-and-variables).

### Sensitive-data boundary

Platform-approved repository scope → runtime environment or MCP-only destination.

### Potential impact (inference)

Repository eligibility is not an attestation of a particular process, field or debugging purpose. Additional release authority would need trusted host context.

### Notes / uncertainty

This corrects the issue’s generic repository-secret wording. Masked session logs do not independently qualify all MCP payloads, derived credentials or personal data. No claim of a demonstrated leak.

### Related patterns

[runtime-secret-release](../../patterns/runtime-secret-release.md)

<a id="copilot-002"></a>

## COPILOT-002 — MCP credentials and returned evidence use distinct directions

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Local MCP configuration can receive secret substitutions in `env`; remote configuration uses headers. An allowlist selects tools that Copilot can call autonomously. Session logs expose MCP startup diagnostics. The built-in GitHub MCP server defaults to read-only access to the current repository.

### Evidence

[Configure MCP servers, configuration and validation](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/configure-mcp-servers).

### Sensitive-data boundary

Host credential → MCP server authentication; server result → agent workflow.

### Potential impact (inference)

A server can authenticate correctly and still return data needing evidence policy. Filter structured results and errors at a controlled server boundary before return.

### Notes / uncertainty

These docs do not establish a general customer-controlled interception point for every managed tool result or pre-storage write. A controlled MCP server is a narrower candidate. No assumption of access to all organization secrets.

### Related patterns

[agent-evidence-boundary](../../patterns/agent-evidence-boundary.md)
