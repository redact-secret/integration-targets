# Security Policy

## Scope

`integration-targets` is a research repository.

It studies external systems where secrets, credentials, PII, PHI, session data, and other sensitive values may cross application, runtime, agent, tooling, or evidence boundaries.

The repository itself must not become a collection point for the sensitive data it studies.

## Never submit live sensitive data

Do not commit, upload, paste into issues, or attach:

- live credentials;
- API keys;
- cloud access keys;
- database passwords;
- session cookies;
- authentication headers;
- signing keys;
- private keys;
- production connection strings;
- real customer PII or PHI;
- private runtime logs containing sensitive values;
- database dumps;
- private network captures;
- internal screenshots containing customer or credential data.

Use unmistakably synthetic fixtures.

Examples:

```text
ghp_SYNTHETICxREVOKEDxTESTx0000000000000
sk_test_SYNTHETIC_NOT_VALID
user@example.test
192.0.2.10
```

## External vulnerability discoveries

This repository is not a vulnerability disclosure channel for third-party projects.

If research reveals a credible security vulnerability in an external product:

1. do not publish exploit details here;
2. do not open a public Integration Targets issue containing undisclosed vulnerability information;
3. use the upstream project's private security reporting process when available;
4. record only a sanitized high-level note here after disclosure is appropriate.

The purpose of this repository is product research, not public vulnerability coordination.

## Redact Secret vulnerabilities

A vulnerability in a Redact Secret repository should be reported through that repository's private security advisory channel.

Examples:

- detection bypass in `redact-secret`;
- unauthorized release in `redact-secret-vault`;
- partial plaintext exposure in `restore`;
- plaintext leakage through errors, traces, or diagnostics.

Do not use `integration-targets` as a substitute for the owning repository's security process.

## Research threat model

This repository studies several recurring boundaries.

### Agent evidence boundary

Sensitive data can appear in:

- stdout/stderr;
- diagnostics;
- tool responses;
- traces;
- HTTP headers;
- cookies;
- request/response bodies;
- generated debugging output.

Risk:

```text
runtime evidence
      |
      v
agent/tool controller
      |
      v
LLM or persisted artifact
```

### Secret materialization boundary

Sensitive configuration may be copied or materialized into:

- Git worktrees;
- remote workspaces;
- containers;
- virtual machines;
- temporary directories.

Risk:

```text
trusted source
     |
     v
plaintext copy
     |
     v
additional storage/lifetime
```

### Persisted evidence boundary

Temporary runtime data may become long-lived through:

- proof bundles;
- screenshots;
- videos;
- run histories;
- traces;
- test reports;
- exported diagnostics.

### Observation boundary

An autonomous agent may learn sensitive data simply by observing a running application, even when the source repository contains no secret.

## Research safety rules

### Prefer source inspection

Prefer reading code and documentation over executing unknown software.

### Avoid real-account testing

Do not test third-party secret handling with production or personal credentials when synthetic evidence is sufficient.

### Do not intentionally exfiltrate

Research should not attempt to cause an agent, tool, or external service to reveal credentials or private data merely to prove that such exposure is possible.

Use source-supported reasoning or controlled synthetic environments.

### Bound test environments

When reproduction is required:

- use synthetic secrets;
- use disposable repositories/accounts where possible;
- avoid production infrastructure;
- remove generated sensitive artifacts after the test;
- document what was executed.

## Screenshots and recordings

Visual evidence is high risk because it may contain information not obvious to the researcher.

Before committing a screenshot or recording, check for:

- email addresses;
- account names;
- tokens;
- browser session state;
- local filesystem paths;
- customer data;
- private repository information;
- internal URLs.

Prefer textual evidence when possible.

## Logs and network captures

Do not commit raw logs or network captures from real applications unless they have been intentionally sanitized.

Pay particular attention to:

```text
Authorization
Cookie
Set-Cookie
Proxy-Authorization
X-API-Key
signed URLs
query parameters
request bodies
response bodies
```

If a sanitized excerpt is sufficient, include only the minimal excerpt.

## Product-claim safety

Security-sensitive product statements must distinguish:

- observed behavior;
- proposed mitigation;
- implemented control;
- tested control;
- qualified support.

Do not imply that a Redact Secret capability:

- secures an entire external runtime;
- provides process isolation;
- replaces a secret manager;
- prevents all model exposure;
- erases plaintext from managed runtime memory;
- protects screenshots or arbitrary binary media unless such support exists.

Prefer narrow statements.

Example:

> Redact Secret may reduce unnecessary plaintext propagation in model-facing logs when the host applies redaction before the agent boundary.

## Product ownership

Research must preserve ecosystem security boundaries.

### `redact-secret` core

May own detection, policy, irreversible redaction, and safe metadata.

### `redact-secret-vault`

May own reversible capture, mapping lifecycle, authorization, expiry, revocation, use budgets, and qualified persistence.

### `restore`

May own token discovery, restore planning, preflight interaction, and reconstruction.

Do not move authorization into `restore`.

Do not move general secret-manager responsibilities into the vault without a deliberate architecture decision.

## Sensitive repository metadata

This repository may reference private Redact Secret planning repositories or private issues.

Before making `integration-targets` public, review all documents for:

- private repository URLs;
- internal issue references;
- unreleased product details;
- confidential partner/vendor information;
- user-specific filesystem paths;
- account identifiers.

## Responsible publication

A target document should remain private or incomplete when publication would:

- reveal an undisclosed third-party vulnerability;
- expose confidential implementation details obtained non-publicly;
- include real sensitive data;
- overstate unverified security behavior.

Research completeness is less important than safe publication.

## Security review triggers

Request additional review when a contribution:

- proposes a new reversible release path;
- changes vault/restore responsibility;
- introduces persistence of mappings;
- proposes runtime secret injection;
- handles screenshots, recordings, or binary evidence;
- adds a remote authority path;
- claims protection against a new attacker class;
- introduces a new supported security profile.

## Security goal of this repository

The repository's role is to improve product understanding without increasing real-world exposure.

The guiding principle is:

> Study sensitive-data flows without collecting the sensitive data itself.
