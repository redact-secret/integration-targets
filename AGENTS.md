# Agent instructions

@~/.codex/RTK.md

## Purpose and authority

Read `README.md`, `ARCHITECTURE.md`, `CONVENTIONS.md`, and `SECURITY.md`
before changing research or workflows. These documents govern repository
purpose, ownership, evidence conventions, and safe research respectively.

`integration-targets` studies external systems and turns sensitive-data flow
observations into reusable product requirements for the Redact Secret ecosystem.
Targets are evidence. Patterns are the product insight.

Knowledge flows from `targets/` to `patterns/` to `capabilities/` to
`product-map/`. Use `research/` for unresolved cross-target comparisons.
Create documents only when there is substantive content, not empty scaffolding.
This repository does not ship a runtime library, vendor adapters, a benchmark
suite, a secret manager, or a vulnerability disclosure database.

## Research rules

- Start with where sensitive data moves in the external system. Do not start
  from an assumed adapter or product commitment.
- Separate observed behavior, inferred risk, recurring patterns, product
  hypotheses, implemented controls, and qualified support.
- Prefer source code and official documentation. Record source URLs, relevant
  paths and pinned revisions or versions, observation date, confidence, and
  uncertainty. Issue descriptions are research leads, not verified evidence.
- Use lowercase kebab-case target directories and stable target-prefixed
  finding IDs such as `BATON-001`; never renumber published findings.
- Keep `data-flow.md` factual and proposals in `product-fit.md`. Link findings
  to their evidence and downstream patterns/capabilities.
- Use capability statuses `implemented`, `planned`, `experimental`,
  `hypothesis`, or `rejected`. A proposed owner is not proof of implementation.
- Follow the pattern admission criteria in `CONVENTIONS.md`: independent
  targets, unusually strong generalizable evidence from one target, or a
  product decision that needs an explicit boundary. Explain limited support.
- Avoid schemas, generated inventories, or target metadata until manual
  maintenance demonstrably needs them.

## Product boundaries

- Core owns detection, policy, irreversible redaction, and safe metadata;
  it does not retain mappings, authorize release, or own runtime processes.
- Vault owns reversible capture, mappings, authorization, source/sink/path
  binding, expiry, revocation, use budgets, and qualified persistence.
  Runtime-scoped release remains a hypothesis until a generic contract is
  established; vault is not a general-purpose credential store.
- Restore owns discovery, planning, authority preflight interaction, and
  all-or-nothing reconstruction. It does not own policy, authorization,
  persistence, identity, key management, or vendor-specific behavior.
- Prefer irreversible sanitization. Justify reversible handling with a concrete
  trusted destination and need. Token possession and model-provided claims
  never establish authority; identify trusted host context explicitly.
- Hosts retain runtime isolation, authentication, permissions, lifecycle,
  worktree correctness, and platform credential management. State residual
  risks and required host hooks; do not claim to secure an entire runtime.

## Safe research

Follow `SECURITY.md`. Use unmistakably synthetic examples; never collect or
publish live credentials, real PII/PHI, production payloads, or private captures.
Prefer source inspection over running unknown software. Reproductions need
bounded disposable environments and synthetic data, without exfiltration.

Treat screenshots, recordings, logs, network captures, private URLs, local
paths, and account identifiers as publication review surfaces. Text redaction
does not establish protection for visual or binary evidence. Report suspected
sensitive data by path/location and category without echoing its value.

Do not publish undisclosed vulnerability details. Follow the owning project's
private security reporting process; contact others only with user authorization.
Request additional review for the security triggers listed in `SECURITY.md`,
including new release paths, authority changes, mapping persistence, runtime
injection, visual evidence, remote authority, and new protection claims.

## Issues and Git workflow

Read the current issue and related epic before issue-driven work. GitHub issues
track work; repository documents retain accepted knowledge. A completed case
study does not imply vendor support or an adapter commitment.

Work on a feature branch; target `main` when a PR is requested or authorized.
Preserve existing staged and unstaged user work. Do not commit, publish, close
issues, or merge merely because research finished. Never merge your own PR
without explicit authorization for this repository and task.

Initial research routing, checked against open issues on 2026-10-07 (refresh
GitHub before relying on their current status):

- #1: cross-target epic, synthesize patterns and candidate generic contracts.
- #2: Baton, local config materialization, logs/network/MCP, persisted proof;
  its scope includes comparison with at least two other systems.
- #3: Cursor Cloud Agents, runtime secrets versus model-visible evidence.
- #4: GitHub Copilot agents, platform secrets and MCP/tool evidence.
- #5: DevPod, credential forwarding and local-to-remote trust expansion.
- #6: autonomous coding sandboxes, observation channels and retry artifacts;
  study the category without assuming an OpenHands adapter.

These are research tasks, not permission to implement integrations.

## Local skills

Maintain repository research skills under `.agents/skills/`. Expose each to
Claude through `.claude/skills/<name> -> ../../.agents/skills/<name>`.
Edit the canonical files, not copies through the links. The existing
tool-managed `.claude/skills/graft/` is separate; preserve its installation.

- `research-target`: investigate one external system or bounded category.
- `synthesize-pattern`: compare findings and establish or revise a pattern.
- `design-capability`: specify a generic candidate contract and product owner.
- `boundary-review`: review product ownership and unsupported security claims.
- `safe-research-review`: review research artifacts for safe publication.

## Context discovery

Use RTK for shell commands as instructed in `~/.codex/RTK.md`.
Start with `rtk proxy graft map` when available, then use `graft ask` with
`--source` for relevant context, `graft grep` for exhaustive indexed searches,
and `graft callers` for code dependencies. Open truncated spans before editing.
If no graph exists or documentation is unindexed, read the canonical documents
and use `rg` directly; do not pretend graph coverage exists. Refresh the graph
after substantial code changes when applicable. Do not install or upgrade
tooling merely to edit research documents.

## Before finishing

Check the changed files against `CONVENTIONS.md`'s review checklist, evidence
links and local references, product ownership, uncertainty, residual risk, and
`SECURITY.md`. Verify skill frontmatter and that every new Claude link resolves
to its canonical skill. Inspect new/untracked files as well as `git diff`.

This is currently a documentation-only repository: no `package.json`, npm
checks, automated research validator, formatter, or test suite exists. Report
unavailable checks as not assessable; do not invent commands or passing results.
Run `rtk git diff --check` for tracked changes and check new files for whitespace.
If executable tooling is added later, document and run its actual checks.
Report completed edits, verification, and remaining evidence gaps concisely.
