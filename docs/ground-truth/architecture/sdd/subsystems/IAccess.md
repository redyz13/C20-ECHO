# Sottosistema Accesso e tutela minori

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.1, pp. 15–16.
Provided interface: `IAccess`.

## Provided services

| Service | Description |
|---|---|
| Registrazione con SPID/CIE | Allows a new user to register through the simulated digital identity service, acquiring the necessary personal identification data. |
| Verifica dell'età minima | Determines the age category (minor or adult) from digital identity data and prevents registration below age 14, indicating alternative information resources. |
| Autorizzazione genitoriale | Requests and verifies authorization from a parent or guardian through the simulated service for the minor to access the service, and checks its validity. |
| Attivazione del Safe Access Path | Allows a minor to access in guest mode without parental authorization when involving their parents is problematic, after checking the age declared in the initial questionnaire and the usage restrictions associated with the device. |
| Login e logout | Allows a registered user to authenticate, identifying their role as Caller, Helper or Supervisor, and to terminate their authenticated session. |

## Required services and dependencies

Source: §3.1.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Helper e Abilitazione (`IHelper`)](IHelper.md) | Verify qualifications associated with users in the Helper or Supervisor role. |
| [Profili e Sicurezza Account (`IProfili`)](IProfili.md) | Verify Safe Access Path usage restrictions associated with the device. |
