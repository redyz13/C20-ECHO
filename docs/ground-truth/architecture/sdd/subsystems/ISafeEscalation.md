# Sottosistema Safe Escalation

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.8, pp. 23–24.
Provided interface: `ISafeEscalation`.

## Provided services

| Service | Description |
|---|---|
| Attivazione della Safe Escalation | Allows the Helper to request Supervisor intervention through a quick command, registering the request while keeping contact with the Caller active. |
| Assegnazione del Supervisor | Identifies the first available Supervisor and automatically assigns the request without the possibility of refusal. If confirmation is not received within the specified time, reassigns the request to the next available Supervisor. If no available Supervisor confirms taking charge, activates Fallback. |
| Passaggio ai servizi di emergenza | Allows the Supervisor to transfer responsibility to the competent simulated services and follows the outcome until they take charge. |
| Condivisione dei dati | Transmits only strictly necessary information to emergency services, together with any relevant descriptions of the Caller provided by the Helper and Supervisor. |
| Registrazione di log audit | Automatically and securely records escalations asynchronously after 10 seconds have elapsed from their conclusion, storing date, time, actors and outcome, without communication content. |
| Stato della richiesta Safe Escalation | Tracks the evolution of the Safe Escalation request. |
| Conclusione senza trasferimento esterno | Allows the Supervisor to conclude Safe Escalation without transferring responsibility to external services, returning the session to its normal management state. |

## Required services and dependencies

Source: §3.8.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Gestione Fallback Escalation (`IFallBack`)](IFallBack.md) | Activate the alternative procedure when no Supervisors are available. |
| [Gestione Notifiche (`INotifiche`)](INotifiche.md) | Communicate the intervention request to the Supervisor. |
| [Profili e Sicurezza Account (`IProfili`)](IProfili.md) | Retrieve the minimum data to provide to emergency services. |
