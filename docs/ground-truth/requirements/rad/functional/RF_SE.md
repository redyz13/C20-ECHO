# Safe Escalation Management (RF_SE)

Source: RAD v1.0.0, § 3.2.5, pp. 20–22.

| ID | Name | Description | Actors | Priority |
|---|---|---|---|---|
| RF_SE_1 | Safe Escalation Activation | The system shall provide a quick command allowing Helpers to request immediate intervention from an E.C.H.O. Supervisor in risky situations or circumstances beyond the Helper's competence. | Helper | High |
| RF_SE_2 | Handover to Professional Services | The system shall allow the Supervisor to transfer responsibility for the case to professional services or emergency facilities. | Supervisor | High |
| RF_SE_3 | Sensitive Data Sharing | The system shall grant access to the Caller's sensitive data exclusively to professionals from external services involved in the Safe Escalation procedure, restricting disclosure to information strictly necessary for taking responsibility for the case. | Supervisor | High |
| RF_SE_4 | Supervisor Assignment | The system shall automatically assign the Safe Escalation request to the first available Supervisor, without allowing rejection. The Supervisor shall confirm acceptance within a predefined time interval. If confirmation is not received within that interval, the system shall automatically reassign the request to the next available Supervisor. | Supervisor | High |
| RF_SE_5 | Fallback Management | When no Supervisor is available, the system shall inform the Helper through a non-blocking notification, allowing continued management of the situation. Depending on the assessed urgency, the Helper shall be able to activate emergency services or maintain the listening channel with the Caller and, if necessary, direct them to qualified services. | Helper | High |
| RF_SE_6 | Fallback Reporting | At the end of the fallback intervention, the system shall require the Helper to complete a report specifying the actions taken and the reasons for the decisions made. Recorded information shall be retained and accessible exclusively to authorized Supervisors. | Helper, Supervisor | High |