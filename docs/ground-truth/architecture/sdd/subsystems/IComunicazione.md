# Sottosistema Comunicazione e Sessione

Source: `C20_E.C.H.O._SDD.pdf`, v1.0.0 (2026-11-25), §3.6, pp. 21.
Provided interface: `IComunicazione`.

## Provided services

| Service | Description |
|---|---|
| Avvio della sessione | Upon assignment, generates nicknames for both participants, prepares communication channels between Caller and Helper and informs the Helper if the Caller is a minor. |
| Chat testuale | Enables real-time message exchange between Caller and Helper devices without retaining content on the server. |
| Chiamata audio | Enables direct audio communication between devices without recording. |
| Ripristino della sessione | After a network interruption, if the closure timeout has not expired, restores the channels within 20 seconds of connectivity returning and recovers messages temporarily retained in the devices’ volatile memory. |
| Chiusura della sessione | Allows Caller and Helper to end the session and closes the channels. Closure is not permitted during Safe Escalation. |

## Required services and dependencies

Source: §3.6.1.

| Subsystem (interface) | Dependency rationale |
|---|---|
| [Richieste di Ascolto (`IRichieste`)](IRichieste.md) | Use information concerning the listening request state. |
