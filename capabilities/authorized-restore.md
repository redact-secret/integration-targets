# Authorized reconstruction into a trusted destination

Status: hypothesis for the generic evidence-host contract. Proposed owners: vault for authority and lifecycle; restore for discovery, planning, preflight interaction and reconstruction; host for delivery. The separate restore component remains planned in this research, with no implementation claim.

## Problem and inputs

[Reversible capture](reversible-capture.md) is useful only if recovery reaches an approved destination. Input consists of tokenized fields, their canonical paths, an explicit allowed capture set, authenticated context and sink/purpose information established by the host.

A concrete destination is an authenticated developer's selected-field diagnostic viewer. A runtime launcher is a distinct proposed destination and is governed by [scoped runtime release](scoped-runtime-release.md), not implicitly included by a viewer grant.

## Proposed flow

```text
validate/discover occurrences → build whole-request plan
→ vault current-authority preflight → atomic consume/resolve
→ complete reconstruction → host-controlled destination
```

The authority checks every occurrence against capture/source, sink/path, expiry, revocation, use budget and, for the chosen server profile, principal/tenant/purpose. Restore must not accept model claims as an alternative.

## Outputs and failure semantics

Return the complete reconstructed field set or no application-visible restored plaintext. Hold all output until every check and reconstruction succeeds. Mixed valid/invalid occurrences deny the whole request. Do not stream restored prefixes.

A successful preflight is not a permanent grant. The authority must revalidate at consume or provide a transaction with equivalent current-policy semantics. Concurrency, repeated occurrences, grant expiry, cancellation and consumed-but-undelivered values must have explicit semantics before implementation.

Application-visible atomicity is not a claim of atomic network delivery, process spawn, database commit, memory erasure or refunded use budgets. A host retry must not automatically restore again or enlarge grants after ambiguous delivery.

## Ownership and non-goals

Restore owns no identity system, policy database, mapping store, key material or vendor knowledge. The vault owns those authority/mapping concerns in its supported profiles. The host chooses the destination, authenticates the recipient and prevents reconstructed output from returning to model/tool logs.

This does not require HTTP, JSON or a process boundary. Native in-process composition may use bulk plans and one-pass output construction. These are design requirements, not measured performance claims.

## Qualification and review

Before implementation, obtain additional release-path review required by [SECURITY.md](../SECURITY.md). Synthetic checks must include one denied occurrence among allowed ones, malformed markers, copied tokens across captures, wrong fields, cross-tenant requests, revoke-between-preflight-and-consume, budget contention, oversized output, cancellation and delivery failure. The expected application-visible result on denial is no restored plaintext.

Current vault-internal restore behavior and a future separate restore package are different implementation surfaces. This research does not claim the latter has shipped.
