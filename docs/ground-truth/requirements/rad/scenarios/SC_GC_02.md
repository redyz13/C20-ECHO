# SC_GC_02 — Session Termination and Mandatory Feedback

Source: RAD v1.0.0, § 3.4.1.3, pp. 35–36.
Actors: Caller, Helper.

| Step | Actor | System |
|---|---|---|
| 1 | A 26-year-old Caller has been discussing work-related difficulties with the Helper over audio for approximately 30 minutes. Both agree to end the conversation. The Caller selects "End session". | Requests confirmation. |
| 2 | Confirms termination. | Closes the audio channel and session, notifies the Helper and displays the mandatory feedback form. |
| 3 | Attempts to return to the home page without completing feedback. | Prevents navigation and informs the Caller that feedback is mandatory to conclude the session. |
| 4 | Completes the feedback form without reporting any issues. | Enables feedback submission. |
| 5 | Submits feedback. | Validates completeness, records feedback anonymously, makes it available to the matching algorithm for future requests and sets the request to [terminata]. |
| 6 | Receives confirmation and selects "Return to home". | Closes the form and returns the Caller to the home page. |
