# Restore ownership

Restore owns token discovery, occurrence validation, whole-request planning, interaction with authority preflight/consume and all-or-nothing application-visible reconstruction. This is the planned separate component boundary, not a claim that it has shipped.

[Authorized restore](../capabilities/authorized-restore.md) records the proposed generic contract. Existing vault-internal reconstruction must not be confused with implementation of a standalone restore package.

Vault owns authorization, mappings, expiry/revocation and current policy. Hosts establish identity and the destination and deliver completed output. Restore owns no storage, tenant/principal identity, key management, detector logic, provider credentials or vendor-specific runtime behavior.

A failed whole-request check returns no restored plaintext. The eventual authority contract must define concurrency and consumption semantics; application-visible atomicity alone does not promise atomic process launch, transport delivery or memory erasure.
