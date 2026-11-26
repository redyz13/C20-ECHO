# E.C.H.O. — Technology Stack

Status: approved. See the document register for version and technical validation status.
Targets: responsive web application, Android, iOS.
Authority: applicable approved project specifications. See [ground truth rules](../README.md).

## 1. Stack

| Area | Technology |
|---|---|
| Client | React Native, Expo, React Native Web, TypeScript (strict), Expo Router |
| UI components and icons | React Native Paper (MD3), Material Design Icons (filled; `@react-native-vector-icons/material-design-icons`) |
| Server state | TanStack Query |
| Client build | Node.js LTS, npm, Expo CLI |
| Backend | Java 21 LTS, Spring Boot, Spring Web MVC, Spring Security, Jakarta Bean Validation |
| Backend build | Apache Maven via Maven Wrapper |
| Persistence | PostgreSQL, Spring Data JPA, Hibernate, Flyway |
| API contracts | REST, JSON, OpenAPI |
| Application events | Spring WebSocket (application events and WebRTC signaling) |
| Session transport | WebRTC peer-to-peer: browser WebRTC API, `react-native-webrtc` on Android/iOS; ICE/STUN/TURN |
| Local infrastructure | Docker, Docker Compose |
| CI/CD and native builds | GitHub Actions, Expo EAS Build |

Use the selected stack. Do not introduce competing frameworks, package managers, ORMs, migration tools or infrastructure without an approved technology decision. Prefer existing dependencies and justify additions. Apply the approved [Design System](design-system.md) to the UI stack; verify SDD alignment and cross-platform compatibility.

## 2. Integration constraints

- Share client code across targets where feasible. Isolate platform-specific integrations; use browser WebRTC APIs on web and `react-native-webrtc` on Android/iOS behind a shared interface. Use compatible Expo development builds and native configuration plugins, not Expo Go.
- Use REST for non-real-time operations and Spring WebSocket for application events and authenticated WebRTC signaling (SDP and ICE exchange). Use WebRTC audio tracks and data channels for session audio and text; use STUN/TURN for ICE connectivity as specified in [SDD deployment](../architecture/sdd/deployment.md). The backend owns domain logic, authorization and session access; restrict signaling to authorized session participants and issue scoped, short-lived TURN credentials server-side. Do not route session content through the application backend or introduce an SFU without an approved architectural change.
- Use one versioned OpenAPI contract for REST; implement clients and server against it. Generate the TypeScript client from the contract with a pinned generator. Do not invent endpoints or edit generated clients manually. Event schemas and endpoint details belong to the architecture/API artifacts.
- Keep simulated external integrations isolated behind replaceable interfaces; external waits must be asynchronous and non-blocking.
- Preserve RAD constraints: `RNF_U_4`, `RNF_A_1`–`RNF_A_4`, `RNF_P_1`–`RNF_P_2`, `RNF_I_1`–`RNF_I_3`, `RNF_IN_1`–`RNF_IN_3`, `RNF_L_4`. See [RAD requirements](../requirements/rad/non-functional/requirements.md) and [known issues](../requirements/rad/known-issues.md).
- No video calls or audio recording (SoW). Do not persist conversation content in databases, files, logs, telemetry, caches or persistent client storage. SDD §§1.2.1 and 3.6 permit temporary content in client volatile memory only, deleted at session conclusion. Reliable data channels alone do not guarantee delivery across disconnections; validate recovery and retransmission without persistent storage. Validate peer network-address exposure against pseudonymity requirements; evaluate TURN-only ICE if necessary, with capacity and latency evidence.
- Use environment-specific configuration, synthetic test data and secret injection. Never embed credentials in clients, `EXPO_PUBLIC_*` variables or repository files.

## 3. Reproducibility and dependencies

| Source of truth | Required configuration |
|---|---|
| Client manifests | `package.json`, `package-lock.json`, pinned Node.js and npm versions |
| Expo configuration | Compatible Expo SDK, React, React Native and React Native Web versions; native plugin configuration |
| Backend manifests | `pom.xml`, Java 21 target, Spring Boot dependency management, committed Maven Wrapper and `.mvn/wrapper/maven-wrapper.properties` |
| Infrastructure | Versioned Dockerfiles and Compose configuration; pinned image versions, preferably immutable digests |
| Native builds | Versioned `eas.json` and Expo app configuration; pinned EAS CLI |

At bootstrap, select mutually compatible supported releases and commit the concrete versions in these files. Use the Expo compatibility matrix and Spring Boot dependency management; avoid floating `latest` tags, Maven snapshots and unbounded dependency upgrades. Commit dependency and lockfile changes together. CI and local development must use the same toolchain baseline. Upgrade dependencies through explicit, validated changes; do not change versions merely to bypass failing tests.

## 4. Database lifecycle

- Flyway is the sole schema migration mechanism. Use versioned SQL migrations and `spring.jpa.hibernate.ddl-auto=validate`.
- Never rewrite migrations already merged or applied to shared environments. Add forward migrations instead. Allocate unique ordered versions; reconcile pending migration collisions before merge.
- Validate migration history and run migrations on disposable PostgreSQL instances in CI. Check both fresh installation and upgrade from the previous merged schema when schema changes. Do not substitute H2 for PostgreSQL integration tests.
- Do not use automatic schema update, Flyway `clean` or `repair` to conceal failures or alter shared environments.

## 5. CI integration contract

Configure the following checks at bootstrap. Keep local and CI entry points identical. Commands run from the corresponding application or infrastructure directory.

| Check | Target entry point |
|---|---|
| Client dependencies | `npm ci` |
| Static analysis | `npm run lint`, `npm run typecheck` |
| Client formatting | `npm run format:check` |
| Client tests | `npm run test:ci` |
| Web build | `npm run build:web` (Expo web export) |
| Expo compatibility | `npm run check:expo` (pinned Expo Doctor) |
| Backend build and tests | `./mvnw -B clean verify` |
| REST contract | Validate OpenAPI, regenerate client and detect drift |
| Database | Flyway validation, migration and PostgreSQL integration tests |
| Infrastructure | `docker compose config --quiet` |
| Native builds | EAS Android/iOS development or preview build profiles |

Run affected static, build, contract and test checks on PRs; include dependent components when shared contracts change. Revalidate the merge candidate against the current target branch. Native integration, browser E2E and load checks use dedicated jobs as appropriate; do not claim platform or capacity acceptance from unit tests alone.

- Run checks non-interactively in isolated environments. Emit actionable diagnostics and machine-readable test reports (e.g. JUnit XML); distinguish formatting, lint/type/compile, test assertion, infrastructure and policy failures. Missing or incomplete evidence is not a passing test.
- Keep application code, implementation tests, independent tests and protected configuration distinguishable by scope. Preserve the specification revision, approved plan and tested commit in validation evidence. Revalidate affected evidence after changes.
- Keep check commands and project-specific configuration reusable by CI and the existing agent roles. Do not require new agents for mechanical checks. Support the existing implementation and test repair paths without relaxing independent testing or audit.
- Never weaken checks, alter protected specifications or skip failing tests to obtain a passing build. Workflow routing, permissions, retry limits, repair policy and deployment gates belong to the pipeline configuration; coding rules belong to `coding-conventions.md`.

## 6. Integration and validation requirements

- Follow the SDD topology. Implementation package layout and authentication protocol must follow applicable approved specifications.
- Pin compatible dependency and runtime versions during bootstrap, including React Native Paper and its icon integration. Verify font and icon loading on all targets.
- Validate cross-platform WebRTC audio/text, microphone permissions, signaling authorization, ICE/TURN connectivity, network-address privacy, session recovery and escalation continuity on web, Android and iOS. A technology selection does not establish compliance with the 500-session target; measure signaling and TURN capacity under representative relay ratios.
- Select testing tools in accordance with TP/TCS and validate the required test coverage, including representative WebRTC/STUN/TURN load tests.
- Establish the deployment environment, signing credentials and release configuration before enabling deployment jobs.

## References

- Project: RAD v1.0.0, §3.3; SDD v1.0.0, §§1.2.1, 2.1, 2.3–2.3.1, 3.6; SoW.
- [Expo SDK compatibility](https://docs.expo.dev/versions/latest/), [WebRTC peer connections](https://webrtc.org/getting-started/peer-connections), [React Native WebRTC](https://github.com/react-native-webrtc/react-native-webrtc), [Expo WebRTC configuration](https://github.com/expo/config-plugins/tree/main/packages/react-native-webrtc), [WebRTC data channels](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Using_data_channels).
- [React Native Paper setup](https://oss.callstack.com/react-native-paper/docs/guides/getting-started), [Paper icons](https://oss.callstack.com/react-native-paper/docs/guides/icons).
- [Spring Boot database initialization](https://docs.spring.io/spring-boot/how-to/data-initialization.html), [Maven Wrapper](https://maven.apache.org/tools/wrapper/), [Flyway validation](https://documentation.red-gate.com/flyway/reference/commands/validate).
- [GitHub Actions Node.js](https://docs.github.com/en/actions/tutorials/build-and-test-code/nodejs), [EAS builds from CI](https://docs.expo.dev/build/building-on-ci/).
