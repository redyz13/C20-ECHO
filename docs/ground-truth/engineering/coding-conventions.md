# E.C.H.O. — Coding Conventions

Status: proposed engineering baseline; automated enforcement pending bootstrap.
Scope: application code, tests and build configuration across all targets.
Read [Technology Stack](tech-stack.md) and the task-relevant ground truth first. SDD/DPD define architecture; TP/TCS define acceptance and test obligations. Agents must not modify ground truth or bypass governance. Escalate only material unresolved conflicts.

## 1. General rules

- Use English for code identifiers, technical comments and test names. Preserve approved domain terms, requirement IDs, API contracts and UI text; do not rename externally defined identifiers for stylistic consistency.
- Keep changes within the assigned task. Reuse existing components and domain logic; avoid unrelated refactoring, speculative abstractions and duplicate implementations.
- Follow the approved module boundaries. Keep domain rules independent of transport and UI code. Do not introduce new architectural layers or dependencies without a concrete need and an authorized decision where required by the technology baseline.
- Prefer explicit types, immutable values where appropriate, descriptive names and cohesive functions. Comment non-obvious constraints and decisions, not obvious code. Remove unused code introduced by the task.
- Use UTF-8, LF line endings and a final newline in text source files. Respect the formatter; do not manually align code or reformat unrelated files.

## 2. Java / Spring Boot

| Element | Convention |
|---|---|
| Types | PascalCase |
| Methods, fields, parameters | camelCase |
| Constants | UPPER_SNAKE_CASE |
| Packages | lowercase |
| Source files | Match public top-level type name |
| Formatting | google-java-format via Spotless |

- Use constructor injection for required dependencies; avoid field injection.
- Keep REST controllers focused on transport, validation and delegation. Enforce domain rules and authorization server-side. Use explicit API DTOs rather than exposing persistence entities.
- Validate external input at boundaries. Use specific exceptions and consistent HTTP errors according to the API contract; never expose internal stack traces.
- Define transaction boundaries around atomic domain operations. Account for concurrent matching and escalation transitions; do not rely on client-side checks or process-local locks as proof of cross-instance consistency.
- Use parameterized queries and appropriate persistence constraints. Avoid blocking external operations inside critical transactions.
- Use injected time sources for time-dependent domain rules where practical; use explicit time zones and contract-defined timestamp formats.

## 3. TypeScript / React Native

| Element | Convention |
|---|---|
| Components and types | PascalCase |
| Functions, variables and hooks | camelCase; hooks start with use |
| Constants | UPPER_SNAKE_CASE for module-level constant values where appropriate |
| Files | PascalCase for component modules, camelCase for other code; Expo Router conventions take precedence for routes |
| Formatting | Prettier |

- Keep TypeScript strict enabled. Do not bypass type errors with `any`, `@ts-ignore` or unchecked assertions. Use `unknown` and narrowing for untrusted data. Generated code follows its generator contract.
- Handle asynchronous operations explicitly; handle rejection, cancellation or stale results where relevant. Keep React hooks unconditional and dependencies correct.
- Use TanStack Query for server state; keep local UI state local. Do not duplicate authoritative server state in independent global stores.
- Reuse shared components and design tokens once [Design System](design-system.md) is available. Preserve accessible labels, focus, loading, error and empty states as applicable. Do not use color alone for critical status.
- Isolate platform-specific code and permissions. Clean up subscriptions, timers, audio resources and connections when their lifecycle ends. Use generated REST clients; do not hand-edit generated output.

## 4. Privacy and reliability

- Apply RAD `RNF_A_4` and `RNF_L_4`: never retain communication content or expose unnecessary personal data. Exclude conversation content, credentials and tokens from logs, telemetry, errors, test artifacts and persistent client state. Keep required escalation audit metadata separate (`RNF_O_1`).
- Use structured, sanitized diagnostic logging and synthetic test data. Use only approved secret injection and configuration mechanisms; no credentials in source or client bundles.
- Enforce permissions and state transitions at the authoritative backend. Treat duplicate, late and out-of-order events explicitly where relevant; use bounded retries and timeouts consistent with the specifications. Never invent timing or retention policies to resolve a missing requirement.

## 5. Tests and migrations

- Test externally observable behavior against relevant requirements and contracts. Include applicable negative, permission, timeout and concurrency cases; use deterministic fixtures and controlled clocks rather than arbitrary sleeps.
- Keep tests independent and repeatable. Mock external boundaries when appropriate; use PostgreSQL for persistence integration tests as specified in the technology stack. Follow TP/TCS once available.
- Fix failing behavior, not the evidence of failure. Do not delete, weaken, skip or replace tests to make CI pass. Preserve independent test derivation from approved specifications; only the authorized test path may change independent acceptance tests. Apply the pipeline audit and retest policy to test repairs.
- Follow the Flyway migration rules in [Technology Stack](tech-stack.md). Do not modify merged migrations or change migration ordering to conceal failures.

## 6. Automated enforcement

Configure these tools at bootstrap using pinned, compatible versions. Configuration files are the executable source of truth for mechanical rules. Do not duplicate rule lists in agent prompts.

| Scope | Tool / configuration | Check entry point |
|---|---|---|
| Client code quality | Expo ESLint flat config; compatible typescript-eslint rules | `npm run lint` |
| Client types | strict `tsconfig.json` | `npm run typecheck` |
| Client formatting | Prettier; `eslint-config-prettier` | `npm run format:check` |
| Backend formatting | Maven Spotless with google-java-format | `./mvnw -B clean verify` |
| Backend compile and tests | Maven lifecycle | `./mvnw -B clean verify` |

- Configure ESLint for React/Expo, unused code and selected type-aware safety rules (e.g. unsafe types and unhandled promises); fail on violations of the enabled baseline. Keep formatting out of lint rules. Exclude generated code, build artifacts and protected specifications from formatting targets; define generated-code checks separately.
- Define `npm run format` for local Prettier writes and `npm run format:check` for read-only checks. Use `./mvnw spotless:apply` for local Java formatting; bind `spotless:check` to Maven `verify`. Apply formatters before validation, limited to changed files within the actor's authorized scope. Do not reformat independent tests from an implementation repair or modify protected files. Use only configured, scope-safe lint autofixes; verify their diff and rerun checks.
- Evaluate SpotBugs as a separate report-only check initially. Promote its calibrated high-confidence findings to a merge gate only after confirming useful diagnostics and acceptable runtime. Avoid redundant style tools and arbitrary coverage/complexity gates.
- Keep local and CI checks identical. Run validation without rewriting tracked source in CI; emit actionable diagnostics and nonzero exit codes for failures. Reuse the commands and evidence requirements in [Technology Stack](tech-stack.md).
- Establish a clean baseline and verify that representative deliberate violations fail each new check before marking it required. Protect workflow, agent, test-policy and quality-check configuration against unauthorized changes. Do not alter scripts, exclusions, rules, thresholds or dependencies to silence a failure. Narrow, justified exceptions must follow the relevant policy; fix the underlying defect whenever possible.
- Use deterministic formatting and safe autofixes within the existing authorized write paths; no additional agent or review is required solely for formatting. Formatting or lint failure alone is not evidence of `TEST_DEFECT` or a functional defect. Route non-mechanical failures through the existing repair policy; do not alter independent tests via implementation repair. Rerun affected checks on the resulting commit and obtain any fresh evidence required by policy. Escalate only unresolved material ambiguity or changes requiring human authority. The pipeline defines routing and authorization; these conventions do not change them.

## References

- Project: RAD v1.0.0, SoW, [Technology Stack](tech-stack.md).
- [Expo ESLint and Prettier](https://docs.expo.dev/guides/using-eslint/), [typescript-eslint typed linting](https://typescript-eslint.io/getting-started/typed-linting/), [Prettier integration](https://prettier.io/docs/integrating-with-linters).
- [Google Java Style](https://google.github.io/styleguide/javaguide.html), [Spotless Maven](https://github.com/diffplug/spotless/tree/main/plugin-maven), [SpotBugs Maven](https://spotbugs.github.io/spotbugs-maven-plugin/).
- [OWASP Logging Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html), [GitHub Copilot custom instructions](https://docs.github.com/en/copilot/concepts/prompting-and-context/custom-instructions).
