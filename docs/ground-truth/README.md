# Ground Truth

## Structure

| Path | Content |
|---|---|
| `document-register.yaml` | Baseline versions, status and source locators |
| `requirements/rad/` | Requirements and analysis models |
| `architecture/sdd/` | System architecture |
| `architecture/dpd/` | Design patterns |
| `traceability/` | Requirement-keyed traceability index |
| `verification/tp/` | Test plan |
| `verification/tcs/` | Test case specifications |
| `engineering/` | Technology stack, coding conventions and design system |
| `../sources/` | Canonical source documents |

## Baseline

- Use the document register to select the current baseline. `finalized` denotes a closed source document; `complete` denotes completed extraction within scope; `verified` denotes an accepted operational baseline with integrity and traceability checks and documented exceptions. It does not assert exhaustive semantic equivalence, absence of source defects or product compliance.
- Approved engineering standards are normative. Their `validation_status` tracks technical integration and enforcement, not approval. Pending documents are unavailable as normative specifications.
- RAD defines requirements, SDD and DPD define design, TP and TCS define verification obligations, and MT indexes declared relationships. Engineering standards govern implementation within these constraints. Do not resolve material conflicts by inventing requirements or silently overriding a source.

## Context retrieval

1. Select the applicable baseline and requirement IDs; use `traceability/mt.json` to locate relevant artifacts.
2. Load only task-relevant specifications, model dependencies, cross-cutting constraints and known issues. Apply recorded dispositions; do not treat clarified issues as open decisions.
3. Consult the relevant original source only if a material discrepancy, omission or ambiguity remains unresolved. Retrieve only the necessary sections, pages or cells; never routinely attach or index entire originals. Do not disclose personal data from source front matter.
4. Escalate only unresolved material uncertainty or changes requiring human authority. Preserve source identifiers and semantics. Report missing or conflicting specifications without guessing.

All source and artifact paths in the register are relative to this directory. Agents must not modify `docs/ground-truth/` or `docs/sources/`. The harness must enforce protected paths and validate selective source access before enabling it.

## Engineering Standards

- [Technology Stack](engineering/tech-stack.md)
- [Coding Conventions](engineering/coding-conventions.md)
- [Design System](engineering/design-system.md)
