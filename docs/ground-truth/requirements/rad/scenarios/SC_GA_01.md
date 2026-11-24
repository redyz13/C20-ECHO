# SC_GA_01 — User Authentication

Source: RAD v1.0.0, § 3.4.1.1, p. 26.
Actors: Utente.

| Step | Actor | System |
|---|---|---|
| 1 | An adult user accesses E.C.H.O. | Displays the home page, user information notice and questionnaire. |
| 2 | Reads the notice and completes the age questionnaire. | Identifies the user as an adult and redirects them to the simulated SPID service. |
| 3 | Enters SPID credentials and confirms authentication. | Receives Identity Provider data and confirms successful authentication. |
| 4 | Receives authentication confirmation. | Redirects the user to their personal area. |
