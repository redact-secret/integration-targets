# Gateway ownership

Status: experimental. The upstream project describes `0.1.0-alpha.0` as an unpublished candidate with no stable support, distributable release or third-party audit. This review inspected documentation, not the qualification runs or production behavior.

The [pinned README](https://github.com/redact-secret/gateway/blob/4758580b5ddf843b434a019cf2ed66070114a3e2/README.md), inspected 2026-10-08, describes a Rust, language-independent HTTP gateway for a single application's localhost LLM egress. Working request coverage is limited to text-only subsets of OpenAI Chat Completions and stateless Responses; Kubernetes sidecar deployment is a separate qualification scope, not blanket runtime support.

Gateway owns bounded HTTP request admission, protocol-field classification, invoking core on designated application-controlled text, building the forwarded request and transport to a fixed configured provider route. Core retains detection, content policy and redaction decisions. This is a host-facing transport role, not vault release authority or restore reconstruction.

The documented contract forwards no request-body bytes before admission, inspection and transformation succeed. Provider responses, SSE streams and provider error contents remain unredacted. Detection can miss values, traffic that bypasses the gateway is outside coverage, and bytes already forwarded cannot be retracted. Qualification against fake upstreams does not verify the real provider DNS/TLS hop.

Deploying hosts retain application identity, permissions, network routing enforcement, runtime isolation and credential management. This inventory does not add a remote vault authority path, mapping persistence or runtime secret injection. Related research: [agent evidence boundary](../patterns/agent-evidence-boundary.md); request egress inspection alone does not sanitize model-facing tool evidence or provider responses.
