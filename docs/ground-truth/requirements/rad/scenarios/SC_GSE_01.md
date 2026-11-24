# SC_GSE_01 — Safe Escalation Activation and Management

Source: RAD v1.0.0, § 3.4.1.4, pp. 36–37.
Actors: Helper, Caller, Supervisor.

| Step | Actor | System |
|---|---|---|
| 1 | During a text listening session, a 22-year-old Caller expresses self-harm intentions and reports imminent danger. The Helper recognizes that the situation exceeds their competence and selects "Safe Escalation". | Registers the escalation and automatically assigns it to the first available Supervisor. Maintains a stable chat channel between Helper and Caller. |
| 2 | The Supervisor receives the notification and confirms responsibility for the escalation, assisting the Helper. | Associates the Supervisor with the ongoing escalation without altering the chat state. |
| 3 | The Supervisor assesses the situation and decides to transfer responsibility to emergency services. | Sends only available, transferable and strictly necessary information through the emergency service interface. |
| 4 | The Helper maintains contact and reassures the Caller until emergency services take responsibility. The Supervisor then confirms closure. | Notifies the completed handover, closes the escalation and automatically records the event securely in the audit logs 10 seconds after closure. |
