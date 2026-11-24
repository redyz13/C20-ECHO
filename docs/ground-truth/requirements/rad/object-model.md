# Object Model

Source: RAD v1.0.0, § 3.4.3.1, pp. 60–65.

## Access Management

| Object | Type | Responsibility |
|---|---|---|
| AccountUtente | Entity | Registered user account storing identification data required for platform access. |
| Dispositivo | Entity | Stores the Safe Access Path device identifier, access count within the defined time window and permanent restriction status to enforce usage limits. |
| SessioneUtente | Entity | Stores technical information required for authentication, session maintenance and termination. |
| AccessoUtente | Control | Coordinates SPID/CIE authentication, registered user authentication, logout and account deletion; verifies access conditions. |
| SAPControl | Control | Coordinates Safe Access Path activation, verifies declared age (14–17), device eligibility and permanent restrictions. |
| QuestionarioForm | Boundary | Allows minor Callers to declare their age through the questionnaire and provide information required to verify access eligibility. |
| AreaOspite | Boundary | Guest interface available to minor Callers after successful Safe Access Path verification. |
| InterfacciaPiattaforma | Boundary | Supports authentication, parental authorization, login, logout, account deletion and Safe Access Path functions. |
| InterfacciaAutenticazione | Boundary | Exchanges user identification data with the external digital identity service. |

## User Management

| Object | Type | Responsibility |
|---|---|---|
| ProfiloUtente | Entity | Registered Caller, Helper or Supervisor profile linking certified read-only SPID/CIE identity data stored in AccountUtente to editable information, preferences and qualifications. |
| Abilitazione | Entity | Specific qualification or training specialization associated with a Helper. |
| Disponibilita | Entity | Helper availability windows storing date, start time, end time and availability status. |
| GestioneAbilitazioniControl | Control | Coordinates Supervisor verification, assignment and updating of Helper qualifications. Retrieves Helper lists and profiles, queries the partner organization, manages manual assignment, updates Abilitazione and notifies Supervisors and Helpers. |
| GestioneDisponibilitaControl | Control | Coordinates creation, modification and removal of Helper availability windows, validates time intervals and updates Disponibilita for matching. |
| GestioneProfiloControl | Control | Coordinates personal area viewing and editing, preserving read-only SPID/CIE identity data and allowing updates only to information and preferences not bound to digital identity. |
| GestioneHelperUI | Boundary | Supervisor interface for listing Helpers, viewing profiles, verifying qualifications with partner organizations, assigning or updating qualifications manually and displaying confirmation or error messages. |
| GestioneDisponibilitaUI | Boundary | Helper interface for viewing the availability calendar and creating, modifying or deleting availability windows. |
| ProfiloUtenteUI | Boundary | Personal area displaying read-only SPID/CIE identity data and Helper qualifications, and allowing authorized information and preference updates. |
| EntePartnerUI | Boundary | Interfaces with the simulated partner organization to verify Helper affiliation and completion of training required for qualifications. |

## Help Management

| Object | Type | Responsibility |
|---|---|---|
| RichiestaAscolto | Entity | Listening request containing selected thematic categories, optional description, Caller age group, unique internal identifier and lifecycle status. |
| HelperRepository | Entity | Provides access to Helper information and identifies available, compatible Helpers based on thematic categories, Caller age group, required qualifications and previously contacted Helpers. |
| RichiestaAscoltoController | Control | Coordinates listening requests and matching. Checks for existing active requests, identifies eligible Helpers, sends proposals, handles responses, rejection and timeout, assigns the first accepting Helper, manages cancellation and communicates outcomes. |
| AreaPersonaleUI | Boundary | Caller interface for initiating requests, selecting categories, entering optional descriptions, viewing waiting status, cancelling requests and receiving assignment outcomes. |
| HelperDashboard | Boundary | Helper interface for receiving proposals with categories and descriptions, accepting or rejecting within the deadline and receiving proposal withdrawal notifications. |

## Safe Escalation Management

| Object | Type | Responsibility |
|---|---|---|
| Rendicontazione | Entity | Mandatory fallback report completed by the Helper, documenting actions taken and reasons for decisions. |
| LogAudit | Entity | Records timestamp, actors and outcome of completed Safe Escalation procedures without retaining conversation content. |
| GestionEscalationControl | Control | Coordinates escalation lifecycle. Receives activation, creates ProceduraEscalation, assigns the first available Supervisor without rejection, verifies timely confirmation, reassigns on non-response, activates fallback when no Supervisor is available, receives closure with or without transfer and generates LogAudit. Maintains the Helper–Caller communication channel throughout the procedure. |
| TrasferimentoDatiControl | Control | Coordinates emergency service handover initiated by the Supervisor or fallback Helper. Selects strictly necessary and available information, transmits it to simulated emergency services, handles retries and outcomes (confirmed handover, unconfirmed handover or transmission failure), and keeps the procedure open until resolved. |
| ModuloRendicontazioneControl | Control | Requests mandatory fallback reporting after intervention, validates completeness, notifies the Helper of the recording outcome and stores the report. |
| TriggerSafeEscalation | Boundary | Helper session interface providing an escalation button visible without scrolling. Displays non-blocking fallback information, allows direct emergency service activation or continued listening and guidance, and reports transfer outcomes. |
| GestioneEmergenzaUI | Boundary | Supervisor interface displaying assigned alerts, confirming responsibility, initiating emergency service handover, closing escalation with or without transfer and displaying transmission errors. |
| ModuloRendiconatzioneUI | Boundary | Mandatory fallback reporting form for recording actions taken and reasons for decisions before procedure completion. |

## Communication Management

| Object | Type | Responsibility |
|---|---|---|
| SessioneAscolto | Entity | Active text or audio communication channel between Caller and Helper, maintaining connection status and disconnection timeout information. |
| Feedback | Entity | Stores mandatory anonymous session feedback, perceived affinity and reports of technical issues or interruptions. |
| GestioneSessioneControl | Control | Coordinates voluntary session termination, termination due to disconnection timeout, network error handling and transition to feedback collection. |
| ChatTestualeUI | Boundary | Enables real-time text messaging between Caller and Helper during listening sessions. |
| ChiamataAudioUI | Boundary | Provides controls for ongoing audio calls between Caller and Helper. |
| ModuloFeedbackUI | Boundary | Allows the Caller to submit mandatory feedback and reports at session termination. |
