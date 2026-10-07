# Contributing research

Read [README.md](README.md), [ARCHITECTURE.md](ARCHITECTURE.md), [CONVENTIONS.md](CONVENTIONS.md) and [SECURITY.md](SECURITY.md) first. This repository retains evidence and product requirements; it does not implement vendor adapters.

## Work from a bounded question

1. Refresh the current issue and parent epic. Preserve the existing working tree and use a feature branch.
2. Follow sensitive data from its source through runtime use, observation, model/tool exposure, persistence and cleanup. Check current primary sources; an issue or prior chat is a research lead, not evidence.
3. Record the source URL, exact source revision/path or live-document access date, confidence, uncertainty and stable target-prefixed finding ID. Separate observation from inferred impact.
4. Create substantive target files only. Compare independent systems before promoting a recurring pattern, or explicitly justify another admission condition.
5. Link patterns to generic capability hypotheses and product ownership. Prefer irreversible handling and name the host hooks, trusted destinations and residual risks.

Use the canonical [research-target](.agents/skills/research-target/SKILL.md), [synthesize-pattern](.agents/skills/synthesize-pattern/SKILL.md) and [design-capability](.agents/skills/design-capability/SKILL.md) workflows where appropriate. Keep reusable knowledge in documents and task state in issues.

## Review and verification

Apply [boundary-review](.agents/skills/boundary-review/SKILL.md) and [safe-research-review](.agents/skills/safe-research-review/SKILL.md) to changed and new files. Complete the conventions checklist, check local links and citation scope, and distinguish an implemented control from qualified support. Respect additional security-review triggers for release, persistence, remote authority, injection and media.

Run `rtk git diff --check` for tracked changes and inspect new files for whitespace, broken references and sensitive content. This documentation repository has no automated research validator, formatter or test suite. Ad hoc link checks are not security or runtime tests. Check skill frontmatter and Claude symlink targets when changing skills.

Do not install or execute upstream software just to inspect source. Do not collect real data, copy private transcripts or publish undisclosed vulnerability details. Use synthetic fixtures in separately authorized, disposable reproductions.

Research completion alone does not authorize commits, publication, issue closure or merge. A case study never implies vendor support.
