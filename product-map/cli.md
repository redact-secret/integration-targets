# CLI ownership

Status: implemented command-line host adapter; upstream documents beta releases, not stable support. This source review did not run upstream tests or independently verify release artifacts.

The [pinned CLI README](https://github.com/redact-secret/redact-secret/blob/95293414dbd2dbdd21103a921a746cf346b28d94/crates/secret-scan-cli/README.md), inspected 2026-10-08, identifies package `redact-secret-cli`, binary `redact-secret`, and source path `crates/secret-scan-cli` in the core repository.

CLI owns arguments, environment/filesystem/stdin access, reports and exit codes. Core owns all detection, policy and redaction decisions. Check mode scans supplied files or stdin, including a staged diff piped by the caller; it does not traverse Git history. Redact mode writes to stdout and never modifies input files in place.

Check-mode exits are `0` for no findings, `1` for findings and `2` for usage/processing failure. Redact mode returns `0` only when the complete output was written, and `2` on usage/processing failure. Streaming failures may leave a sanitized but incomplete prefix: callers must check success before using output and discard output on any unexpected failure status. Detection is bounded and incomplete, and PII is opt-in.

CLI owns neither mappings nor release authority nor runtime isolation. Pipeline placement and output delivery remain caller responsibilities. Related research: [irreversible evidence sanitization](../capabilities/irreversible-sanitization.md), whose generic host contract remains a hypothesis.
