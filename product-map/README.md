# Ecosystem products and ownership

Ownership is an architectural boundary, not proof that a capability is implemented or qualified. [ARCHITECTURE.md](../ARCHITECTURE.md) governs the core/vault/restore boundaries; the anonymizer addition records the supplied design discussion as a proposal. The adapter, CLI and gateway pages record upstream documentation inspected on 2026-10-08.

- [Core](core.md): detection, policy, irreversible redaction and safe metadata.
- [Anonymizer](anonymizer.md): optional cross-detector normalization, arbitration and forward transformation.
- [Vault](vault.md): reversible capture, retained mappings and release authority/lifecycle.
- [Restore](restore.md): discovery, planning, authority interaction and atomic reconstruction.
- [Adapters](adapters.md): host-specific integration for logging, tracing, AI context and MCP; core retains detection and policy decisions.
- [CLI](cli.md): command-line file/stdin checks and irreversible redaction over core.
- [Gateway](gateway.md): experimental, unpublished HTTP gateway for bounded LLM request inspection and forwarding.

Adapters, CLI and Gateway implement host-facing integration roles. Their documented scope does not establish support for the external systems studied in this repository.

The host owns protocol parsing, identity, permissions, runtime isolation, process/workspace lifecycle, injection, pre-model/pre-storage interception and artifact cleanup. Credential providers retain issuance, storage and rotation. No package sequence is mandatory.

```text
simple evidence: host → core → host-approved sanitized sink
composed evidence: host/detectors → anonymizer → host-approved sink
optional recovery: vault authority ↔ restore → trusted host destination
```

The first prototype candidate is [irreversible evidence sanitization](../capabilities/irreversible-sanitization.md). [Runtime release](../capabilities/scoped-runtime-release.md) remains a security-sensitive hypothesis. Package separation does not require IPC, HTTP or serialization.
