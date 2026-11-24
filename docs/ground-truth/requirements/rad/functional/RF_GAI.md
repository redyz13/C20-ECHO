# Help Management (RF_GAI)

Source: RAD v1.0.0, § 3.2.3, p. 17.

| ID | Name | Description | Actors | Priority |
|---|---|---|---|---|
| RF_GAI_1 | Request Submission | The system shall allow the Caller to create and submit a support/listening request by selecting one or more thematic categories describing it, with an optional additional description. | Caller | High |
| RF_GAI_2 | Matching System | The system shall assign each help request to a group of available and eligible Helpers through a suitable matching algorithm. | Helper, Caller | High |
| RF_GAI_3 | Request Acceptance | The system shall allow the Helper to accept a request assignment proposal. | Helper | High |
| RF_GAI_4 | Request Rejection | The system shall allow the Helper to reject a request assignment proposal. In case of rejection or no response, the system shall offer the request to other eligible Helpers. | Helper | High |
| RF_GAI_5 | No Available Helper | When no eligible Helper is available, the system shall inform the Caller and indicate available alternatives. | Caller | High |
| RF_GAI_6 | Request Cancellation | The system shall allow the Caller to cancel a listening request that has not yet been accepted. | Caller | Medium |