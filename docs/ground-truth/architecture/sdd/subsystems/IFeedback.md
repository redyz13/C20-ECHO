# Sottosistema Feedback e Segnalazioni

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.7, pp. 22.
Provided interface: `IFeedback`.

## Provided services

| Service | Description |
|---|---|
| Raccolta del feedback | At the end of a session, except those started via Safe Access Path, requires the Caller to evaluate the Helper through anonymous feedback and allows reporting technical problems or a voluntary, non-agreed disconnection. The feedback is not visible to the Helper. |
| Affinità Caller – Helper | Makes the ratings given by the same Caller to each Helper available to Matching. |
| Segnalazioni di disconnessione | Counts non-agreed disconnection reports per Helper and alerts Supervisors when the specified threshold is reached. |
| Segnalazioni di utilizzo improprio Safe Access Path | Allows the Helper to report possible misuse of Safe Access Path by the minor Caller at the end of the session. |

## Required services and dependencies

Source: §3.7.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Gestione Notifiche (`INotifiche`)](INotifiche.md) | When the specified number of non-agreed disconnection reports is reached, notify the Supervisor of the Helper’s systematic behavior. |
| [Richieste di Ascolto (`IRichieste`)](IRichieste.md) | Use information concerning the listening request state. |
