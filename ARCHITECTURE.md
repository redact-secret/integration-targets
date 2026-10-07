# Architecture

## 1. Purpose

`integration-targets` is a product-research repository for the Redact Secret ecosystem.

It does not ship a runtime library and does not own production security behavior.

Its architecture is a knowledge architecture:

```text
external implementation
        |
        v
target evidence
        |
        v
recurring pattern
        |
        v
candidate capability
        |
        v
product ownership
```

The central design rule is:

> **Targets are evidence. Patterns are the product insight.**

## 2. Repository layers

### 2.1 Targets

`targets/` contains concrete external systems.

A target may be:

- a product;
- a framework;
- a runtime;
- a development environment;
- a protocol-driven tool;
- a clearly bounded product category when individual vendors are not the important distinction.

A target document records what the external system does.

It should not start by asking how Redact Secret can integrate with it.

The first question is:

> Where does sensitive data move in this system?

Recommended target layout:

```text
targets/<target>/
├── README.md
├── data-flow.md
├── findings.md
├── product-fit.md
└── target.yaml          # optional once structured metadata is useful
```

#### `README.md`

Short orientation:

- what the system is;
- why it is tracked;
- research status;
- related issues;
- related patterns.

#### `data-flow.md`

Observed data movement only.

Examples:

- local config -> worktree;
- repository secret -> runtime;
- runtime -> logs;
- network capture -> MCP;
- screenshot -> proof bundle.

Product proposals should not be mixed into this file.

#### `findings.md`

Discrete observations with evidence.

Recommended identifier form:

```text
BATON-001
CURSOR-001
DEVPOD-001
```

A finding should include:

- statement;
- evidence;
- confidence;
- affected boundary;
- possible impact;
- related pattern.

#### `product-fit.md`

Maps confirmed findings to Redact Secret capabilities.

This is where hypotheses belong.

### 2.2 Patterns

`patterns/` contains recurring problems supported by one or more targets.

A pattern is not vendor-specific.

Example:

```text
Baton ---------+
               |
DevPod --------+--> secret-materialization
               |
Cloud agent ---+
```

Recommended pattern document:

```md
# Pattern name

Status: emerging | supported | mature

## Problem

## Evidence

## Common data flow

## Security consequence

## Product opportunity

## Product boundary

## Open questions

## Supporting targets
```

A pattern should become stronger as independent evidence accumulates.

Do not create a pattern solely because it sounds plausible.

### 2.3 Capabilities

`capabilities/` records vendor-neutral capabilities that may address patterns.

A capability is not necessarily a package.

Examples:

- `irreversible-sanitization`;
- `reversible-capture`;
- `authorized-restore`;
- `scoped-runtime-release`.

Each capability should declare a status:

```text
implemented
planned
experimental
hypothesis
rejected
```

Recommended capability fields:

- problem addressed;
- inputs;
- outputs;
- trusted context required;
- security invariants;
- owning product;
- non-goals;
- supporting patterns;
- qualification needed.

### 2.4 Product map

`product-map/` protects ecosystem boundaries.

The initial product ownership model is:

```text
redact-secret core
    |
    | detection / policy / irreversible redaction / safe metadata
    v
redact-secret-vault
    |
    | capture / mapping / authorization / lifecycle
    v
restore
    |
    | restore planning / preflight interaction / reconstruction
    v
trusted destination
```

This is not a mandatory execution pipeline.

For many use cases, core-only irreversible sanitization is the correct solution.

## 3. Initial product ownership

### 3.1 `redact-secret` core

Owns:

- sensitive-data detection;
- policy evaluation;
- irreversible redaction;
- safe finding metadata;
- formatting of non-authoritative placeholders;
- evidence sanitization primitives.

Does not own:

- retained plaintext mappings;
- persistence;
- release authorization;
- runtime process ownership;
- secret injection;
- restore reconstruction.

### 3.2 `redact-secret-vault`

Owns reversible authority behavior:

- explicit capture;
- mapping lifecycle;
- source/capture binding;
- sink/path grants;
- purpose where applicable;
- principal/tenant checks in server profiles;
- expiry;
- revocation;
- use budgets;
- persistent authority profiles;
- current-policy checks.

Potential future capability under research:

- runtime-scoped release.

The vault must not become a general-purpose secret manager merely because integration targets expose secret-injection problems.

### 3.3 `restore`

Owns reconstruction:

- token discovery;
- occurrence validation;
- restore planning;
- interaction with an authority preflight/consume contract;
- all-or-nothing reconstruction;
- efficient output construction.

Does not own:

- storage;
- policy;
- tenant identity;
- principal identity;
- key management;
- persistence;
- secret detection.

`restore` should remain unaware of specific targets such as Baton, Cursor, or DevPod.

## 4. Research-to-product flow

The preferred decision flow is:

```text
1. Observe target behavior
2. Record evidence
3. Identify a recurring boundary
4. Compare with other targets
5. Name the pattern
6. Decide whether Redact Secret can reduce the risk
7. Define a generic capability
8. Assign product ownership
9. Prototype only after the contract is sufficiently generic
```

Vendor-specific adapter work should occur only after step 8 and only when justified separately.

## 5. Initial recurring patterns

The first epic is expected to test at least these patterns.

### Agent evidence boundary

```text
runtime evidence
      |
      v
agent/tool controller
      |
      v
LLM
```

Relevant evidence:

- logs;
- diagnostics;
- network details;
- traces;
- tool results.

Likely owner:

- core for irreversible sanitization;
- vault + restore only when controlled reveal is explicitly required.

### Runtime secret release

```text
secret needed by runtime
          |
          X
model does not need plaintext
```

Likely owner:

- vault authority if reversible/runtime-scoped release proves justified.

Status:

- hypothesis until a generic contract is defined.

### Observation boundary

```text
application
    |
    v
runtime observation
    |
    v
agent
```

This broadens secret protection beyond files and prompts.

### Secret materialization

```text
trusted secret source
       |
       v
copy / materialize
       |
       v
worktree / VM / container
```

The research goal is to understand when plaintext-at-rest duplication is avoidable.

### Persisted debug evidence

```text
temporary runtime value
        |
        v
debug/proof artifact
        |
        v
long-lived storage
```

Examples:

- proof bundles;
- traces;
- HAR-like captures;
- screenshots;
- test reports;
- run histories.

## 6. Structured metadata

Do not introduce structured metadata merely for completeness.

Add `target.yaml`, JSON schemas, or generated matrices only when enough targets exist that manual maintenance becomes error-prone.

A future target record may look like:

```yaml
id: baton
name: Baton
status: researched

category:
  - local-runtime
  - coding-agent
  - mcp

observed_boundaries:
  - secret-materialization
  - agent-evidence
  - persisted-debug-evidence

product_fit:
  core:
    - irreversible-sanitization
  vault:
    - reversible-capture
    - scoped-runtime-release
  restore:
    - authorized-restore
```

Schemas should validate records, not dictate research conclusions.

## 7. Issues vs repository files

GitHub issues manage work.

Repository files retain accepted knowledge.

Do not require readers to reconstruct product conclusions from old issue threads.

Conversely, do not copy every investigative comment into permanent documentation.

Move durable conclusions into repository files when they are sufficiently supported.

## 8. Non-goals

This repository is not:

- an adapter monorepo;
- a secret manager;
- an integration marketplace;
- a vulnerability disclosure database;
- a benchmark suite;
- a competitor scorecard;
- a promise to support documented vendors.

A target may remain valuable even when no integration is ever built.

## 9. Success criteria

The repository is working when it helps answer questions such as:

- Is this problem unique to one tool or recurring across the ecosystem?
- Can core solve it irreversibly?
- Does the use case genuinely need vault semantics?
- Is restore required, or would restoration unnecessarily increase risk?
- What trusted context must a host provide?
- What remains the responsibility of the external runtime?
- Which product capability would still make sense if the named vendor disappeared tomorrow?
