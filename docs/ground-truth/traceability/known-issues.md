# MT — Known Issues

Source: `C20_E.C.H.O._MT.xlsx`, v1.0.

| ID | References | Issue / disposition |
|---|---|---|
| KI_MT_01 | RF_GAI_1, RNF_U_3 | `RichiestaAscoltoUI (SD 2)` is not an exact entry in the RAD Object Model; SD2 is explicitly referenced. See KI_RAD_09. |
| KI_MT_02 | RF_SE_1, RF_SE_2, RF_SE_3, RF_SE_4, RF_SE_5, RF_SE_6, RNF_A_1, RNF_A_3, RNF_O_1, RNF_L_2 | `GestioneEscalationControl` differs from RAD `GestionEscalationControl`. See KI_RAD_10. |
| KI_MT_03 | RF_SE_6 | `ModuloRendicontazioneUI` differs from RAD `ModuloRendiconatzioneUI`. See KI_RAD_10. |
| KI_MT_04 | RF_SE_1, RF_SE_4 | `ProceduraEscalation` is referenced in RAD but has no separate Object Model row; it is present in the [SDD Class Diagram](../architecture/sdd/diagrams/class-diagram.puml). Preserve the original analysis reference; use the SDD class as design context. |

## Scope

- Mock-up references are preserved in JSON but excluded from extracted scope; do not invent locators.
- TP/TCS links require explicit source relationships. Use `unresolved_references` for record-level details; escalate only material unresolved issues.
