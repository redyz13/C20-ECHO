# SDD — Design Goals and Trade-Offs

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §§1.2–1.2.1, pp. 6–8.
Origin requirements: [RAD non-functional requirements](../../requirements/rad/non-functional/requirements.md).

## Design Goals

| Rank | ID | Source title | Description | Category | Origin RNFs |
|---|---|---|---|---|---|
| 1 | DG_1 | Safe Escalation | When the Caller or other people are at risk, the escalation request must be registered and visible to the Supervisor within 30 seconds under stable conditions. If no Supervisor is available, Fallback is activated. Contact between Helper and Caller must be maintained under stable conditions throughout the escalation procedure. | Dependability | RNF_A_1, RNF_A_3 |
| 2 | DG_2 | Sicurezza e pseudonimato | Each actor knows only strictly necessary information. Interactions use system-generated nicknames. Communication content is not retained in any form, and personal data is minimized. | Dependability | RNF_A_4, RNF_L_4 |
| 3 | DG_3 | Tracciabilità | Escalations and personal-data operations requiring traceability are recorded and accessible only to authorized parties. | Dependability | RNF_L_2, RNF_O_1 |
| 4 | DG_4 | Usabilità | The escalation button must always be visible on every session screen without scrolling. Main functions must be reachable within three interactions from the initial post-authentication screen. | End User | RNF_U_2, RNF_U_3 |
| 5 | DG_5 | Modificabilità e testabilità | Integrations with simulated external services (SPID/CIE, partner organizations, emergency services) must use interfaces and replaceable mock components without requiring changes to the rest of the system. | Maintenance | RNF_I_1, RNF_IN_1, RNF_IN_2, RNF_IN_3 |
| 6 | DG_6 | Fruibilità multi-dispositivo | The system must be usable on devices with different screen widths, without horizontal scrolling, on the latest two versions of Chrome and Firefox. | End User | RNF_U_4 |
| 7 | DG_7 | Ripristino della sessione | Interrupted sessions must be restored within 20 seconds after connectivity returns, without loss of previously sent messages and in compliance with confidentiality and non-retention constraints. | Dependability | RNF_A_2, RNF_A_4 |
| 8 | DG_8 | Documentazione | The system must include a user manual covering its main operational functions. | End User | RNF_PA_1 |

## Trade-Offs

| Source title | Accepted trade-off |
|---|---|
| Riservatezza vs Tracciabilità | To ensure traceability of Safe Escalation operations, some activity information is retained. Audit logs are limited to date, time, actors and operation outcome; communication content is excluded. |
| Riservatezza vs Tutela del Caller | To manage Safe Escalation effectively, necessary Caller personal information may need to be transmitted to emergency services. Only information that is available and strictly necessary for emergency management may be transmitted. |
| Ripristino delle sessioni vs Riservatezza | To restore sessions without message loss, content is temporarily kept in volatile memory on users' devices, without persistent storage. Content is deleted at the end of the session in compliance with confidentiality requirements. |
| Accessibilità del Safe Access Path vs Prevenzione degli abusi | Access without parental authorization must remain simple and have few obstacles. Proportionate abuse-prevention controls limit misuse without compromising ease of access for minors who genuinely need it. |
