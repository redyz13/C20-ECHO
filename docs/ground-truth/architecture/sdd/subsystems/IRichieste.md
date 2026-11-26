# Sottosistema Richieste di Ascolto

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.4, pp. 18–19.
Provided interface: `IRichieste`.

## Provided services

| Service | Description |
|---|---|
| Creazione e invio della richiesta | Allows the Caller to submit a listening request with one or more thematic categories, an optional description and the desired channel (chat or audio), after checking that no other request is active, and starts processing it. |
| Annullamento della richiesta | Allows the Caller to cancel a request not yet taken in charge and withdraws any active proposals. Cancellation takes precedence over simultaneous acceptance. |
| Stato della richiesta | Tracks the evolution of the request and makes it available to the Caller and other subsystems. |

## Required services and dependencies

Source: §3.4.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Matching e presa in carico (`IMatching`)](IMatching.md) | Start identifying eligible Helpers by transmitting the necessary request information. |
| [Feedback e Segnalazioni (`IFeedback`)](IFeedback.md) | Signals to the subsystem when feedback has been recorded, allowing it to track the change in request state. |
| [Comunicazione e Sessione (`IComunicazione`)](IComunicazione.md) | Signals to the subsystem when the session has ended, allowing it to track the change in request state. |
