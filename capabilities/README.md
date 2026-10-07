# Candidate capabilities

Every document here has status `hypothesis` for the proposed host contract. Existing product primitives are cited separately and do not imply that any target integration is implemented or qualified.

- [Irreversible evidence sanitization](irreversible-sanitization.md): first prototype candidate; core plus trusted host interception.
- [Composed transformation](composed-transformation.md): optional anonymizer orchestration when multiple finding sources justify it.
- [Reversible evidence capture](reversible-capture.md): vault retention only for a concrete recovery need.
- [Authorized restore](authorized-restore.md): whole-request reconstruction under current vault authority.
- [Scoped runtime release](scoped-runtime-release.md): trusted runtime delivery, still requiring authority and host-lifecycle design.

Start with irreversible handling. Release paths, injection, mapping persistence, remote authority and visual handling require additional review under [SECURITY.md](../SECURITY.md). These drafts record those review needs; they are not approval to implement or publish a supported profile.
