# Agent evidence and observation boundary

Status: supported. Reviewed 2026-10-07.

## Problem

A runtime tool can return data from an application even when its source repository contains no credential. The observation boundary is the point where runtime-derived text or structure becomes agent input. It includes successful results and diagnostic failures.

## Evidence and admission

Independent support comes from [Baton logs/network](../targets/baton/findings.md#baton-002), [Copilot MCP](../targets/github-copilot-agents/findings.md#copilot-002), [Cursor MCP hooks](../targets/cursor-cloud-agents/findings.md#cursor-003) and [OpenHands terminal observations](../targets/autonomous-coding-sandboxes/findings.md#sandbox-001). This satisfies the multiple-independent-target admission rule. Supported means the boundary recurs, not that leakage or mitigation effectiveness has been measured.

## Common data flow

```text
runtime observation → tool/controller → model-facing result
```

## Security consequence (inference)

Runtime permission is not a decision about whether every returned value belongs in model context. Errors, URIs and structured metadata can be as sensitive as the main text. Returned data may also contain untrusted instructions; secret filtering is not prompt-injection prevention.

## Product opportunity and ownership

Prototype [irreversible sanitization](../capabilities/irreversible-sanitization.md) first. Hosts extract and reconstruct protocol fields; core detects and applies policy. [Anonymizer composition](../capabilities/composed-transformation.md) is optional for multiple finding sources. Vault and restore enter only for justified recovery.

## Counterexamples and product boundary

Vendor controls already exist: Cursor and GitHub document masking, and the SDK masks registered terminal secrets. Baton OTel is metadata-only. SDK PostToolUse is not a replacement filter. A shared contract must preserve these distinctions.

Hosts retain authentication, runtime isolation, permissions, process/workspace lifecycle and retention. No pattern establishes that an external runtime is secured or that every sensitive value can be detected.

## Open questions

Which host hooks can block or replace output before any observer, trace or persistence write? What policy covers unseen returned data and binary media?

## Supporting targets

Finding links above are the authoritative support set. See the [cross-target comparison](../research/comparisons/agent-runtime-boundaries.md) for source, consumer, hook and retention differences.
