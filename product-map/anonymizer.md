# Anonymizer ownership

Status: hypothesis for the integration role. The supplied design conversation identifies anonymizer as a planned forward-transformation orchestrator. No implementation, stable API, general anonymization guarantee or public support is asserted.

[Composed transformation](../capabilities/composed-transformation.md) assigns it normalization of independent findings, deterministic overlap arbitration, replacement planning, one-pass output construction and a plaintext-free transformation manifest. The requirement becomes useful when one evidence field needs multiple detectors or replacement strategies.

Core keeps its complete standalone redaction path and internal detector policy. Optional NER providers, such as fastner, remain independent recognizers. Anonymizer does not implement their detection, nor parse HTTP/MCP, frame streams, persist artifacts, issue authority or run processes.

Vault owns capture, token identity, original values, grants and lifecycle. Restore owns reverse reconstruction. Anonymizer may coordinate a separately reviewed capture contract; it never retains a mapping or authorizes reveal. Native composition need not cross a serialization/process boundary.

This page deliberately includes no private repository URL or copied private design document. Before public publication, review the proposed product naming and unreleased scope as required by [SECURITY.md](../SECURITY.md).
