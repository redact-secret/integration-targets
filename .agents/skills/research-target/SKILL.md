---
name: research-target
description: Research one external product or bounded runtime category and document evidence-backed sensitive-data flows. Use for target case studies, not vendor adapter implementation.
---

# Research a target

Read the root instructions and canonical documents. Read the selected issue,
its parent epic, and existing target findings. Refresh issue scope from GitHub;
the initial case studies are #2 through #6, not a permanent task queue.

## Investigate

Follow sensitive data from source through transfer/materialization, runtime
use, observation, model/tool exposure, persistence, and cleanup. Distinguish
copying, proxying, and forwarding instead of assuming they have equal lifetimes.
Inspect primary sources and pin code evidence to a revision and path/lines.
Record observation date and product/version scope for changing documentation.
Issue assertions and secondary reports need independent verification.

For each finding record a stable target-prefixed ID, observation, source,
confidence with rationale, affected boundary, inferred impact, uncertainty,
and related patterns. Do not call an unverified path observed. If evidence is
unavailable, record the exact gap and what would establish the claim.

Focus according to the case: Baton covers config copies and logs/network/proof;
Cursor separates runtime need from model visibility; Copilot covers platform
secret scope and MCP/tool output; DevPod distinguishes forwarding from copying
and remote retention; autonomous sandboxes cover observation and retry loops.
Verify these leads rather than assuming the issue describes current behavior.
For Baton, address its comparison requirement with at least two other systems
or state that this part remains incomplete.

## Retain the result

Create only substantive files under `targets/<kebab-case-name>/`: orientation
and related issues in `README.md`, observed flows in `data-flow.md`, findings
in `findings.md`, and interpretations in `product-fit.md`. Use a category name
for category research. Update existing documents instead of session snapshots.

Map confirmed findings to generic opportunities, first considering irreversible
sanitization. For reversible proposals identify why later recovery is needed,
the trusted destination, host hooks, and authority context. Separate status
from ownership; do not imply implementation or vendor support. Record visual
evidence limitations, external responsibilities, and residual risk.

Check citations, cross-links, safe examples, and the requested issue outcomes.
Report what is established and what remains unknown. Do not close the issue,
post comments, run third-party software, or build an adapter by implication.
