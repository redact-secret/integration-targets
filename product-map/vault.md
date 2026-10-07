# Vault ownership

Vault owns explicit reversible capture, token identity, retained mappings, capture/source binding, sink/path grants, expiry, revocation, use budgets and authority policy in the selected profile. Persistence belongs only to its qualified persistence profiles.

The [pinned README](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/README.md), [single-user reference](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/docs/reference/vault.md) and [server reference](https://github.com/redact-secret/redact-secret-vault/blob/9e03618626e86fc3c790bbf4572a12f2adb8f8f6/docs/reference/vault-server.md), inspected 2026-10-07, distinguish existing capture/restore behavior from profile-specific authorization. A single-user in-memory vault does not establish multi-tenant authorization; persistence availability is not a blanket qualification claim.

[Reversible evidence capture](../capabilities/reversible-capture.md) is optional and requires a concrete recovery destination. [Runtime release](../capabilities/scoped-runtime-release.md) is a hypothesis that reuses authority concepts but requires trusted host identity and delivery semantics. No process-isolation or generic secret-manager responsibility is added.

Vault authority must decide current permission; restore must not infer it. Revocation denies future authorized use, not access to plaintext already released. Host authentication, credential issuance, process lifecycle and remote-workspace security remain external.
