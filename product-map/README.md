# Product ownership

Ownership is an architectural boundary, not proof that a capability is implemented or qualified. [ARCHITECTURE.md](../ARCHITECTURE.md) governs the existing ecosystem; the anonymizer addition below records the supplied design discussion as a proposal.

- [Core](core.md): detection, policy, irreversible redaction and safe metadata.
- [Anonymizer](anonymizer.md): optional cross-detector normalization, arbitration and forward transformation.
- [Vault](vault.md): reversible capture, retained mappings and release authority/lifecycle.
- [Restore](restore.md): discovery, planning, authority interaction and atomic reconstruction.

The host owns protocol parsing, identity, permissions, runtime isolation, process/workspace lifecycle, injection, pre-model/pre-storage interception and artifact cleanup. Credential providers retain issuance, storage and rotation. No package sequence is mandatory.

```text
simple evidence: host → core → host-approved sanitized sink
composed evidence: host/detectors → anonymizer → host-approved sink
optional recovery: vault authority ↔ restore → trusted host destination
```

The first prototype candidate is [irreversible evidence sanitization](../capabilities/irreversible-sanitization.md). [Runtime release](../capabilities/scoped-runtime-release.md) remains a security-sensitive hypothesis. Package separation does not require IPC, HTTP or serialization.
