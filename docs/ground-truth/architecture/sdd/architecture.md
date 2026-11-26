# SDD — Software Architecture

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §§2.1, 2.2.1 (overview), 2.2.2 (text), pp. 10, 12.
Related standards: [Technology Stack](../../engineering/tech-stack.md).

## Architectural overview (§2.1)

The system adopts the Three-Tier architectural style. The separation of presentation, application logic and data management supports maintainability, scalability and security.

| Tier | Responsibility |
|---|---|
| Presentation Tier | User interface; Boundary objects implement communication between the system and the user. |
| Application Tier | Application logic; Entity and Control objects implement business logic. |
| Data Tier | Persistent data. |

## Technology mapping (§2.1)

| Concern | SDD decision |
|---|---|
| Web and mobile interfaces | React Native and TypeScript; React Native Web for browser access. |
| Application logic | Java and Spring; roles, capabilities, privacy, Caller-Helper matching and external integrations. |
| Non-real-time client-server operations | REST APIs. |
| Persistent data | PostgreSQL. |
| Real-time text chat and audio calls | WebRTC. |

External institutional services are simulated by components isolated behind interfaces to allow future replacement. Waiting for external resources must be asynchronous and non-blocking.

## Subsystem decomposition (§2.2.1)

The system is divided into functional subsystems to support modularity and extensibility. Each unit is responsible for a coherent set of functions and collaborates with other units.

## Architectural decomposition (§2.2.2)

Each subsystem is divided into GUI, Control and DAL. The DAL includes Service and DAO.

| Element | Responsibility |
|---|---|
| GUI | Implements the interface layer. |
| Control | Implements business logic. |
| DAL / Service | Provides persistent-data services to business logic. |
| DAL / DAO | Accesses the database. |
