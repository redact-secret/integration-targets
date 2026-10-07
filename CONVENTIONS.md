# Conventions

## 1. Core rule

> **Targets are evidence. Patterns are the product insight.**

Do not turn `integration-targets` into a list of products we might integrate with.

Every contribution should help distinguish:

- observed external behavior;
- inferred risk;
- recurring pattern;
- Redact Secret product hypothesis;
- implemented product capability.

These categories must not be blurred.

## 2. Language

Use precise, neutral language.

Prefer:

- "observed";
- "the source shows";
- "the documentation states";
- "this may create";
- "potential exposure";
- "candidate product capability";
- "requires further research".

Avoid unsupported statements such as:

- "unsafe";
- "secure";
- "vulnerable";
- "prevents leakage";
- "solves the problem";
- "production-ready";

unless the claim is directly supported and appropriately scoped.

## 3. Target naming

Directory names use lowercase kebab-case:

```text
targets/baton/
targets/cursor-cloud-agents/
targets/github-copilot-agents/
targets/devpod/
```

Use the upstream product's preferred name in prose.

When a case intentionally represents a broader category, name the category rather than pretending one vendor represents the whole market.

Example:

```text
targets/autonomous-coding-sandboxes/
```

## 4. Finding identifiers

Use stable target-prefixed identifiers when a target accumulates multiple findings.

Examples:

```text
BATON-001
BATON-002
CURSOR-001
DEVPOD-001
```

Do not renumber findings after publication.

A finding should contain:

```md
## BATON-001 — Short finding title

Status: observed
Confidence: high

### Observation

### Evidence

### Sensitive-data boundary

### Potential impact

### Related patterns

### Notes / uncertainty
```

## 5. Evidence priority

Prefer sources in this order:

1. source code;
2. official architecture/security documentation;
3. official product documentation;
4. reproducible behavior;
5. public maintainer issue/discussion;
6. secondary commentary.

Use primary sources whenever possible.

Record the exact repository path, version, commit, release, or documentation date when it materially affects the observation.

## 6. Observation vs hypothesis

Keep these separate.

### Observation

Example:

> Baton searches for `.env*` and selected secret-bearing configuration names and copies matching files into alternate worktrees.

This is a source-supported behavior.

### Hypothesis

Example:

> A runtime-scoped release contract may reduce the need to duplicate plaintext configuration into agent-owned worktrees.

This is a Redact Secret product hypothesis.

Never write the second as if it were already an implemented or validated capability.

## 7. Product-fit language

Use the following status vocabulary:

```text
implemented
planned
experimental
hypothesis
rejected
```

Example:

```md
Capability: scoped-runtime-release
Status: hypothesis
Potential owner: redact-secret-vault
```

Avoid assigning work to a product solely because it is the closest existing package.

## 8. Product boundaries

### Core

Use core for:

- detection;
- policy;
- irreversible redaction;
- safe metadata;
- evidence sanitization.

Do not assign:

- secret storage;
- retained mappings;
- restore authorization;
- runtime lifecycle.

### Vault

Use vault for:

- reversible capture;
- mapping lifecycle;
- source binding;
- sink/path grants;
- expiry/revocation;
- use budgets;
- server authority;
- qualified persistence.

Do not casually broaden vault into a general-purpose secret manager.

### Restore

Use restore for:

- token discovery;
- restore planning;
- authority preflight interaction;
- all-or-nothing reconstruction.

Do not assign restore:

- policy;
- authorization;
- storage;
- tenant/principal identity;
- crypto/key ownership;
- vendor-specific integrations.

## 9. Patterns

Create a new pattern only when at least one of the following is true:

- multiple independent targets exhibit the same boundary;
- one target provides unusually strong evidence for a clearly generalizable problem;
- an existing product decision depends on naming the boundary explicitly.

Pattern names should describe the problem, not the vendor.

Good:

```text
agent-evidence-boundary
runtime-secret-release
secret-materialization
persisted-debug-evidence
```

Poor:

```text
baton-env-problem
cursor-secret-feature
```

## 10. Target documents

Recommended target structure:

```text
targets/<target>/
├── README.md
├── data-flow.md
├── findings.md
└── product-fit.md
```

Do not create empty files in advance.

Create a document when there is enough evidence to justify it.

### `README.md`

Keep concise.

### `data-flow.md`

Facts and observed flows only.

### `findings.md`

Evidence-backed findings.

### `product-fit.md`

Redact Secret interpretation and hypotheses.

## 11. Research documents

Use `research/` for cross-target work that does not yet belong in a stable pattern.

Examples:

```text
research/comparisons/
research/open-questions/
```

A research document may remain uncertain.

When the conclusion stabilizes, move the durable result into:

- `patterns/`;
- `capabilities/`;
- `product-map/`.

## 12. GitHub issues

Use issues for bounded work.

Recommended issue types:

- Epic — broad problem space;
- Case study — external target;
- Research — unanswered cross-target question;
- Follow-up — evidence gap or validation task.

A case-study issue should clearly state:

> No vendor-specific implementation is required unless separately approved.

Closing a research issue does not mean Redact Secret supports the target.

## 13. Security claims

Do not claim that Redact Secret "secures" an external product.

Prefer narrow claims such as:

> Redact Secret may reduce unnecessary plaintext propagation across this boundary when the host provides an integration point.

Always document residual risk and external ownership.

## 14. Fixtures and examples

Use synthetic, unmistakably fake values.

Good:

```text
ghp_SYNTHETICxREVOKEDxTESTx0000000000000
user@example.test
192.0.2.10
```

Never commit:

- live credentials;
- real customer PII;
- production payloads;
- copied private logs;
- valid session cookies;
- internal secrets from an external target.

## 15. Screenshots and binary evidence

Avoid committing screenshots when text/source evidence is sufficient.

Screenshots can accidentally capture:

- user names;
- email addresses;
- access tokens;
- local filesystem paths;
- customer data;
- browser sessions.

If visual evidence is necessary, sanitize it before commit and record what was removed.

## 16. Structured metadata

Do not add schemas, generated indexes, or YAML inventories until manual maintenance becomes a real problem.

When added:

- source documents remain authoritative;
- generated files must be reproducible;
- metadata must not imply stronger confidence than the research supports.

## 17. File growth

Prefer a small number of durable documents over continuously adding audit snapshots.

Create a new file when it represents a stable conceptual boundary, not merely because a research session occurred.

Historical detail can remain in Git history and linked issues.

## 18. Review checklist

Before merging research documentation, verify:

- Is each factual claim supported?
- Are observations separated from hypotheses?
- Is uncertainty explicit?
- Does the proposed capability remain useful beyond the named vendor?
- Is product ownership consistent with `ARCHITECTURE.md`?
- Are non-goals stated?
- Are sensitive fixtures synthetic?
- Does the document avoid implying unsupported integration or security guarantees?
