# Agent runtime boundaries: comparison and issue outcomes

Research reviewed: 2026-10-07. Scope: open epic #1 and cases #2–#6, refreshed from GitHub with their current bodies and comments. This is a source/documentation research result, not a runtime security qualification. All six issues remain open; this work does not change their remote state.

## Decision

Prototype the [irreversible runtime-evidence contract](../../capabilities/irreversible-sanitization.md) in a bounded synthetic host before choosing a vendor. It addresses independently observed [agent evidence](../../patterns/agent-evidence-boundary.md) and [persistence](../../patterns/persisted-debug-evidence.md) boundaries.

Keep [scoped runtime release](../../capabilities/scoped-runtime-release.md) as a hypothesis. Existing secret delivery/masking must be understood before adding vault semantics. Recovery is exceptional and requires a real approved destination. Optional [anonymizer composition](../../capabilities/composed-transformation.md) serves multiple finding sources, not every simple redaction path.

## Evidence scope and differences

### Baton

Source: [pinned findings](../../targets/baton/findings.md). Source configuration, process output and source-specific network observations have different readers and lifetimes. Local functions provide inspectable interception candidates; none is a qualified plugin contract. History/proof create separate writes. Owned versus attached checkout cleanup must remain distinct.

### Cursor Cloud Agents

Source: [official-documentation findings](../../targets/cursor-cloud-agents/findings.md). Native secret classes, masking and cloud retention make runtime/model/storage policies visibly distinct. A documented MCP output replacement is narrower than universal evidence enforcement. No deployment or tenant was tested.

### GitHub Copilot cloud agent

Source: [official-documentation findings](../../targets/github-copilot-agents/findings.md). Dedicated Agents secret scopes and MCP configuration are explicit. A controlled MCP service is a plausible narrow filtering point; a platform-wide pre-model/pre-storage hook is unconfirmed. Native session log masking must not be omitted from the comparison.

### DevPod

Source: [pinned findings](../../targets/devpod/findings.md). Provider execution and workspace credential helpers are different trust paths. Helper responses and signing delegation are not equivalent to copying a source file. Stopping a forwarding server does not prove that a consuming process discarded prior values. It contributes an independent remote-development comparison, not proof of agent-specific behavior.

### Autonomous sandbox category

Source: [pinned SDK sample](../../targets/autonomous-coding-sandboxes/findings.md). Terminal observations and serialized events make the observation/persistence path inspectable. Existing output masking is a control to preserve. Built-in post-tool notification is not a replacement filter. One SDK sample plus independent case comparisons supports a generic concept, not market-wide prevalence or all deployment versions.

<a id="baton-comparison"></a>
## Baton comparison required by #2

- Against Cursor: compare local alternate-checkout copying with snapshot retention and cloud secret classes. Both support separate storage-lifetime analysis; they do not establish identical release mechanisms.
- Against Copilot: compare MCP-readable local runtime evidence with platform-approved MCP credentials and returned data. The common requirement is downstream result policy; platform authorization stays with the host.
- Against DevPod: compare file materialization with helper-mediated access. The useful abstraction is constrained runtime use, not a claim that both copy `.env` files.
- Against the SDK sample: compare log/network serialization with tool observations and event files. In both, transformation must precede the first protected consumer, not merely a later display callback.

This satisfies the at-least-two-other-systems comparison with independent evidence, while preserving differences and existing controls.

## Issue-by-issue outcome

### #2: Baton

The [case study](../../targets/baton/README.md) covers configuration copying, live/history logs, conditional network detail and persisted proof. The [evidence contract](../../capabilities/irreversible-sanitization.md) defines the sink model, diagnostic utility, structured/text handling and streaming constraints. [Runtime release](../../capabilities/scoped-runtime-release.md) maps trusted context to current documented vault concepts. [Capture](../../capabilities/reversible-capture.md) distinguishes recovery need from ordinary sanitization. [Visual gates](../open-questions/qualification-gates.md#visual-evidence), minimum hooks in [product fit](../../targets/baton/product-fit.md), and the comparison above cover the remaining research deliverables.

### #3: Cursor

The [case study](../../targets/cursor-cloud-agents/README.md) separates runtime use, model evidence, native masking and retention. Its conclusion is a qualified opportunity for controlled MCP evidence, not proof of a universal integration hook. The [product fit](../../targets/cursor-cloud-agents/product-fit.md) answers where irreversible treatment suffices, what would justify reveal, and why image/snapshot policies remain separate. Runtime-only confidentiality requires a host boundary; environment delivery alone is insufficient.

### #4: Copilot

The [case study](../../targets/github-copilot-agents/README.md) distinguishes Agents secrets, MCP credentials and returned evidence. Repository eligibility cannot substitute for per-session destination authority. The [product fit](../../targets/github-copilot-agents/product-fit.md) identifies a controlled MCP response/error boundary and the missing platform-wide hook. Debugging utility and a reusable sink model are specified by the evidence contract; no broader secret-manager replacement is proposed.

### #5: DevPod

The [case study](../../targets/devpod/README.md) distinguishes helper forwarding, signing delegation and provider options. Per-process release needs additional host identity/isolation, not just a forwarded connection. Cleanup means closing future access plus separately governing consumer copies. A later AI consumer requires a new trust assessment. [Runtime release](../../capabilities/scoped-runtime-release.md) shares authority vocabulary with Baton but deliberately leaves delivery mechanisms separate.

### #6: Autonomous coding sandboxes

The [case study](../../targets/autonomous-coding-sandboxes/README.md) traces execution, terminal masking, observations and event persistence in a pinned SDK. The conclusion is a first-class vendor-neutral evidence envelope with separate text/structured/media contracts. Tool wrappers and serializers are candidate enforcement points; the inspected post-tool hook alone is insufficient. Retry multiplication is an inference, not a measured incident. Visual content and earlier spill/telemetry writes remain qualification gates.

### #1: Epic acceptance criteria

- Multiple concrete external examples: all five [target studies](../../targets/README.md), with source or official-documentation evidence and explicit scope.
- Recurring patterns: [agent evidence](../../patterns/agent-evidence-boundary.md), [materialization](../../patterns/secret-materialization.md), [persisted evidence](../../patterns/persisted-debug-evidence.md), and emerging [runtime release](../../patterns/runtime-secret-release.md). Each states its admission basis.
- Ownership: [product map](../../product-map/README.md), including core, vault, restore, optional anonymizer and external host responsibilities.
- At least one generic prototype candidate: [irreversible runtime evidence](../../capabilities/irreversible-sanitization.md), with inputs, outputs, invariants, failure behavior and synthetic validation plan.
- Non-goals/residual risk: each case's product fit plus the contract's explicit detection, runtime, media and persistence limits.
- No whole-runtime security claim: neither native controls nor proposed Redact Secret composition are treated as comprehensive protection.

The bounded research deliverables are documented. Runtime experiments and security contract approval remain explicitly unperformed and are not required to manufacture an “implemented” outcome. Issue closure, publication, implementation and vendor support are separate decisions.

## Pattern consolidation

The observation boundary is included in agent evidence, rather than duplicated in another nearly identical file. Local-to-remote development is a context within runtime release and this comparison; current evidence does not require a separate remote-development capability. Revisit only if new evidence adds a distinct requirement.

## Source provenance and remaining work

The user-supplied design conversation was read to recover repository organization and the optional anonymizer boundary. It is not used as evidence of external product behavior; its raw transcript and unrelated security claims are not retained here. Assertions from issue bodies were independently checked, narrowed or marked uncertain.

Live docs carry an access date, not an invented immutable revision. Primary source code links pin exact commits. No upstream software, credentials, captures or real-account tests were used. The [qualification gates](../open-questions/qualification-gates.md) state what evidence must precede stronger claims.
