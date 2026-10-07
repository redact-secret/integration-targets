# Integration Targets

Integration Targets studies real systems where sensitive data crosses application, runtime, agent, and evidence boundaries, and turns those observations into reusable product requirements for the Redact Secret ecosystem.

> **Targets are evidence. Patterns are the product insight.**

This repository is not a backlog of vendor integrations and does not imply that Redact Secret will build or maintain an adapter for every system documented here.

Its purpose is to study real external products, runtimes, workflows, and developer environments; identify recurring sensitive-data boundaries; and determine where those boundaries map to `redact-secret`, `redact-secret-vault`, `restore`, or a future ecosystem capability.

## Start reading

The initial research set is documented as of 2026-10-07:

- [Five target studies](targets/README.md), with pinned sources or dated official documentation.
- [Cross-target conclusions and issue #1–#6 outcomes](research/comparisons/agent-runtime-boundaries.md).
- [Recurring patterns](patterns/README.md) and [candidate contracts](capabilities/README.md).
- [Product ownership](product-map/README.md), including the optional proposed anonymizer boundary.
- [Remaining qualification gates](research/open-questions/qualification-gates.md) and [contribution workflow](CONTRIBUTING.md).

Source research does not establish tested integrations. The first prototype candidate is irreversible evidence sanitization; runtime release remains a hypothesis. No vendor adapter or runtime library is shipped here.

## Why this repository exists

Modern coding systems increasingly combine:

- autonomous or semi-autonomous coding agents;
- local and remote development runtimes;
- Git worktrees and disposable environments;
- shell and process execution;
- browser and simulator control;
- MCP and other tool protocols;
- network inspection;
- logs, traces, screenshots, and proof artifacts;
- repository, organization, cloud, and local runtime secrets.

This creates sensitive-data paths that traditional source scanning alone does not address.

A secret or PII value may never be committed to Git and still cross into a model or persist in debugging evidence:

```text
trusted developer environment
          |
          +----------------------+
          |                      |
          v                      v
    runtime inputs          runtime outputs
   env / config / auth     logs / network /
          |               diagnostics / proof
          |                      |
          +-----------+----------+
                      |
                      v
               coding agent / LLM
```

Integration Targets records these cases so the Redact Secret ecosystem can distinguish isolated vendor behavior from recurring market-level problems.

## Repository model

Knowledge should flow through four layers:

```text
External systems
      |
      v
targets/
Concrete observations and evidence
      |
      v
patterns/
Recurring cross-product problems
      |
      v
capabilities/
Vendor-neutral product capabilities
      |
      v
product-map/
Ownership across core / vault / restore
```

### `targets/`

One directory per external system or clearly defined system category.

A target is evidence, not a commitment to integrate.

Examples:

- Baton
- Cursor Cloud Agents
- GitHub Copilot coding agents
- DevPod
- autonomous coding sandboxes

Target research should distinguish observed facts from inferred product opportunities.

### `patterns/`

Recurring problems observed across multiple targets.

Examples:

- agent evidence boundary;
- runtime secret release;
- observation boundary;
- secret materialization;
- persisted debug evidence;
- remote development boundary.

A pattern becomes more valuable as independent targets support it.

### `capabilities/`

Vendor-neutral Redact Secret capabilities that could address one or more patterns.

Examples:

- irreversible evidence sanitization;
- reversible capture;
- authorized restore;
- scoped runtime release.

Capabilities may be implemented, planned, experimental, or hypotheses. Their status must be explicit.

### `product-map/`

Defines ownership boundaries across the ecosystem.

At minimum:

- `redact-secret` core;
- `redact-secret-vault`;
- `restore`.

This layer exists to prevent product-boundary drift. A new use case must not silently move authorization, persistence, runtime ownership, or reconstruction into the wrong package.

## Issue workflow

GitHub issues are work units. Repository documents are durable knowledge.

A typical flow is:

```text
case-study issue
      |
      v
source review / research
      |
      v
document observed findings
      |
      v
extract or strengthen patterns
      |
      v
map patterns to capabilities
      |
      v
record product ownership
```

An issue can be closed after the research work is complete even when the resulting pattern remains active.

## Current epic

The initial research track is:

**Protect sensitive data across AI coding runtime and agent evidence boundaries.**

Initial case studies include:

- Baton — local runtime, worktree, network, and proof evidence;
- Cursor Cloud Agents — runtime secrets vs agent-visible evidence;
- GitHub Copilot coding agents — repository secrets and MCP/tool boundaries;
- DevPod — credential forwarding across remote development environments;
- autonomous coding sandboxes — runtime observation as a sensitive-data boundary.

The goal is not to build five adapters.

The goal is to learn whether the same product requirements recur across all five systems.

## Product boundaries

Integration Targets may identify opportunities for Redact Secret to:

- sanitize logs, diagnostics, network evidence, and tool output;
- prevent sensitive values from unnecessarily entering model context;
- capture values reversibly where a trusted destination genuinely requires later recovery;
- bind release to trusted runtime context such as source, session, purpose, sink, and path;
- reduce plaintext duplication across agent-controlled development environments.

This repository must not imply that Redact Secret owns:

- process or VM sandboxing;
- daemon authentication;
- IDE authorization;
- third-party account security;
- Git worktree correctness;
- cloud-provider secret storage;
- operating-system isolation;
- arbitrary malicious local code.

The host system remains responsible for its own runtime and security boundary.

## Evidence standard

Prefer primary evidence:

1. source code;
2. official architecture or security documentation;
3. official product documentation;
4. reproducible behavior;
5. public issue or maintainer discussion.

Record uncertainty when behavior cannot be confirmed.

Do not turn inference into fact.

## Security

Never use live secrets, customer data, real PII, production credentials, private tokens, or confidential payloads as research fixtures.

See [SECURITY.md](SECURITY.md).

## Repository status

This repository is research-oriented.

Documents may describe:

- observed behavior;
- product hypotheses;
- planned capabilities;
- open questions.

Every document should make clear which category a statement belongs to.
