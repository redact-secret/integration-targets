# Qualification gates after source research

Status: unresolved product/security qualification, reviewed 2026-10-07. These are scoped gaps with acceptance evidence, not findings of an exploited vulnerability. Research conclusions remain useful without pretending these gates are passed.

## Enforcing evidence hooks

Known: the [target findings](../../targets/README.md) identify serializers, tool paths and documented hooks. Unknown: end-to-end ordering across each host's model input, tracing, caching, error handling, raw spill files and artifact writers.

Evidence required: a host-controlled synthetic trace of every intended sink showing that transformation precedes its first write. Include failure, retry, cancellation and unsupported payloads. An audit-only callback or hook that starts after some turns cannot qualify universal coverage. Responsible layer: host integration, with core/anonymizer conformance in their own repositories.

<a id="visual-evidence"></a>
## Visual and binary evidence

Known: [Baton proof](../../targets/baton/findings.md#baton-004) copies images; text redaction does not transform those pixels. The category also includes browser observations and media.

Decision: no image/video protection claim in the text contract. The host should withhold unsupported media from any sink claimed to be protected, or use a separately reviewed visual process. OCR alone cannot establish complete pixel protection.

Evidence required: disposable synthetic screens, metadata inspection, all frames where applicable, review of residual visual identifiers and verification before upload/storage. No screenshots or media were collected in this research. Additional security review is required before introducing media handling.

## Runtime authority and delivery

Known: documented vault capture/sink/path concepts and the source-backed runtime-use pattern. Unknown: a generic trustworthy host attestation and transaction spanning authorization, consumption, reconstruction and launch.

Evidence required: synthetic wrong-project/session/target/path denials, current-policy and revocation races, use-budget contention, launch failure, ambiguous delivery and cleanup behavior. Demonstrate a real model/consumer trust separation. Responsible layers: vault authority, restore reconstruction and host identity/lifecycle. Runtime release remains a hypothesis pending additional security review.

## Persistence and cleanup

Known: evidence stores and forwarding lifecycles differ across targets. Unknown: deployed retention/deletion effectiveness, tool-owned caches, snapshots and downstream consumers. This study selects no persistent vault profile.

Evidence required: inventory every storage owner, test configured retention with synthetic artifacts, verify permission and backup behavior, and cite an exact store/language/version qualification if mappings persist. Deletion does not prove erasure from managed memory or already exported copies. Responsible layer: host/storage provider; vault only for qualified mapping persistence.

## Detection, utility and composition

Known: core has bounded detection and policy primitives; native target controls already mask some secret values. Unknown: incremental benefit, diagnostic loss, unknown/derived secrets, optional PII profiles and multi-detector overlap policy for these evidence channels.

Evidence required: a synthetic corpus with both protected values and useful failure signals, explicit negatives and unsupported classes, byte/UTF-16/code-point conversion cases, safe manifests, and whole-record/stream failure cases. Declare actual thresholds/profile limits before tests; do not invent pass rates from source inspection. Responsible layer: owning detector/composition product plus host qualification.

## Public publication review

The changed/new research contains no raw shared-session transcript, copied private product documents, actual credentials or captured media. The current repository is private; its issue URLs are retained intentionally as internal work references. Review those references and the proposed anonymizer/restore scope before public publication, because task context and product plans may be unreleased. Private product-source URLs are omitted. This is a working-tree review, not a full-history audit. No public posting or repository visibility change is authorized by completion of these documents.
