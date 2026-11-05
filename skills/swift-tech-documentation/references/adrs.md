# Architecture decision records

Consider an ADR when choosing a framework, architectural pattern, API shape, or platform-specific approach. Write it when the decision is made so the alternatives and constraints are still clear. An ADR records the decision's context and trade-offs, not a product requirement. Use the repository's existing location, template, numbering, and status conventions. If none exist, a simple record can contain:

```markdown
# Decision title

Date: YYYY-MM-DD
Status: Accepted | Declined | Outdated

## Context

What problem and constraints led to the decision?

## Decision

What was chosen?

## Consequences

What benefits, costs, and trade-offs follow?
```

An ADR must have status `Accepted`, `Declined`, or `Outdated` when merged into the working branch. Use `Outdated` when a decision no longer applies. Link an ADR from the code or documentation it explains. When a decision changes, update the record so it describes the current approach and preserve the reason for the change. When implementation departs from a documented plan, record what changed and why at the narrowest useful location; summarize it in the change description if one exists.
