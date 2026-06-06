# NER Sample 2: Emergency Department Note

**Document Type:** Emergency Department Triage & Assessment Note  
**Annotator:** Isaac Ochekwu, MBBS  
**Annotation Status:** Complete  

---

## Raw Text (Pre-Annotation)

> A 62-year-old female was brought to the emergency department with sudden onset severe chest pain radiating to the left arm, associated with profuse sweating and nausea for the past 3 hours. She has a history of Type 2 Diabetes Mellitus on metformin 500mg twice daily and a previous myocardial infarction 4 years ago. She is a known hypertensive on lisinopril 10mg once daily. On arrival, BP was 160/95 mmHg, heart rate 102 bpm, RR 18 breaths/min, SpO2 94% on room air, and temperature 36.8°C. ECG showed ST elevation in leads II, III, and aVF. Troponin I was elevated at 2.8 ng/mL. She was given aspirin 300mg stat, clopidogrel 600mg loading dose, and morphine 2.5mg IV for pain. She was admitted to the coronary care unit with a working diagnosis of inferior STEMI and referred urgently for percutaneous coronary intervention.

---

## Annotated Text

> A `[TEMPORAL: 62-year-old]` female was brought to the emergency department with `[SYMPTOM: sudden onset severe chest pain]` `[SEVERITY: severe]` `[SYMPTOM: radiating to the left arm]`, associated with `[SYMPTOM: profuse sweating]` and `[SYMPTOM: nausea]` for the past `[TEMPORAL: 3 hours]`. She has a history of `[DIAGNOSIS: Type 2 Diabetes Mellitus]` on `[DRUG: metformin]` `[DOSAGE: 500mg twice daily]` and a `[DIAGNOSIS: previous myocardial infarction]` `[TEMPORAL: 4 years ago]`. She is a known `[DIAGNOSIS: hypertensive]` on `[DRUG: lisinopril]` `[DOSAGE: 10mg once daily]`. On arrival, `[LAB: BP]` was `[LAB_VALUE: 160/95 mmHg]`, `[LAB: heart rate]` `[LAB_VALUE: 102 bpm]`, `[LAB: RR]` `[LAB_VALUE: 18 breaths/min]`, `[LAB: SpO2]` `[LAB_VALUE: 94% on room air]`, and `[LAB: temperature]` `[LAB_VALUE: 36.8°C]`. `[LAB: ECG]` showed `[LAB_VALUE: ST elevation in leads II, III, and aVF]`. `[LAB: Troponin I]` was `[LAB_VALUE: elevated at 2.8 ng/mL]`. She was given `[DRUG: aspirin]` `[DOSAGE: 300mg stat]`, `[DRUG: clopidogrel]` `[DOSAGE: 600mg loading dose]`, and `[DRUG: morphine]` `[DOSAGE: 2.5mg IV]` for pain. She was admitted to the `[ANATOMY: coronary care unit]` with a working `[DIAGNOSIS: inferior STEMI]` and referred urgently for `[PROCEDURE: percutaneous coronary intervention]`.

---

## Entity Summary Table

| Entity | Tag | Notes |
|--------|-----|-------|
| sudden onset severe chest pain | SYMPTOM | Onset qualifier (sudden) and severity (severe) embedded in phrase |
| severe | SEVERITY | Also tagged separately for severity-specific downstream tasks |
| radiating to the left arm | SYMPTOM | Classic STEMI radiation pattern; separate tag from chest pain |
| profuse sweating | SYMPTOM | Diaphoresis — autonomic symptom; severity qualifier (profuse) embedded |
| nausea | SYMPTOM | Associated symptom |
| 3 hours | TEMPORAL | Duration of presenting complaint |
| Type 2 Diabetes Mellitus | DIAGNOSIS | Background comorbidity |
| metformin | DRUG | Generic name |
| 500mg twice daily | DOSAGE | Linked to metformin |
| previous myocardial infarction | DIAGNOSIS | Past cardiac history — relevant to current presentation |
| 4 years ago | TEMPORAL | Anchors past MI to timeline |
| hypertensive | DIAGNOSIS | Shorthand for hypertension; tagged as diagnosis |
| lisinopril | DRUG | ACE inhibitor — background medication |
| 10mg once daily | DOSAGE | Linked to lisinopril |
| BP | LAB | Vital sign |
| 160/95 mmHg | LAB_VALUE | Elevated — clinically significant in STEMI context |
| heart rate | LAB | Vital sign |
| 102 bpm | LAB_VALUE | Tachycardic — flagged in notes |
| RR | LAB | Respiratory rate vital sign |
| 18 breaths/min | LAB_VALUE | Within normal range |
| SpO2 | LAB | Pulse oximetry |
| 94% on room air | LAB_VALUE | Mildly reduced — clinically significant |
| temperature | LAB | Vital sign |
| 36.8°C | LAB_VALUE | Normal |
| ECG | LAB | Diagnostic investigation |
| ST elevation in leads II, III, and aVF | LAB_VALUE | Qualitative result with anatomical lead specification — inferior territory |
| Troponin I | LAB | Cardiac biomarker |
| elevated at 2.8 ng/mL | LAB_VALUE | Quantitative result with qualifier (elevated) |
| aspirin | DRUG | Antiplatelet agent |
| 300mg stat | DOSAGE | Loading dose; "stat" = immediate — temporally significant |
| clopidogrel | DRUG | P2Y12 inhibitor |
| 600mg loading dose | DOSAGE | Loading dose — higher than maintenance; clinically relevant distinction |
| morphine | DRUG | Opioid analgesic |
| 2.5mg IV | DOSAGE | Route included |
| coronary care unit | ANATOMY | Clinical location — tagged for care setting extraction |
| inferior STEMI | DIAGNOSIS | Working diagnosis; "inferior" is anatomical qualifier — both embedded |
| percutaneous coronary intervention | PROCEDURE | Therapeutic procedure |

---

## Annotator Notes

- **"sudden onset":** Onset qualifier retained within the SYMPTOM tag as it carries diagnostic significance for ACS vs. other chest pain aetiologies.
- **SEVERITY tag:** Tagged "severe" as a standalone SEVERITY entity in addition to embedding within the SYMPTOM phrase — enables downstream severity-specific extraction.
- **"working diagnosis of inferior STEMI":** "Working" signals diagnostic uncertainty — noted but not a separate tag. In a structured annotation schema, an attribute (confirmed vs. suspected) would be assigned to the DIAGNOSIS entity.
- **Troponin I "elevated at 2.8 ng/mL":** The qualifier "elevated" is retained within LAB_VALUE as it represents clinician interpretation, not just a raw number.
- **Clopidogrel 600mg:** Loading dose is clinically distinct from maintenance dose (75mg OD). The DOSAGE tag captures this, and the distinction is noted for NLP models that may need to differentiate loading from maintenance dosing patterns.
