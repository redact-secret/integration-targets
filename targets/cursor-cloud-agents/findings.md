# Cursor Cloud Agents findings

Scope: Cursor-hosted Cloud Agents, official unversioned documentation accessed 2026-10-07. These are documentation observations, not independently tested controls. Self-hosted deployments are not covered.

<a id="cursor-001"></a>

## CURSOR-001 — Secret classes have different visibility

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Environment Variables are agent-visible. Runtime Secrets remain environment variables but are masked in tool results, transcripts and commits; a human Terminal user can still view them. Build Secrets are confined to Docker builds.

### Evidence

[Secrets & Network, Secret protection](https://cursor.com/docs/cloud-agent/security-network#secret-protection).

### Sensitive-data boundary

Configured secret → build or runtime → selected presentation surfaces.

### Potential impact (inference)

Runtime access and model display are separate policy decisions. Existing vendor masking must be credited before proposing extra filtering.

### Notes / uncertainty

Transformed values, newly returned PII and visual content are not qualified by this observation.

### Related patterns

[runtime-secret-release](../../patterns/runtime-secret-release.md); [agent-evidence-boundary](../../patterns/agent-evidence-boundary.md)

<a id="cursor-002"></a>

## CURSOR-002 — Conversation and snapshot retention are separate

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Conversation history defaults to indefinite retention. Snapshots expire after 90 days of inactivity, extended on start/resume. Delete Agent removes transcript/artifacts, not snapshots. The setup FAQ says `.env.local` included when creating a snapshot is saved.

### Evidence

- [Data retention](https://cursor.com/docs/cloud-agent/security-network#data-retention).
- [Cloud Agents FAQ](https://cursor.com/docs/cloud-agent).

### Sensitive-data boundary

Workspace → snapshot; tool/demo evidence → conversation storage.

### Potential impact (inference)

Ending execution does not establish deletion of all evidence or configuration copies.

### Notes / uncertainty

Retention is documented, not deletion-tested. Enterprise policy can change conversation retention. These facts do not establish the contents of any particular snapshot.

### Related patterns

[persisted-debug-evidence](../../patterns/persisted-debug-evidence.md); [secret-materialization](../../patterns/secret-materialization.md)

<a id="cursor-003"></a>

## CURSOR-003 — Cloud hook coverage has explicit limits

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Cloud hooks start after a writable environment is available, not during early read-only turns. `postToolUse` supports `updated_mcp_tool_output` for MCP results only. Dedicated before/after MCP hooks are listed as unavailable in cloud agents.

### Evidence

[Hooks, Cloud agent support and postToolUse](https://cursor.com/docs/hooks#cloud-agent-support).

### Sensitive-data boundary

Tool result → host hook → model-facing MCP result.

### Potential impact (inference)

The documented replacement is a candidate interception point for MCP evidence, not a universal shell-output or pre-storage sanitizer.

### Notes / uncertainty

Hook availability does not prove fail-closed behavior, pre-persistence ordering or complete media coverage. Those need host qualification.

### Related patterns

[agent-evidence-boundary](../../patterns/agent-evidence-boundary.md)
