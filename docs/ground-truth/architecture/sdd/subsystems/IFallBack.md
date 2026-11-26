# Sottosistema Gestione Fallback Escalation

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.9, pp. 24–25.
Provided interface: `IFallBack`.

## Provided services

| Service | Description |
|---|---|
| Gestione del Fallback | When no Supervisors are available, informs the Helper through a non-blocking notification and allows them to continue listening, potentially directing the Caller towards qualified services, or directly activating the simulated emergency services. |
| Rendicontazione del Fallback | Requires the Helper, at the end of the fallback intervention, to complete a reporting form containing the actions taken and reasons for the decisions made. Recorded information is accessible exclusively to authorized Supervisors. |

## Required services and dependencies

Source: §3.9.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Gestione Notifiche (`INotifiche`)](INotifiche.md) | Communicate Supervisor unavailability and available alternatives to the Helper. |
| [Safe Escalation (`ISafeEscalation`)](ISafeEscalation.md) | Use information concerning the Safe Escalation request state. |
