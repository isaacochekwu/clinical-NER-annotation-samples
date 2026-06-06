# NER Sample 3: Discharge Summary Annotation

**Document Type:** Inpatient Discharge Summary  
**Annotator:** Isaac Ochekwu, MBBS  
**Annotation Status:** Complete  

---

## Raw Text (Pre-Annotation)

> Patient: 29-year-old female. Admitted: 3 days ago. Discharge Diagnosis: Severe malaria with thrombocytopaenia.
>
> She presented with a 5-day history of high-grade fever, headache, vomiting, and generalised body weakness. No history of seizures or altered consciousness. She had no significant past medical history and takes no regular medications. She denied any known drug allergies.
>
> On examination at admission: temperature 39.2°C, BP 104/68 mmHg, heart rate 114 bpm, SpO2 98% on room air. She appeared pale and febrile. Abdominal examination revealed mild splenomegaly.
>
> Investigations: Malaria RDT positive (Plasmodium falciparum). Full blood count showed haemoglobin of 9.2 g/dL and platelet count of 68 x10⁹/L. Liver function tests were within normal limits. Blood culture sent; results pending at discharge.
>
> Management: She was commenced on IV artesunate 2.4 mg/kg at 0, 12, and 24 hours, then switched to oral artemether-lumefantrine after 24 hours of IV therapy. She received IV fluids (Normal Saline) for hydration. Platelet count was monitored daily. No transfusion was required.
>
> Condition at discharge: Afebrile for 48 hours. Haemoglobin 10.1 g/dL. Platelet count improved to 112 x10⁹/L. Clinically stable and tolerating oral medication.
>
> Discharge medications: Artemether-lumefantrine 80/480mg BD for 3 days (to complete course). Haematinics: Ferrous sulphate 200mg OD and Folic acid 5mg OD for 4 weeks.
>
> Follow-up: Review in outpatient clinic in 1 week. Repeat FBC and malaria parasite count at follow-up.

---

## Annotated Text

> Patient: `[TEMPORAL: 29-year-old]` female. Admitted: `[TEMPORAL: 3 days ago]`. Discharge `[DIAGNOSIS: Severe malaria with thrombocytopaenia]`.
>
> She presented with a `[TEMPORAL: 5-day history]` of `[SYMPTOM: high-grade fever]` `[SEVERITY: high-grade]`, `[SYMPTOM: headache]`, `[SYMPTOM: vomiting]`, and `[SYMPTOM: generalised body weakness]`. `[NEGATION: No history of seizures]` or `[NEGATION: altered consciousness]`. She had `[NEGATION: no significant past medical history]` and `[NEGATION: takes no regular medications]`. She `[NEGATION: denied any known drug allergies]`.
>
> On examination at admission: `[LAB: temperature]` `[LAB_VALUE: 39.2°C]`, `[LAB: BP]` `[LAB_VALUE: 104/68 mmHg]`, `[LAB: heart rate]` `[LAB_VALUE: 114 bpm]`, `[LAB: SpO2]` `[LAB_VALUE: 98% on room air]`. She appeared `[SYMPTOM: pale]` and `[SYMPTOM: febrile]`. Abdominal examination revealed `[SYMPTOM: mild splenomegaly]` `[SEVERITY: mild]`.
>
> Investigations: `[LAB: Malaria RDT]` `[LAB_VALUE: positive (Plasmodium falciparum)]`. `[LAB: Full blood count]` showed `[LAB: haemoglobin]` of `[LAB_VALUE: 9.2 g/dL]` and `[LAB: platelet count]` of `[LAB_VALUE: 68 x10⁹/L]`. `[LAB: Liver function tests]` were `[LAB_VALUE: within normal limits]`. `[PROCEDURE: Blood culture]` sent; results pending at discharge.
>
> Management: She was commenced on `[DRUG: IV artesunate]` `[DOSAGE: 2.4 mg/kg at 0, 12, and 24 hours]`, then switched to oral `[DRUG: artemether-lumefantrine]` after `[TEMPORAL: 24 hours]` of IV therapy. She received `[DRUG: IV fluids (Normal Saline)]` for hydration. `[LAB: Platelet count]` was monitored daily. `[NEGATION: No transfusion was required]`.
>
> Condition at discharge: `[NEGATION: Afebrile]` for `[TEMPORAL: 48 hours]`. `[LAB: Haemoglobin]` `[LAB_VALUE: 10.1 g/dL]`. `[LAB: Platelet count]` improved to `[LAB_VALUE: 112 x10⁹/L]`. Clinically stable and tolerating oral medication.
>
> Discharge medications: `[DRUG: Artemether-lumefantrine]` `[DOSAGE: 80/480mg BD for 3 days]` (to complete course). Haematinics: `[DRUG: Ferrous sulphate]` `[DOSAGE: 200mg OD]` and `[DRUG: Folic acid]` `[DOSAGE: 5mg OD]` for `[TEMPORAL: 4 weeks]`.
>
> Follow-up: Review in outpatient clinic in `[TEMPORAL: 1 week]`. `[PROCEDURE: Repeat FBC and malaria parasite count]` at follow-up.

---

## Entity Summary Table

| Entity | Tag | Notes |
|--------|-----|-------|
| Severe malaria with thrombocytopaenia | DIAGNOSIS | Compound diagnosis — both severity and complication embedded |
| high-grade fever | SYMPTOM | Severity qualifier embedded |
| high-grade | SEVERITY | Separately tagged for severity extraction |
| headache | SYMPTOM | — |
| vomiting | SYMPTOM | — |
| generalised body weakness | SYMPTOM | Full phrase tagged |
| No history of seizures | NEGATION (inner: SYMPTOM) | Neurological red flag excluded |
| altered consciousness | NEGATION (inner: SYMPTOM) | Cerebral malaria sign excluded |
| no significant past medical history | NEGATION | Broad negation; no specific inner entity |
| takes no regular medications | NEGATION | Medication history negation |
| denied any known drug allergies | NEGATION | Safety-critical allergy negation |
| temperature 39.2°C | LAB + LAB_VALUE | Significantly elevated — severe malaria criterion |
| BP 104/68 mmHg | LAB + LAB_VALUE | Low-normal; hypotension threshold monitoring relevant |
| heart rate 114 bpm | LAB + LAB_VALUE | Tachycardic |
| SpO2 98% | LAB + LAB_VALUE | Normal |
| pale | SYMPTOM | Examination finding — correlates with anaemia (Hb 9.2) |
| febrile | SYMPTOM | Examination confirmation of symptom |
| mild splenomegaly | SYMPTOM | SEVERITY (mild) embedded and separately tagged |
| Malaria RDT | LAB | Rapid diagnostic test |
| positive (Plasmodium falciparum) | LAB_VALUE | Qualitative result with species identification |
| Full blood count | LAB | Panel investigation |
| haemoglobin 9.2 g/dL | LAB + LAB_VALUE | Mild anaemia by WHO criteria |
| platelet count 68 x10⁹/L | LAB + LAB_VALUE | Thrombocytopaenic — part of diagnosis |
| Liver function tests | LAB | Panel investigation |
| within normal limits | LAB_VALUE | Qualitative result |
| Blood culture | PROCEDURE | Therapeutic/diagnostic procedure — results pending |
| IV artesunate | DRUG | Route embedded in name — common clinical shorthand |
| 2.4 mg/kg at 0, 12, and 24 hours | DOSAGE | Weight-based dosing with multi-timepoint schedule |
| artemether-lumefantrine | DRUG | Oral combination antimalarial |
| 24 hours | TEMPORAL | Switch point from IV to oral therapy |
| IV fluids (Normal Saline) | DRUG | Crystalloid — tagged as drug for medication extraction tasks |
| No transfusion was required | NEGATION | Therapeutic negation — clinically significant |
| Afebrile for 48 hours | NEGATION + TEMPORAL | Negation of fever; 48 hours = duration of apyrexia |
| Haemoglobin 10.1 g/dL | LAB + LAB_VALUE | Improved from 9.2 — recovery trend |
| Platelet count 112 x10⁹/L | LAB + LAB_VALUE | Improved from 68 — recovery trend |
| Artemether-lumefantrine 80/480mg BD for 3 days | DRUG + DOSAGE | Completion course |
| Ferrous sulphate 200mg OD | DRUG + DOSAGE | Haematinic |
| Folic acid 5mg OD | DRUG + DOSAGE | Haematinic |
| 4 weeks | TEMPORAL | Duration of haematinic course |
| 1 week | TEMPORAL | Follow-up appointment window |
| Repeat FBC and malaria parasite count | PROCEDURE | Follow-up investigations |

---

## Annotator Notes

- **"IV artesunate":** Route (IV) is embedded in the commonly used drug name. Tagged as-is; route noted separately in annotation metadata.
- **"Afebrile for 48 hours":** Annotated as NEGATION (negation of fever symptom) combined with TEMPORAL (48 hours). This dual-entity pattern is common in discharge summaries when documenting recovery milestones.
- **Platelet count repeated across admission and discharge:** Both instances tagged; the trajectory (68 → 112 x10⁹/L) is clinically significant. NLP models trained on this should learn to associate serial LAB_VALUEs with the same LAB entity across time.
- **"Normal Saline":** Tagged under DRUG for completeness in medication extraction tasks, though it is a fluid rather than a pharmacological agent. This is a schema decision that should be standardised across a team before annotation begins.
- **Blood culture results pending:** PROCEDURE tagged; no LAB_VALUE assigned — annotator must not fabricate a result. Pending status documented in notes.
