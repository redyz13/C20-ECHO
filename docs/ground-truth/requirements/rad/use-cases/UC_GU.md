# UC_GU — Helper Qualification Management

Source: RAD v1.0.0, pp. 46–48.
Version: 1.00.000
Date: 2026-11-14

## Specification

- Description: Allows Supervisors to assign, update or verify Helper qualifications.
- Primary actor: Supervisor.
- Secondary actor: Helper.
- Entry condition: The Supervisor is authenticated and accesses their restricted area.
- Success: Helper qualifications are validated and/or updated; the Helper is notified of changes.
- Failure: Validation or update fails, qualifications remain unchanged, the Supervisor receives an error message and the Helper is notified of the unsuccessful operation.
- Priority: High.
- Estimated frequency: 50/day.
- Extension points: N/A.

## Main Flow

| Step | Actor | Action |
|---|---|---|
| 1 | Supervisor | Opens Helper Management from their restricted area. |
| 2 | System | Retrieves and displays all registered Helpers. |
| 3 | Supervisor | Selects the Helper whose profile is to be examined. |
| 4 | System | Retrieves and displays the Helper's personal data and qualifications. |
| 5 | Supervisor | Initiates verification of a specific qualification. |
| 6 | System | Queries the partner organization's interface to verify affiliation and completion of the required training. |
| 7 | System | Receives a positive result, confirms qualification validity and displays confirmation. |
| 8 | Supervisor | Reviews the result and selects Return to list. |
| 9 | System | Closes the profile details and returns to the registered Helper list. |

## Alternative Flow — Manual Qualification Assignment or Update

| Step | Actor | Action |
|---|---|---|
| 4.1 | Supervisor | Selects Edit qualifications instead of initiating external verification. |
| 4.2 | System | Displays the configurable qualifications. |
| 4.3 | Supervisor | Selects or deselects qualifications according to the training documentation received and confirms the changes. |
| 4.4 | System | Validates the operation, stores the updated qualifications in the database, associates them with the Helper profile, notifies the Helper and confirms the update to the Supervisor. Resumes at step 8. |

## Error Flow — Certification Not Verified by Partner Organization

| Step | Actor | Action |
|---|---|---|
| 6.1 | System | Receives a negative result indicating incomplete training or an unrecognized qualification. |
| 6.2 | System | Keeps the qualification inactive and notifies the Helper of ineligibility. Terminates or resumes at step 4. |

## Error Flow — Partner Organization Interface Failure

| Step | Actor | Action |
|---|---|---|
| 6.3 | System | Detects a timeout or communication error involving the external partner service. |
| 6.4 | System | Interrupts verification, informs the Supervisor of the technical error and suggests retrying later. Resumes at step 4. |
