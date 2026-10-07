# Composed finding transformation

Status: hypothesis. Proposed owner: anonymizer for cross-detector orchestration. This reflects the supplied design conversation and current planning boundaries; no implementation or public support is asserted.

## Problem

[Agent evidence](../patterns/agent-evidence-boundary.md) may combine credentials, structured personal data and contextual entities. More than one detector can return overlapping findings. This motivates an optional composition layer, not a requirement that every evidence workflow use it.

## Inputs and outputs

Input: immutable text, findings from independent engines or a trusted caller, declared offset units, finding provenance and explicit replacement policy. Output: a deterministic accepted-span plan, one completed transformed text and a manifest with safe counts/categories and policy provenance.

The proposed stages are normalization, overlap arbitration, replacement planning and one-pass output construction. This is not an API freeze or a benchmark claim. Cross-language offsets must be converted explicitly; byte, UTF-16 and code-point ranges cannot be mixed.

## Invariants and ownership

Reject out-of-range, invalid Unicode-boundary or inconsistent spans before output. Specify deterministic overlap precedence and ensure discarded findings cannot leave a protected subspan unintentionally visible. A statistical entity score does not automatically outrank a deterministic credential finding.

Core retains its complete scan/policy/redact path and its internal overlap behavior. Fastner or other detectors own their recognition logic. Anonymizer may compose findings; it must not own detector implementations, HTTP/MCP parsing, stream framing, artifact persistence or runtime processes.

Irreversible output is the default. If an accepted span genuinely needs later recovery, the vault owns token issuance, retained values, grants and lifecycle. Anonymizer inserts an authorized token representation and never turns its manifest into release authority. Restore owns the reverse reconstruction algorithm.

## Non-goals, review and qualification

No claim of general anonymization, re-identification resistance, all-PII coverage, image redaction or complete detection. A manifest must not disclose original text or stable credential fingerprints. Trusted findings and policy do not remove the need to validate their spans.

Before prototyping: fix the common finding contract, offset conversion, overlap rules and manifest schema. Test deterministic replay, adversarial Unicode, nested/overlapping findings, invalid ranges and output-limit failures using synthetic data. Any reversible composition needs the release-path review in [SECURITY.md](../SECURITY.md).

The standalone core path is the first evidence-contract candidate; composition becomes worthwhile only when multiple engines or richer replacement requirements are demonstrated. See [anonymizer ownership](../product-map/anonymizer.md).
