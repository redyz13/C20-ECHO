# RAD — Known Issues

Source: RAD v1.0.0.

## Open Issues

| ID | References | Issue |
|---|---|---|
| KI_RAD_01 | RF_GC_3, UC_CS, SCD1, UC_CS.puml | Feedback exemption for Safe Access Path is absent from the use case and diagrams. |
| KI_RAD_02 | RNF_A_2, SC_GC_01 | Recovery time after reconnection and disconnection timeout are not equivalent. |
| KI_RAD_03 | RNF_A_2, RNF_A_4 | Message recovery must comply with the prohibition on retaining communication content. |
| KI_RAD_04 | RNF_O_1, UC_GSE | Audit logging is specified both as 10 seconds after closure and within 10 seconds of closure. |
| KI_RAD_05 | RNF_O_1, SD3 | Audit logging precedes the distinction between closed and open escalation procedures. |
| KI_RAD_06 | SD1, object-model.md | Dispositivo is classified as Boundary and Entity, respectively. |
| KI_RAD_07 | SD1 | Device eligibility is evaluated in a separate alt fragment from age validation. |
| KI_RAD_08 | UC_GU, UC_GU.puml | The use case identifier differs: UC_GU vs UC_GU_1. |
| KI_RAD_09 | SD2, object-model.md | AreaPersonaleUI and RichiestaAscoltoUI are inconsistent. |
| KI_RAD_10 | SD3, object-model.md | Controller and boundary names are inconsistent. |
| KI_RAD_11 | UC_GAI.puml | The source uses extends instead of extend. |

## Extraction Limitations

- SD2 represents the matching-loop break as a reference annotation.
- PlantUML diagrams were reconstructed from RAD figures.
- Structural checks and rendering do not establish semantic equivalence.
- Full source-to-extraction semantic review remains pending.

## Exclusions

- Current and proposed system activity diagrams.
- Analysis class diagram; design class diagram deferred to SDD.
- Mock-ups.

Escalate only unresolved issues that materially affect the assigned task.
