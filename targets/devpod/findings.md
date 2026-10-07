# DevPod findings

Scope: source commit `5a0efcbff6610ab114b421f68a890739a452e66b`, inspected 2026-10-07; OSS credential-helper paths. No workspace created.

<a id="devpod-001"></a>

## DEVPOD-001 — Git and Docker credentials are requested through helpers

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

DevPod installs/configures credential helpers. Its tunnel server gates Git and Docker lookups with separate allow flags, resolves local credentials and returns credential responses. Docker configuration selects the `devpod` credential store helper; this is not evidence of copying the entire local credential store.

### Evidence

- [Docker helper configuration](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/pkg/dockercredentials/dockercredentials.go#L44-L96).
- [Credential lookup and allow flags](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/pkg/agent/tunnelserver/tunnelserver.go#L147-L260).
- [Git credential fill](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/pkg/gitcredentials/gitcredentials.go#L203-L230).
- [Documented HTTPS helpers and SSH forwarding](https://devpod.sh/docs/developing-in-workspaces/credentials).

### Sensitive-data boundary

Workspace consumer → helper/tunnel → local credential source → response to consumer.

### Potential impact (inference)

Proxying can avoid a whole-store disk copy while still conveying usable credentials to a remote consumer. SSH agent forwarding exposes signing capability rather than demonstrating private-key file copying.

### Notes / uncertainty

Consumer caching, platform-mode behavior and provider-specific persistence need separate evidence. Forwarding is not proof of per-process isolation or guaranteed removal of returned values.

### Related patterns

[runtime-secret-release](../../patterns/runtime-secret-release.md)

<a id="devpod-002"></a>

## DEVPOD-002 — Provider options do not prove credentials enter the devcontainer

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

Provider documentation says options become provider-command environment variables, and illustrates obtaining AWS options from the local environment. It also allows options in the provider agent section.

### Evidence

[Provider options and local command examples](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/docs/pages/developing-providers/options.mdx#L6-L36), [AWS example](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/docs/pages/developing-providers/options.mdx#L126-L158).

### Sensitive-data boundary

Local option source → provider command; further movement depends on provider implementation.

### Potential impact (inference)

Provisioning authority and workspace runtime authority must be investigated separately. Treating every AWS option as forwarded into every container would overstate the evidence.

### Notes / uncertainty

No universal claim about AWS credentials being copied to workspaces is supported here. A specific provider and its environment/materialization code are needed for that assertion.

### Related patterns

[runtime-secret-release](../../patterns/runtime-secret-release.md)

<a id="devpod-003"></a>

## DEVPOD-003 — Tunnel shutdown is narrower than downstream cleanup

Status: observed. Observation date: 2026-10-07.
Confidence: high for the documented/source behavior; no runtime reproduction.

### Observation

The credential server forwards responses to requesters and closes its HTTP server when its context ends.

### Evidence

[Response handling](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/pkg/credentials/server.go#L94-L130), [context-driven server close](https://github.com/loft-sh/devpod/blob/5a0efcbff6610ab114b421f68a890739a452e66b/pkg/credentials/server.go#L60-L81).

### Sensitive-data boundary

Active forwarding service → consuming process; cancellation terminates the server.

### Potential impact (inference)

Future lookup availability and already-consumed credential lifetime are different. Introducing an agent into a workspace changes the consumer without automatically narrowing the existing forwarding permission.

### Notes / uncertainty

No tested guarantee about remote process memory, caches, volumes, snapshots or provider revocation. The later-agent scenario is an inference, not a reproduced DevPod behavior.

### Related patterns

[runtime-secret-release](../../patterns/runtime-secret-release.md)
