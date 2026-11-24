# UC_GSE — Safe Escalation Management

Source: RAD v1.0.0, pp. 56–59.
Version: 1.00.000
Date: 2026-11-12

## Specification

- Description: Allows Helpers to trigger Safe Escalation during imminent danger. The automatically assigned Supervisor, or the Helper under fallback, manages the situation through selective data transfer to emergency services or internal resolution and guidance.
- Primary actors: Helper, Supervisor.
- Secondary actors: Caller, External emergency services.
- Entry condition: An active listening session exists and the Helper identifies an emergency or imminent danger to the Caller's safety.
- Success: Escalation concludes through selective data transfer or internal resolution and guidance, with mandatory fallback reporting where applicable. The event is securely recorded in audit logs.
- Failure: Data transfer to emergency services fails. The Supervisor is promptly notified while the Helper–Caller communication channel remains active.
- Priority: High.
- Estimated frequency: 15/day.
- Extension points: N/A.
- Generalization of: N/A.

## Main Flow

| Step | Actor | Action |
|---|---|---|
| 1 | Helper | Selects the visible Safe Escalation emergency button during the session. |
| 2 | System | Registers activation, automatically assigns the request to the first available Supervisor without a rejection option and maintains a stable Helper–Caller communication channel. |
| 3 | Supervisor | Views the assigned alert and confirms responsibility within the predefined time interval. |
| 4 | System | Associates the Supervisor with the escalation and enables emergency management tools without altering the Helper–Caller session. |
| 5 | Helper | Maintains verbal or textual contact with the Caller, providing reassurance while coordinating with the Supervisor. |
| 6 | Supervisor | Assesses severity, establishes imminent danger and initiates transfer to emergency services. |
| 7 | System | Selectively decrypts available, transferable and strictly necessary information and forwards it through the emergency services interface. |
| 8 | Supervisor | Receives handover confirmation from emergency services and closes Safe Escalation. |
| 9 | System | Concludes escalation, archives the assignment in the Supervisor interface and automatically records the event in audit logs 10 seconds after closure, including timestamp, actors and outcome, but no conversation content. |

## Alternative Flow I — Fallback and Reporting without Available Supervisors

| Step | Actor | Action |
|---|---|---|
| 2.1 | System | Detects Supervisor unavailability, activates fallback and displays a non-blocking notice reminding the Helper of responsibilities and subsequent reporting obligations. Maintains contact with the Caller. |
| 2.2 | Helper | Assesses urgency and decides whether to contact emergency services directly in case of imminent danger or continue listening and guide the Caller towards qualified professional services. |
| 2.3 | System | If emergency services are directly activated, selectively decrypts strictly necessary personal details and transfers them through the dedicated interface. At the end of the intervention, requests mandatory fallback reporting. |
| 2.4 | Helper | Completes the report, describing actions taken and justifying decisions. |
| 2.5 | System | Records the report, makes it accessible to authorized Supervisors for subsequent review and records the event in audit logs within 10 seconds of closure, excluding conversation content. |

## Alternative Flow II — Reassignment after Supervisor Non-response

| Step | Actor | Action |
|---|---|---|
| 3.1 | System | Detects failure to confirm responsibility within the predefined interval and automatically reassigns the request to the next available Supervisor. Activates fallback if no further Supervisors are available or non-response persists. |

## Alternative Flow III — Internal Resolution without External Handover

| Step | Actor | Action |
|---|---|---|
| 6.1 | Supervisor | Determines that the situation is under control and no imminent threat to life remains. Closes escalation without transferring responsibility to external emergency services. |
| 6.2 | System | Receives the closure command, archives the assignment in the Supervisor interface and restores normal session management. |
| 6.3 | Helper | Continues listening until normal conversation termination. The system records the escalation outcome in audit logs within 10 seconds of escalation closure, excluding messages. |

## Error Flow I — Emergency Services Interface Failure

| Step | Actor | Action |
|---|---|---|
| 7.1 | System | Detects transmission failure or interface unavailability, interrupts transmission and notifies the Supervisor or fallback Helper. Maintains the Helper–Caller communication channel. Handover is not considered complete; escalation remains open until another transmission attempt or confirmation of responsibility by external emergency services. |

## Special Requirements

- Assignment to the first available Supervisor shall be automatic, without a rejection option, with automatic reassignment after the confirmation deadline.
- Supervisor unavailability shall activate fallback with a non-blocking notice and mandatory subsequent reporting.
- Sensitive Caller data transferred to emergency services shall be limited to strictly necessary information.
- Audit logging shall occur 10 seconds after closure without retaining conversation content.
