# UC_GAI — Listening Request and Matching

Source: RAD v1.0.0, pp. 48–52.
Version: 1.00.000
Date: 2026-11-12

## Specification

- Description: Allows Callers to submit listening requests and the system to propose them to groups of available and eligible Helpers until one accepts. Handles rejection, non-response, unavailability and cancellation.
- Primary actor: Caller.
- Secondary actor: Helper.
- Entry condition: The Caller is authenticated, with valid parental authorization if a minor, or accesses Safe Access Path in guest mode.
- Success: The request is assigned to a Helper, pseudonymous communication begins and the Caller is notified.
- Failure: The request remains unassigned and becomes inactive following cancellation, expiration of the maximum acceptance time or prolonged Caller disconnection.
- Priority: High.
- Estimated frequency: 150/day.
- Extension points: Ep1 — Cancel request; Ep2 — Respond to request.
- Generalization of: N/A.

## Main Flow

| Step | Actor | Action |
|---|---|---|
| 1 | Caller | Selects Request listening. |
| 2 | System | Verifies that no active request exists and displays the category selection form with an optional description field. |
| 3 | Caller | Selects one or more thematic categories and optionally enters a description. |
| 4 | Caller | Confirms request submission. |
| 5 | System | Verifies that at least one category is selected, creates the request and associates it with a unique internal identifier and the Caller's age group (minor or adult). |
| 6 | System | Identifies available Helpers compatible with the selected categories. |
| 7 | System | Forwards the request to a group of Helpers and displays the waiting screen to the Caller. |
| 8 | Helper | Receives a notification containing the categories and optional description; may accept within the maximum response time. |
| 9 | System | Assigns the request to the first Helper to accept and withdraws other pending proposals. |
| 10 | System | Initiates pseudonymous chat and audio communication, notifies the Caller and generates session nicknames. Shows the Caller only the Helper's nickname; shows the Helper the Caller's nickname and whether the Caller is a minor. |

## Alternative Flow I — Caller Cancellation

| Step | Actor | Action |
|---|---|---|
| 7.1.1 | Caller | Selects Cancel request while matching is in progress. |
| 7.1.2 | System | Withdraws active proposals and confirms cancellation. If cancellation and Helper acceptance occur simultaneously, cancellation prevails; the Helper is informed that the request is unavailable. |

## Alternative Flow II — Caller Connection Loss

| Step | Actor | Action |
|---|---|---|
| 7.2.1 | System | Detects connection loss during matching. |
| 7.2.2 | System | If the Caller reconnects in time, restores the waiting screen and continues matching. |
| 7.2.3 | System | Otherwise, cancels the request and informs previously notified Helpers. Informs the Caller upon their next access. |

## Alternative Flow III — Helper Rejection

| Step | Actor | Action |
|---|---|---|
| 8.1.1 | Helper | Rejects the proposal within the response deadline. |
| 8.1.2 | System | Records rejection and withdraws the Helper's proposal. |
| 8.1.3 | System | Once all group proposals have been resolved through rejection or timeout without acceptance, checks the maximum waiting time. If expired, follows Error Flow III. |
| 8.1.4 | System | Otherwise, repeats matching, excluding previously contacted Helpers. If other Helpers are found, forwards proposals and resumes at step 7; otherwise, follows Error Flow III. |

## Alternative Flow IV — Helper Non-response

| Step | Actor | Action |
|---|---|---|
| 8.2.1 | System | If the Helper does not respond before the deadline, records non-response and withdraws the proposal. |
| 8.2.2 | System | Once all group proposals have been resolved through rejection or timeout without acceptance, checks the maximum waiting time. If expired, follows Error Flow III. |
| 8.2.3 | System | Otherwise, repeats matching, excluding previously contacted Helpers. If other Helpers are found, forwards proposals and resumes at step 7; otherwise, follows Error Flow III. |

## Error Flow I — Existing Active Request

| Step | Actor | Action |
|---|---|---|
| 2.1 | System | Detects an existing active request. |
| 2.2 | System | Does not display the form and informs the Caller of the existing request. |

## Error Flow II — No Category Selected

| Step | Actor | Action |
|---|---|---|
| 5.1 | System | Detects that no category was selected. |
| 5.2 | System | Does not create the request and prompts the Caller to select a category. |
| 5.3 | System | Resumes at step 3. |

## Error Flow III — No Available or Further Eligible Helpers

| Step | Actor | Action |
|---|---|---|
| 6.1 | System | Finds no further available and eligible Helpers or detects expiration of the Caller's maximum overall waiting time. |
| 6.2 | System | Informs the Caller that assignment is currently unavailable. Suggests retrying later, consulting informational resources and contacting qualified services. |

## Notes

- Feedback is not considered for guest Callers.
- Rejection and non-response do not automatically change Helper availability or incur penalties.
- Exclusion of previously contacted Helpers applies only to the current request.
