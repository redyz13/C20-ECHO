# SC_GSE_02 — Safe Escalation Management without External Handover

Source: RAD v1.0.0, § 3.4.1.4, pp. 37–38.
Actors: Helper, Caller, Supervisor.

| Step | Actor | System |
|---|---|---|
| 1 | During a listening session, the Caller expresses confused thoughts and severe distress. Concerned about the Caller's safety, the Helper activates Safe Escalation. | Registers the escalation and automatically assigns it to the first available Supervisor. Maintains a stable communication channel between Helper and Caller. |
| 2 | The Supervisor receives the notification and confirms responsibility, assisting the Helper. | Associates the Supervisor with the ongoing escalation without interrupting or altering the communication channel. |
| 3 | After consulting the Helper, the Supervisor determines that the Caller is calming down and no imminent danger remains. Closes the escalation without transferring responsibility to emergency services. | Receives the closure command, archives the escalation in the Supervisor interface and restores the session to its normal management state. |
| 4 | The Helper continues listening, provides informational resources or non-urgent support contacts if necessary, and ends the session normally. | Closes the listening session and automatically records the escalation securely in the audit logs 10 seconds after escalation closure. |
