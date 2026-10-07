---
name: safe-research-review
description: Inspect research text and artifacts for sensitive data, unsafe publication, and overbroad protection claims. Use before sharing research or when reviewing a diff; not an automatic full-history audit.
---

# Review research publication safety

Read `SECURITY.md` and the examples/evidence rules in `CONVENTIONS.md`. Establish
whether the scope is a diff, working tree, selected artifacts, or publication
review. A working-tree review is not a full-history audit.

Inventory scoped files before reading content. Avoid dumping raw logs, captures,
or suspect files into terminal output or chat. If using a scanner, use a mode
that reports only paths, locations, and categories; inspect its configuration
and coverage before claiming protection. Do not invent a scanner command.

Check for credentials, session values, real PII/PHI, production payloads, private
logs/captures, account identifiers, user filesystem paths, private repository
URLs, unreleased plans, and confidential third-party details. Distinguish clearly
synthetic examples from unknown-origin material; an expired or revoked real
value is not made synthetic by adding a label. Never echo a suspected value.

Prefer source/text references over screenshots. If visual evidence is necessary,
inspect the entire artifact and applicable metadata for browser sessions,
customer data, tokens, local paths, and private information. If the available
tools cannot inspect a format, mark it not assessed. Sanitized text does not
prove the pixels or embedded payloads are sanitized.

Review whether research execution used bounded synthetic environments and
whether the document exposes an undisclosed vulnerability. Keep vulnerability
details out of public artifacts and point to the owning project's private
reporting process without contacting anyone automatically.

Report findings with file/location, category, why publication is problematic,
and a safe correction such as replacement with synthetic text or omission.
Record required additional review under `SECURITY.md` and distinguish checked
text, checked media, and unassessed artifacts. Absence of matches is not proof
of safe history or total protection. Do not delete artifacts, rewrite history,
upload material, or contact third parties without authorization.
