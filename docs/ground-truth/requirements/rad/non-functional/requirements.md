# Non-functional Requirements

Source: RAD v1.0.0, § 3.3, pp. 23–25.

## Usability (RNF_U)

| ID | Description | Priority |
|---|---|---|
| RNF_U_1 | The readability index shall exceed 80, as measured using GULPEASE. | Medium |
| RNF_U_2 | The escalation button shall remain visible on every session screen without scrolling. | High |
| RNF_U_3 | The following core functions shall be accessible within three interactions from the initial post-authentication screen: help request submission (Caller), acceptance or rejection of an assignment proposal (Helper). | High |
| RNF_U_4 | The system shall be responsive. All functions shall be usable on devices with different screen widths, without horizontal scrolling, on the latest two versions of Chrome and Firefox. | High |

## Reliability (RNF_A)

| ID | Description | Priority |
|---|---|---|
| RNF_A_1 | Under stable conditions, an escalation request shall be recorded and visible to the Supervisor within 30 seconds of activation by the Helper. | Medium |
| RNF_A_2 | An interrupted session shall be restored within 20 seconds of connection recovery, without losing previously sent messages. | Medium |
| RNF_A_3 | Under stable conditions, the system shall maintain the communication channel (chat/audio) between Helper and Caller throughout the escalation process. | High |
| RNF_A_4 | The system shall ensure data persistence through a database without retaining communication content in any form. | High |

## Performance (RNF_P)

| ID | Description | Priority |
|---|---|---|
| RNF_P_1 | The system shall operate asynchronously and without blocking while awaiting a response from an external resource. | High |
| RNF_P_2 | The system shall support at least 500 concurrent active sessions. | Medium |

## Supportability (RNF_S)

| ID | Description | Priority |
|---|---|---|
| RNF_S_1 | Upon account deletion, the application shall enforce a policy for deleting data not required for statistical purposes. | Medium |

## Implementation (RNF_I)

| ID | Description | Priority |
|---|---|---|
| RNF_I_1 | External service integrations (SPID/CIE, geolocation) shall use mock components isolated behind interfaces, allowing replacement without modifying the rest of the system. | High |
| RNF_I_2 | Real-time audio interactions between Helper and Caller shall use WebRTC-based communication protocols. | High |
| RNF_I_3 | Frontend-backend communication for non-real-time application operations shall use REST APIs. | High |

## Interfaces (RNF_IN)

| ID | Description | Priority |
|---|---|---|
| RNF_IN_1 | The platform shall provide interfaces for communication with external digital identity systems (simulated SPID/CIE). | High |
| RNF_IN_2 | The platform shall provide interfaces for simulated verification of Helper affiliation with partner organizations and associated qualifications. | High |
| RNF_IN_3 | The platform shall provide an interface to simulated emergency services for case handover. | High |

## Operations (RNF_O)

| ID | Description | Priority |
|---|---|---|
| RNF_O_1 | The system shall automatically and securely record each escalation procedure in the audit logs 10 seconds after its completion, storing the date/time, actors involved and final outcome. | High |

## Packaging (RNF_PA)

| ID | Description | Priority |
|---|---|---|
| RNF_PA_1 | The system shall include written documentation (user manual) covering its main operational functions. | High |

## Legal (RNF_L)

| ID | Description | Priority |
|---|---|---|
| RNF_L_1 | The system shall manage personal data retention and deletion according to the periods and conditions established by applicable legislation. | High |
| RNF_L_2 | The system shall log access to and operations on personal data requiring traceability, restricting log access to authorized parties. | High |
| RNF_L_3 | The system shall provide users with clear and understandable information on the nature of the service, its use and personal data processing, requesting consent where necessary. | High |
| RNF_L_4 | The system shall ensure pseudonymous interactions. Each actor shall know only strictly necessary information, and data shall be handled with the utmost confidentiality. | High |