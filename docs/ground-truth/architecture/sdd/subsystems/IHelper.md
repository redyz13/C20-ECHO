# Sottosistema Helper e Abilitazione

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.3, pp. 17–18.
Provided interface: `IHelper`.

## Provided services

| Service | Description |
|---|---|
| Gestione delle abilitazioni Helper | Allows the Supervisor to assign and verify Helper qualifications and specializations based on their training, including qualification to handle minors. |
| Verifica dell’abilitazione di Supervisor | Allows access in the Supervisor role only to users whose qualification has been verified with the relevant Partner Organization (Ente Partner). |
| Gestione della disponibilità | Allows the Helper to set and update their availability hours. |

## Required services and dependencies

Source: §3.3.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Profili e Sicurezza Account (`IProfili`)](IProfili.md) | View and modify Helper profile information to update availability. |
