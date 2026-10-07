# Baton findings

Scope: source inspection of `0.2.6`, commit `1cb8c960306433404c79ec4fc404b1fb2df25490`. No upstream software executed.

<a id="baton-001"></a>

## BATON-001 — Alternate checkouts receive local configuration

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

`copyLocalConfig` selects `.env*`, `*.local.json`, case-insensitive `secrets*`, two mobile-service configuration filenames, and referenced Dart define files. Selection is name-based, not a check that Git ignores the file. Attached and reused owned checkouts preserve existing destination files; newly created owned checkouts permit overwriting.

### Evidence

- [Selection and copying](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/checkouts.ts#L63-L164).
- [Attached/reused/new checkout call sites](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/checkouts.ts#L296-L339).
- [Release ownership and removal](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/checkouts.ts#L255-L292), [removal fallback](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/checkouts.ts#L350-L356).

### Sensitive-data boundary

Source checkout → additional filesystem copy → application checkout.

### Potential impact (inference)

A matching file containing sensitive values creates another plaintext location. An attached checkout can retain that copy after a session ends.

### Notes / uncertainty

File names do not prove sensitive contents. Owned checkout cleanup exists; release skips attached and in-place checkouts and defers deletion while still used. Crash recovery, backups and secure erasure were not tested. Do not describe all copies as abandoned or all checkouts as deleted.

### Related patterns

[secret-materialization](../../patterns/secret-materialization.md)

<a id="baton-002"></a>

## BATON-002 — Process logs have live and historical agent readers

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Process output reaches the session log buffer and log events. MCP `read_logs` renders returned log text and accepts live session or past-run identifiers. The persistent writer serializes log text to JSONL.

### Evidence

- [Process output](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/adapters/process.ts#L93-L129), [buffer/event emission](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/session-base.ts#L67-L86).
- [MCP log result](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/mcp/index.ts#L149-L163), [disk writer](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/log-store.ts#L86-L149).

### Sensitive-data boundary

Child stdout/stderr → session → MCP result and run-history storage.

### Potential impact (inference)

Application-provided sensitive text may reach both an agent and retained diagnostics. Filtering only the MCP response would leave the disk path outside that protection.

### Notes / uncertainty

No general content redaction is present in these inspected operations; this is not an exhaustive claim about every adapter or upstream application. Buffer and disk limits restrict volume, not sensitivity. Actual retention depends on pruning and host lifecycle.

### Related patterns

[agent-evidence-boundary](../../patterns/agent-evidence-boundary.md); [persisted-debug-evidence](../../patterns/persisted-debug-evidence.md)

<a id="baton-003"></a>

## BATON-003 — Network detail depends on capture source and request options

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

The detail model includes URI, headers, cookies, events and optional bodies. MCP omits bodies unless `includeBodies` is enabled; its documented cap is 256 KB. The `otel-node` branch returns metadata with empty headers/cookies and states that bodies and URL queries are not captured. Live detail and stored request summaries are separate paths.

### Evidence

- [Data types](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/core/types.ts#L78-L122).
- [MCP list and optional detail](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/mcp/index.ts#L202-L244).
- [Capture-source branch](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/daemon/network.ts#L92-L117).
- [OTel export field selection and URL cleaning](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/instrumentation/node.mjs#L13-L35).

### Sensitive-data boundary

Instrumented runtime → source-specific network representation → MCP text.

### Potential impact (inference)

On detail-capable paths, credential-bearing fields and returned personal data warrant separate policies. Even summary URI/error fields require inspection before reuse.

### Notes / uncertainty

The type alone is not evidence that every adapter captures every field. Body opt-in and the OTel limitation are material counterexamples to the issue’s broad wording. No real traffic was collected.

### Related patterns

[agent-evidence-boundary](../../patterns/agent-evidence-boundary.md)

<a id="baton-004"></a>

## BATON-004 — Proof bundles persist multiple evidence formats

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

`writeProofBundle` writes per-cell logs and network snapshots as JSON, creates network rollups, and copies available screenshots into per-cell and images directories. The network artifact type is `NetworkRequestSnapshot[]`, not the full body-bearing detail type.

### Evidence

- [Bundle writes and screenshot copies](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/daemon/proof.ts#L507-L549).
- [Collection of per-cell artifacts](https://github.com/kanumuri9593/Baton/blob/1cb8c960306433404c79ec4fc404b1fb2df25490/src/daemon/proof.ts#L764-L807).

### Sensitive-data boundary

Runtime evidence → proof directory → later review or export.

### Potential impact (inference)

Proof introduces storage copies independent of model display. Text-only sanitization cannot establish protection for image pixels.

### Notes / uncertainty

No screenshot was collected. No claim that proof always contains HTTP bodies, that every image is sensitive, or that artifact deletion erases prior copies. Visual-policy qualification remains open.

### Related patterns

[persisted-debug-evidence](../../patterns/persisted-debug-evidence.md)
