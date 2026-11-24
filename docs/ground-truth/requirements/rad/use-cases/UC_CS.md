# UC_CS — Session Termination and Feedback

Source: RAD v1.0.0, pp. 52–55.
Version: 1.00.000
Date: 2026-11-12

## Specification

- Description: Allows the Caller or Helper to terminate an active text or audio session. Requires anonymous Caller feedback, including optional reports of technical issues or intentional, unagreed interruptions by the Helper. Supervisors are notified when the predefined disconnection report threshold is reached.
- Primary actors: Caller, Helper.
- Secondary actor: Supervisor.
- Entry condition: An active listening session exists between the Caller and assigned Helper.
- Success: The session is closed, anonymous feedback and any report are recorded, the request is [terminata] and the Caller returns to the main screen.
- Failure: The session is closed but feedback cannot be recorded. The Caller is informed and may retry; the request remains [in attesa di feedback].
- Priority: High.
- Estimated frequency: 150/day.
- Extension points: N/A.
- Generalization of: N/A.

## Main Flow

| Step | Actor | Action |
|---|---|---|
| 1 | Caller | Selects End session. |
| 2 | System | Requests confirmation. |
| 3 | Caller | Confirms termination. |
| 4 | System | Closes communication and the session, sets the request to [in attesa di feedback], notifies the Helper and displays the mandatory feedback form to the Caller. |
| 5 | Caller | Selects a rating representing perceived affinity and rapport during the listening session. |
| 6 | Caller | Submits feedback without reporting issues. |
| 7 | System | Validates completeness, records anonymous feedback, makes it available to the matching algorithm, sets the request to [terminata] and retains no communication content. |
| 8 | System | Confirms feedback receipt and returns the Caller to the main screen. |

## Alternative Flow I — Termination by Helper

| Step | Actor | Action |
|---|---|---|
| 1.1 | Helper | Selects End session and confirms termination. |
| 1.2 | System | Resumes at step 4, notifying the Caller instead of the Helper. |

## Alternative Flow II — Caller Cancels Termination

| Step | Actor | Action |
|---|---|---|
| 3.1 | Caller | Cancels termination confirmation. |
| 3.2 | System | Keeps the session active and terminates the use case. |

## Alternative Flow III — Unintentional Communication Interruption

| Step | Actor | Action |
|---|---|---|
| 1.3 | System | Detects interruption, informs the connected participant and attempts session recovery. |
| 1.4 | System | If connectivity returns before the closure timeout expires, restores the session within 20 seconds of connection recovery without losing previously sent messages. Terminates the use case without closing the session. |
| 1.5 | System | When disconnection-related closure attempts expire, proceeds according to the disconnected user and resumes at step 4. |

## Alternative Flow IV — Technical Issue or Unagreed Interruption Report

| Step | Actor | Action |
|---|---|---|
| 6.1 | Caller | Selects Technical issue or Intentional and unagreed interruption by the Helper and submits feedback. |
| 6.2 | System | Records anonymous feedback and report, associates the report with the Helper and sets the request to [terminata]. Increments the Helper's report counter only for unagreed interruptions. |
| 6.3 | System | If the counter reaches the predefined threshold, automatically alerts Supervisors with the Helper identifier and report summary, excluding conversation content and Caller identifying data. |
| 6.4 | System | Resumes at step 8. |

## Error Flow I — Missing Feedback

| Step | Actor | Action |
|---|---|---|
| 5.1 | Caller | Attempts to proceed or leave the form without selecting a rating. |
| 5.2 | System | Informs the Caller that feedback is mandatory, prevents further navigation and keeps the form displayed. Resumes at step 5. |

## Error Flow II — Feedback Recording Failure

| Step | Actor | Action |
|---|---|---|
| 7.1 | System | Cannot record feedback, displays an error and offers resubmission while preserving the entered form data. Resumes at step 6. |

## Special Requirements

- Feedback shall be anonymous.
- Audio calls shall not be recorded.
- Communication content shall not be retained in any form.
- Supervisor alerts shall contain only strictly necessary information.
