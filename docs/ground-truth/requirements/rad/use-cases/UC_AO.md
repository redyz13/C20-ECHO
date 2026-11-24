# UC_AO — Ordinary Access via SPID/CIE

Source: RAD v1.0.0, pp. 40–42.
Version: 1.00.000
Date: 2026-11-12

## Specification

- Description: Allows adult Callers, Helpers and Supervisors to access E.C.H.O. through SPID/CIE authentication.
- Primary actors: Adult Caller, Helper, Supervisor.
- Secondary actors: N/A.
- Entry condition: The user accesses the E.C.H.O. home page.
- Success: The user is authenticated, a session is created and role-specific functions become accessible.
- Failure: Authentication fails or the operation is cancelled.
- Priority: High.
- Estimated frequency: 300/day.
- Extension points: N/A.
- Generalization of: N/A.

## Main Flow

| Step | Actor | Action |
|---|---|---|
| 1 | System | Displays the home page and user information notice; requests completion of the age questionnaire. |
| 2 | Utente | Reads the notice and declares adulthood in the questionnaire. |
| 3 | System | Acquires the questionnaire result and redirects the user to SPID/CIE authentication. |
| 4 | Utente | Selects the authentication method and enters credentials. |
| 5 | System | Acquires Identity Provider data and confirms authentication. |
| 6 | Utente | Receives authentication confirmation. |

## Alternative Flow I — Authentication Cancellation

| Step | Actor | Action |
|---|---|---|
| 4.1 | Utente | Cancels authentication while entering credentials. |

## Error Flow I — Authentication Failure

| Step | Actor | Action |
|---|---|---|
| 5.1 | System | Receives a negative authentication result, interrupts the procedure and informs the user that authentication was unsuccessful. |

## Special Requirements

- Communication with authentication providers shall use a secure connection.
- Identity data shall be verified before access is granted.
