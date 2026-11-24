# UC_ACM — Minor Caller Access

Source: RAD v1.0.0, pp. 42–45.
Version: 1.00.000
Date: 2026-11-12

## Specification

- Description: Allows minor Callers aged 14–17 to register and access the platform through SPID/CIE with verified parental authorization or through Safe Access Path in guest mode.
- Primary actor: Caller Minorenne.
- Secondary actors: N/A.
- Entry condition: The minor Caller accesses the E.C.H.O. home page to use the service.
- Success: The Caller accesses their personal area pseudonymously or enters through Safe Access Path in guest mode.
- Failure: Access is denied due to missing parental consent, exceeded usage limits or device restriction, or the operation is cancelled.
- Priority: High.
- Estimated frequency: 100/day.
- Extension points: N/A.
- Generalization of: N/A.

## Main Flow

| Step | Actor | Action |
|---|---|---|
| 1 | System | Displays the home page and user information notice; requests completion of the age questionnaire. |
| 2 | Caller Minorenne | Reads the notice and declares an age between 14 and 17. |
| 3 | System | Redirects the Caller to the SPID/CIE authentication service for minors. |
| 4 | Caller Minorenne | Enters minor SPID credentials, initiating a parental consent request. |
| 5 | System | Acquires Identity Provider data, identifies the 14–17 age group and verifies parental or guardian authorization. |
| 6 | System | Confirms authorization, enables the pseudonymous profile and redirects the Caller to their personal area. |

## Alternative Flow I — Safe Access Path Activation

| Step | Actor | Action |
|---|---|---|
| 2.1 | Caller Minorenne | Declares an age between 14 and 17, indicates that parental involvement is problematic and selects Safe Access Path. |
| 2.2 | System | Verifies that the device is not restricted and has not exceeded the usage limit within the defined time window. |
| 2.3 | System | Activates Safe Access Path, grants guest access to the alternative support path and records usage for the current device. |

## Error Flow I — Restricted Device or Exceeded Usage Limit

| Step | Actor | Action |
|---|---|---|
| 2.2.1 | System | Detects an exceeded device usage limit or a restriction imposed for previous improper use. |
| 2.2.2 | System | Blocks Safe Access Path and informs the Caller that access cannot proceed. |

## Error Flow II — Missing Parental Consent

| Step | Actor | Action |
|---|---|---|
| 5.1 | System | Detects parental or guardian refusal, or expiration of the consent deadline. |
| 5.2 | System | Informs the Caller that registration cannot proceed and redirects them to the home page. |

## Notes

Safe Access Path grants guest access without parental consent or Identity Provider authentication.

## Special Requirements

- Parental authorization shall not grant access to conversation content or the minor Caller's request history.
- Safe Access Path shall enforce a maximum number of uses per device within a defined time window and block devices previously restricted for abuse.
