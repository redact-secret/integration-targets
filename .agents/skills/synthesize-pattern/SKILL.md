---
name: synthesize-pattern
description: Compare target findings to extract or revise vendor-neutral sensitive-data patterns. Use for cross-target research and epic synthesis, not to treat proposed issue claims as observations.
---

# Synthesize a pattern

Read `CONVENTIONS.md` sections on patterns and research documents plus existing
target findings and the relevant epic. Work from finding IDs and sources, not
vendor names or the number of issue descriptions repeating the same premise.

Compare source, boundary crossing, observer, retention, host interception hook,
and cleanup across targets. Separate independent evidence from shared upstream
claims. Preserve differences such as local versus remote execution, copied
versus proxied credentials, live versus persisted evidence, and text versus
visual channels. Note counterexamples and missing evidence.

Admit a pattern when multiple independent targets support it, one target gives
unusually strong evidence of generalizability, or a product decision requires
the boundary to be named. State which condition applies. If none applies,
retain the question under `research/comparisons/` or `research/open-questions/`.

Write or update `patterns/<problem-name>.md` with status (`emerging`,
`supported`, or `mature`), problem, linked evidence/finding IDs, common flow,
security consequence, opportunity, product boundary, open questions, and
supporting targets. Explain the chosen status; there are no numeric maturity
thresholds in this repository. Do not invent one or promote confidence from
target count alone.

Map the pattern toward candidate capabilities without silently implementing
contracts. Include host responsibilities and residual risk. Keep unstable
comparisons in `research/` and durable conclusions in the owning layer.

For epic synthesis, check the live acceptance criteria: multiple concrete
examples, recurring flows, core/vault/restore mapping, at least one generic
contract worth prototyping, explicit non-goals and residual risk, and no claim
that the external runtime is secured. Link evidence or mark a criterion open.
Research completion does not authorize an issue closure or adapter commitment.
