# Sottosistema Profili e Sicurezza Account

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.2, pp. 16–17.
Provided interface: `IProfili`.

## Provided services

| Service | Description |
|---|---|
| Visualizzazione del profilo | Allows the user to consult information in their personal area. |
| Modifica del profilo | Allows the user to update personal-area information not obtained through SPID/CIE. |
| Eliminazione dell’account | Allows the user to delete their account, removing personal data not required for statistical purposes and retaining audit logs in pseudonymized form. |
| Fornitura di dati minimi di profilo | Makes only strictly necessary user information available to other subsystems. |
| Mitigazione degli abusi del Safe Access Path | Manages the maximum number of Safe Access Path uses per device within a defined time window and permanently prevents the device from using this mode if misuse is reported. |

## Required services and dependencies

Source: §3.2.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Feedback e Segnalazioni (`IFeedback`)](IFeedback.md) | Manage feedback associated with the user after account deletion and acquire Safe Access Path misuse reports for device inhibition. |
