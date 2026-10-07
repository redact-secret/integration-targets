---
name: boundary-review
description: Review research documents or proposed contracts for Redact Secret product ownership drift, evidence gaps, and unsupported integration or security claims. Read-only unless fixes are requested.
---

# Review product boundaries

Read `ARCHITECTURE.md`, `CONVENTIONS.md`, and `SECURITY.md`. Establish the requested
scope: diff, target, pattern, capability, or product map. Include new files when
reviewing working-tree changes, without absorbing unrelated staged user work.

Trace important conclusions backward from ownership to capability, pattern,
finding, and source. Flag inference presented as observed behavior, proposals
presented as implementation, issue closure presented as vendor support, or a
vendor-specific assumption presented as a generic requirement.

Check responsibility precisely:

- Core: detection, policy, irreversible redaction, safe metadata; no mappings,
  persistence, release authorization, or runtime ownership.
- Vault: capture, mappings, authorization and lifecycle; no implicit expansion
  into general credential storage or platform security.
- Restore: token discovery, planning, authority interaction and all-or-nothing
  reconstruction; no policy, identity, persistence, key management, or vendor
  awareness.
- Host: authentication, sandboxing, permissions, process/workspace lifecycle,
  trustworthy context and interception hooks.

Check that reversible handling has a justified destination and current authority,
not merely a token or model assertion. Identify preflight/consume assumptions
and partial-output risks without asserting an unimplemented guarantee. Check
visual coverage separately from textual filtering and separate sanitization
before display from sanitization before persistence.

Report concrete findings by severity, file/location, evidence, consequence,
and smallest useful correction. Distinguish a demonstrated conflict from an
open question and identify required security review. If no findings exist,
state the reviewed scope and unassessed claims; do not certify runtime security.
Do not edit files or send review comments unless requested.
