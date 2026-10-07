# Irreversible runtime evidence sanitization

Status: hypothesis for this host integration contract. Proposed owner: core for detection, policy and irreversible replacement; host for interception, parsing, enforcement and output delivery. This is the first contract worth prototyping, not an implemented vendor integration.

The existing core exposes standalone scan/redact operations; that is narrower than qualification of this contract. [Pinned core README](https://github.com/redact-secret/redact-secret/blob/f6f481b168b000ac27e8d60598cd2cb5c0265d59/README.md), reviewed 2026-10-07. No package was installed or executed here.

## Supported problem

[Agent evidence](../patterns/agent-evidence-boundary.md) and [persisted debug evidence](../patterns/persisted-debug-evidence.md) recur across independent targets. The same transformation decision should govern model-facing output and retained diagnostics without making a text library own protocols or storage.

## Inputs and outputs

The proposed host envelope carries an opaque observation ID, channel, trusted source/run identity, destination (`model-evidence` or `persisted-evidence`), policy/profile version, and a bounded payload. These names describe a candidate contract, not a current SDK API.

Payload variants are UTF-8 text or host-extracted text fields with canonical structural paths. The host retains the original schema and reconstructs it after processing. HTTP, MCP and log parsers remain outside core/anonymizer. Numeric metadata is allowed only by an explicit policy, not because it is called metadata.

Return either a complete sanitized representation with a manifest, or a fixed input-free denial/error. The manifest carries transformation counts, categories, policy version, completeness/truncation state and an opaque correlation ID. It must not contain original snippets, credential fingerprints, raw URLs, unreviewed paths, tokens or replayable grants.

## Processing and invariants

1. The trusted host admits the channel and bounds bytes, nesting and field count before transformation. It validates encodings and structural paths. Limits must be explicit in a prototype profile; no production thresholds are invented here.
2. Inspect text and sensitive structural fields, including URI components, headers, cookies, errors and payloads. A parse error or unsupported type causes withholding or an explicit safe omission, never fallback to raw bytes.
3. Apply selected detection and policy. Core `block` is a host decision to reject the evidence, not merely replacement text. A host must explicitly handle `warn` and `allow`; the default detector policy is not a blanket no-sensitive-data policy.
4. Rebuild the representation and run size/structure checks. Keep any raw input confined to the host's trusted processing boundary.
5. Publish only the completed result to each authorized model/storage sink. Do not log raw input, exceptions or intermediate fields during processing. A successful model write does not prove the storage path used the same filter.

Irreversible placeholders are display labels, not recoverable tokens. Mapping retention is absent by default. An empty finding set means no supported finding under the selected policy, not proof of clean data.

## Streaming and errors

For a first prototype, buffer a bounded complete record before publication. When a record exceeds limits, omit it with a safe status rather than emit an unexamined prefix. Do not split on arbitrary transport chunks and assume secrets align with chunks.

A later streaming profile must use the core's qualified incremental semantics, hold incomplete matches and UTF-8 sequences, and prove flush, cancellation, overflow and cross-chunk behavior. Existing core streaming support does not qualify any chosen host framing. No universal overlap window is specified.

Every error path and retry uses the same policy; no automatic retry with weaker detection, larger release grants or raw pass-through. Backpressure and disposal belong to the host.

## Debugging usefulness

Preserve method/status, duration, byte counts, error class, event order and correlation where policy permits. Normalize endpoints rather than forwarding raw query values. Preserve JSON shape and field presence without retaining original field values. Classification/counts can explain that a value was removed.

Use separate policies for model context and retained proof if their audience/lifetime differ; both must enforce the required baseline. Measure diagnostic usefulness on synthetic failures, not merely whether output looks plausible.

## Trust and residual risks

The host must control the hook and policy outside model-writeable authority, and know every intended consumer. A filter installed only in a display callback cannot cover earlier file, telemetry or screenshot writes. Redaction does not defeat arbitrary code with raw-process access, prompt injection, unknown formats, unsupported encodings or all PII/PHI.

Images, video and opaque binary bodies are outside this text contract. Exclude them from a claimed protected sink or route them to a separately qualified media process; see [qualification gates](../research/open-questions/qualification-gates.md#visual-evidence).

## Bounded synthetic qualification plan

Use a disposable host harness without external accounts or network destinations. Exercise synthetic credentials, `user@example.test`, unknown secret formats, safe negative examples, nested fields, errors, fragmented records, invalid encoding, cancellation and oversized inputs. Record which classes are deliberately unsupported.

Intercept both the model sink and artifact writer. Require zero synthetic protected values at those sinks, valid reconstructed structure, input-free errors, and policy-approved diagnostic fields. A deliberately unsupported channel must be rejected, not counted as passing. Verify all actual release/profile limits against their boundary cases when chosen.

This repository defines the research contract only. A harness, release conformance suite and vendor adapter require separate implementation work.
