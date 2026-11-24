# Access Management (RF_GA)

Source: RAD v1.0.0, § 3.2.1, pp. 14–15.

| ID | Name | Description | Actors | Priority |
|---|---|---|---|---|
| RF_GA_1 | SPID/CIE Registration | The system shall allow users to register through a SPID/CIE digital identity service. | Utente | High |
| RF_GA_2 | Safe Path Activation | The system shall allow a minor Caller experiencing difficulties with their parents or guardians to activate the Safe Access Path without parental authorization. On first use, the user shall complete a brief age verification questionnaire. If the user declares an age between 14 and 17, the system shall grant access and allow communication with an eligible Helper. | Caller Minorenne | High |
| RF_GA_3 | Parental Authorization | When accessing through SPID/CIE, the system shall require parental authorization for minor Callers. Authorization shall not grant access to the Caller's requests or sessions. | Caller Minorenne | High |
| RF_GA_4 | Login | The system shall allow registered users to authenticate and access the platform. | Utente | High |
| RF_GA_5 | Logout | The system shall allow users to terminate their authenticated session. | Utente | High |
| RF_GA_6 | Minimum Age Verification | The system shall verify age before registration and prevent completion of SPID/CIE registration for Callers under 14, providing alternative informational resources. | Caller | High |
| RF_GA_7 | Account Deletion | The system shall allow users to delete their accounts. | Utente | Medium |
| RF_GA_8 | Safe Access Path Abuse Mitigation | The system shall implement abuse detection and mitigation. At the end of the call, the Helper shall be able to report improper use of the Safe Access Path, resulting in permanent restriction of this access mode on the specific device. Safe Access Path usage from the same device shall also be subject to a maximum number of uses within a defined time window. | Helper | Medium |
