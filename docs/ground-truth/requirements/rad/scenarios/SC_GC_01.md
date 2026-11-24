# SC_GC_01 — Unagreed Disconnection Reports and Supervisor Alert

Source: RAD v1.0.0, § 3.4.1.3, pp. 33–34.
Actors: Caller, Helper, Supervisor.

| Step | Actor | System |
|---|---|---|
| 1 | A 19-year-old Caller is discussing loneliness during an audio call. The Helper leaves without notice or mutual agreement. The Caller waits. | Detects the audio interruption, informs the Caller that the Helper is disconnected and attempts session recovery without recording or retaining call content. |
| 2 | The Caller waits, but the Helper does not reconnect within 20 seconds. | Terminates the session, notifies the Caller and displays the mandatory feedback form, including technical issue and unagreed interruption reporting options. |
| 3 | The Caller rates the session, selects "Intentional and unagreed interruption by the Helper" rather than "Technical issue", and submits feedback. | Validates completeness, records feedback and the report anonymously, and sets the request to [terminata]. Associates the report with the Helper, who already has two equivalent reports. Increments the counter, which reaches the predefined threshold, and automatically alerts Supervisors. |
| 4 | Receives confirmation and selects "Return to home". | Closes the form and returns the Caller to the home page. |
| 5 | The Supervisor opens the alert from the dashboard. | Displays the Helper identifier, report count and report dates, without communication content or Caller identifying data. |
| 6 | The Supervisor takes responsibility for the alert and decides to contact the Helper outside the platform to investigate and provide guidance. | Records the assignment, sets the alert to [preso in carico] and retains the Helper's report history. |
