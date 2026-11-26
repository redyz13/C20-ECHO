# Sottosistema Matching e presa in carico

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.5, pp. 19–20.
Provided interface: `IMatching`.

## Provided services

| Service | Description |
|---|---|
| Individuazione degli Helper idonei | Selects available Helpers compatible with the request categories, reserving minor Callers for qualified Helpers. Forms the recipient group using the matching algorithm, taking into account previous feedback from the same Caller, except for Safe Access Path access. |
| Proposta di presa in carico | Forwards the request to the group of Helpers, collects acceptances or refusals within the maximum time and assigns the request to the first Helper to accept. |
| Rifiuto, mancata risposta e riassegnazione | Records refusals and missing responses, excludes Helpers already contacted and repeats the search until the Caller’s maximum waiting time expires. |
| Gestione dell’indisponibilità | When no further eligible Helpers exist, informs the Caller that the request cannot be assigned and communicates the available alternatives. |

## Required services and dependencies

Source: §3.5.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Helper e Abilitazione (`IHelper`)](IHelper.md) | Retrieve information on Helper qualifications and availability. |
| [Feedback e Segnalazioni (`IFeedback`)](IFeedback.md) | Retrieve feedback previously provided by the Caller about Helpers. |
| [Gestione Notifiche (`INotifiche`)](INotifiche.md) | Send listening proposals to Helpers and communicate search outcomes to the Caller. |
| [Richieste di Ascolto (`IRichieste`)](IRichieste.md) | Use information concerning the listening request state. |
