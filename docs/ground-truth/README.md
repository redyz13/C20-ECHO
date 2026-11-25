# Ground Truth

## Structure

| Path | Content |
|---|---|
| requirements/rad/ | Requirements and analysis models |
| architecture/sdd/ | System architecture |
| architecture/dpd/ | Design patterns |
| traceability/ | Traceability matrix |
| verification/tp/ | Test plan |
| verification/tcs/ | Test case specifications |
| engineering/ | Technology stack, coding conventions and design system |

## Rules

- Check `document-register.yaml` before selecting specifications.
- Use verified, task-relevant artifacts and applicable cross-cutting constraints.
- Follow traceability links and model dependencies.
- Check `requirements/rad/known-issues.md` for unresolved RAD issues.
- Block tasks only when unresolved specification conflicts materially affect correctness.
- Verify relevant unverified artifacts against their source when available. Escalate material uncertainties only.
- Preserve source identifiers, titles, model elements and semantics.
- Report missing, ambiguous or conflicting specifications.
- Agents must not modify any file under docs/ground-truth/.

## Engineering Standards

- [Technology Stack](engineering/tech-stack.md)
- [Coding Conventions](engineering/coding-conventions.md)
- [Design System](engineering/design-system.md)
