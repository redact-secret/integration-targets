# Cursor Cloud Agents: product fit

Status: hypothesis for every target-specific application below. This is research, not implemented integration or qualified support.

## Finding-to-capability mapping

[CURSOR-001](findings.md#cursor-001) is evidence of an existing native control, not proof of a missing vendor feature. First select the appropriate native secret class. Additional [irreversible evidence policy](../../capabilities/irreversible-sanitization.md) is a hypothesis for host-controlled MCP output and selected data types that need independent qualification.

[CURSOR-003](findings.md#cursor-003) identifies a documented MCP replacement hook. It does not establish complete interception of early turns, terminal results or stored artifacts. [CURSOR-002](findings.md#cursor-002) supports treating storage policy independently of display policy.

No present requirement for Redact Secret reversible capture was established. Only a separately approved need for an authenticated human to recover a selected original field would justify capture. Runtime release remains a hypothesis, not a replacement for Cursor provisioning or its native secret controls.

## Minimum host hooks

For a viable integration the host must supply trusted run identity and a controlled MCP server or qualified hook, prove ordering before each intended destination, and identify retention destinations. Repository-controlled scripts alone are not trustworthy authority if the agent can edit them. Do not treat a post-tool callback as proof that raw artifacts were never uploaded.

## Residual risk and non-goals

Cursor owns VM isolation, accounts, repository access, egress, snapshots and deletion. No claim covers screenshots/video, all PII or encoded/derived values. Qualification needs a synthetic canary exercise at the specific hook and storage path; no live tenant was tested.

## Qualification

Use the [qualification gates](../../research/open-questions/qualification-gates.md) before any support claim. Reversible release, runtime injection and visual handling need additional security review under [SECURITY.md](../../SECURITY.md). No such implementation is approved by this case study.
