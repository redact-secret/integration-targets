# Reversible evidence capture

Status: hypothesis for the evidence-host workflow. Proposed owner: vault. Existing vault capture is documented separately; it does not establish support for these targets.

## Problem and justified destination

[Persisted evidence](../patterns/persisted-debug-evidence.md) normally needs only irreversible redaction. Retention is justified only when an authenticated developer must inspect one original diagnostic value in a trusted viewer to resolve a concrete ambiguity that sanitized evidence cannot resolve. The model is not that destination.

## Inputs and outputs

Inputs: selected eligible plaintext findings, trusted source/capture context, exact viewer sink/path grants, explicit expiry and use limits, and identity/purpose policy where the selected server profile requires them. Output: tokenized evidence and an opaque capture reference. Store no plaintext or release credentials alongside a proof artifact.

The [current capture reference](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/docs/reference/vault.md) supports explicit `release` sink/path grants, `maxUses`, capture IDs and selected PII retention. Multi-user authorization belongs to the [server profile](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/docs/reference/vault-server.md), not the single-user in-memory vault. Both were reviewed 2026-10-07; no runtime conformance test was performed here.

## Invariants and host responsibilities

- Prefer irreversible removal; capture only the subset whose later recovery is justified.
- Retained values and token identity belong to vault, not core, anonymizer or artifact metadata.
- Token possession and model-provided source or purpose never establish authority.
- The host separates tokenized evidence from the authenticated viewer and keeps mappings within the selected qualified lifecycle.
- If capture fails, return an input-free failure or deliberately irreversible result with no recovery promise. Do not leak the original as a fallback.
- A mapping expires/revokes independently of an artifact. A surviving token can become unrestorable; do not extend retention just because a proof file survives.

## Non-goals and qualification

No default mapping persistence, general credential storage, automatic human-reveal UI or protection from code sharing raw process memory. Persisting mappings or introducing a new viewer release path requires additional security review under [SECURITY.md](../SECURITY.md).

Qualify source substitution, wrong sink/path, cross-tenant requests, expiry, revocation, repeated occurrences, cancellation, and the absence of originals from artifact/error output using synthetic fixtures. Persistence must cite a specific store/language/version qualification; the [vault status](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/README.md) distinguishes beta memory support from alpha and partially qualified persistence. No persistence profile is selected here.

See [authorized restore](authorized-restore.md) for reconstruction; capture alone never authorizes release.
