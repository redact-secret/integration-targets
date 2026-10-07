---
name: design-capability
description: Define a vendor-neutral candidate capability or integration contract from supported patterns and map core, vault, restore, and host responsibilities. Use for product hypotheses, not implementation or release authorization.
---

# Design a capability

Read `ARCHITECTURE.md`, `CONVENTIONS.md`, `SECURITY.md`, and the supporting
patterns and findings. Confirm the contract addresses an evidenced boundary
and would remain useful if the named vendor disappeared.

First decide whether irreversible sanitization meets the need. Reversible
capture requires a concrete recovery need and trusted destination; debugging
convenience or token possession alone is not authority.

Write or update `capabilities/<name>.md` with explicit status (`implemented`,
`planned`, `experimental`, `hypothesis`, or `rejected`), supporting patterns,
problem, inputs, outputs, trusted context, invariants, proposed owner, non-goals,
qualification needed, and unresolved decisions. A new proposal starts as a
hypothesis unless evidence supports another status. Verify implementation in
the owning product before claiming it exists.

Specify interception before model exposure and/or persistence, text versus
structured inputs, streaming or buffering needs, error behavior, and retained
debugging utility where relevant. A proposed text contract does not protect
screenshots or binary media. Describe limits explicitly.

For release proposals distinguish model-supplied fields from trusted host
assertions: source/capture, project/workspace, process/session, destination/path,
purpose, expiry, revocation, use budget, and principal/tenant where applicable.
Record which fields matter and which host can attest to them. Keep mapping and
authorization in vault, preflight interaction and atomic reconstruction in
restore, and process injection/lifecycle in the host. Do not imply a mandatory
core-to-vault-to-restore pipeline or a general credential store.

Record justified ownership decisions in `product-map/`, linking the capability
and evidence. Keep unresolved ownership explicit instead of assigning the
nearest package. Include host prerequisites, failure and partial-release risks,
residual exposure, and a bounded synthetic validation plan.

Apply the additional-review triggers in `SECURITY.md`, including new release
paths, runtime injection, persistence, remote authority, visual handling, and
new security claims. A written draft may be completed with review needs stated;
it must not be presented as an approved or qualified security contract. Do not
implement adapters, mutate owning products, or publish external messages unless
the user authorizes that work.
