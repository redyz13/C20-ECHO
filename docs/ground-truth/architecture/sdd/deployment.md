# Hardware/Software Mapping

Source: SDD v1.0.0, §2.3–2.3.1, pp. 13–14.

## Technology mapping

| Architectural responsibility | Technology specified in SDD |
|---|---|
| Web and mobile UI | React Native, TypeScript, React Native Web |
| Application logic (access, roles, capabilities, privacy, listening requests, matching and Safe Escalation) | Java, Spring |
| Transactional persistence and referential integrity | PostgreSQL |
| Real-time communication | WebRTC, direct between user devices or through relay services when needed |

Server-side application components run on a single application node (centralized deployment). The deployment diagram represents the database, STUN/TURN infrastructure and simulated institutional services as separate devices.

## Communication

| Nodes | Protocol / mechanism |
|---|---|
| Client → Application Server | REST over HTTPS for non-real-time application operations |
| Application Server → Database Server | TCP/IP (§2.3); JDBC / JPA (diagram) |
| Client 1 ↔ Client 2 | WebRTC (Media & Data P2P) |
| Each client → STUN / TURN Infrastructure | STUN / TURN (ICE) |
| Application Server → External Institutional Services | REST / HTTPS (simulated external APIs) |

See [Deployment Diagram](diagrams/deployment.puml). The [Technology Stack](../../engineering/tech-stack.md) defines signaling and cross-platform WebRTC integration for this topology.
