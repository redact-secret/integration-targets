# Adapters ownership

Status: implemented for the integration surfaces documented upstream, with package-specific qualification limits. This source review did not run upstream tests or independently verify registry releases.

The [pinned README](https://github.com/redact-secret/redact-secret-adapters/blob/88f8340664ff7f30514073321ec410f1caa8f046/README.md), inspected 2026-10-08, describes adapters for pino, JavaScript/Python OpenTelemetry traces, Python logging, masking callbacks, AI context and MCP tool results/resource reads. OpenTelemetry Logs is a separate beta package; metrics and model output are not covered.

Adapters own host-specific extraction, integration hooks and delivery of core results. Core decides detection, policy and redaction. Logging/tracing adapters use fixed failure markers; AI-context and MCP adapters return outcomes with no value unless successful. These are documented integration behaviors, not a guarantee that every secret is detected.

Coverage depends on placement: bypassing handlers, processors or transports remain outside the adapter. Logging/tracing adapters do not scan object keys independently or rewrite them; AI-context and MCP adapters do scan keys. PII is opt-in. Hosts retain identity, permissions, lifecycle and destination control; vault retains mappings and release authority, and restore retains reconstruction.

Related research: [agent evidence boundary](../patterns/agent-evidence-boundary.md). Existing host adapters do not imply a Baton, Cursor or DevPod integration.
