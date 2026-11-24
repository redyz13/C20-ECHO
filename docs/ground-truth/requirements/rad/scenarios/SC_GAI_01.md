# SC_GAI_01 — Helper Rejection, Non-response or Unavailability

Source: RAD v1.0.0, § 3.4.1.2, pp. 30–31.
Actors: Caller, Helper A, Helper B, Helper C.

| Step | Actor | System |
|---|---|---|
| 1 | A 24-year-old Caller submits a listening request under the "Loneliness" category and waits. | Validates the request, identifies available and compatible Helpers, and sends assignment proposals to Helpers A and B. Displays a waiting indicator and cancellation option. |
| 2 | Helper A receives the notification and rejects the proposal. | Records the rejection and withdraws the proposal to Helper A. |
| 3 | Helper B receives the notification but does not open it or respond before the deadline. | Records the non-response and withdraws the proposal and any remaining pending proposals in the group. |
| 4 | The Caller continues waiting. | Repeats matching, excluding Helpers already contacted for the current request. Identifies Helper C as available and eligible, then sends the proposal. |
| 5 | Helper C does not respond before the deadline. | Withdraws the proposal and records the non-response. |
| 6 | The Caller continues waiting. | Repeats matching. No other available and eligible Helpers are found. Stops searching, informs the Caller and presents alternatives: retry later, consult informational resources or contact qualified services. |
| 7 | The Caller decides to retry later and selects "Return to home". | Closes the request screen and returns the Caller to the home page. |
