# NER Sample 1: Outpatient Clinical Note

**Document Type:** Outpatient Consultation Note  
**Annotator:** Isaac Ochekwu, MBBS  
**Annotation Status:** Complete  

---

## Raw Text (Pre-Annotation)

> A 45-year-old male presents with a 2-week history of productive cough, fever, and right-sided chest pain that worsens on deep breathing. He denies haemoptysis or shortness of breath at rest. He has a background history of hypertension managed on amlodipine 10mg once daily. No known drug allergies. On examination, temperature was 38.6°C, respiratory rate 22 breaths/min, and SpO2 96% on room air. Chest auscultation revealed reduced air entry at the right base with dullness to percussion. Chest X-ray showed right lower lobe consolidation. He was diagnosed with community-acquired pneumonia and commenced on amoxicillin-clavulanate 625mg TDS for 7 days and azithromycin 500mg OD for 5 days. He was advised to return if symptoms worsen or if fever persists beyond 72 hours.

---

## Annotated Text

> A `[TEMPORAL: 45-year-old]` male presents with a `[TEMPORAL: 2-week history]` of `[SYMPTOM: productive cough]`, `[SYMPTOM: fever]`, and `[SYMPTOM: right-sided chest pain that worsens on deep breathing]`. He `[NEGATION: denies haemoptysis]` or `[NEGATION: shortness of breath at rest]`. He has a background history of `[DIAGNOSIS: hypertension]` managed on `[DRUG: amlodipine]` `[DOSAGE: 10mg once daily]`. `[NEGATION: No known drug allergies]`. On examination, `[LAB: temperature]` was `[LAB_VALUE: 38.6°C]`, `[LAB: respiratory rate]` `[LAB_VALUE: 22 breaths/min]`, and `[LAB: SpO2]` `[LAB_VALUE: 96% on room air]`. Chest auscultation revealed `[SYMPTOM: reduced air entry at the right base]` with `[SYMPTOM: dullness to percussion]`. `[LAB: Chest X-ray]` showed `[LAB_VALUE: right lower lobe consolidation]`. He was diagnosed with `[DIAGNOSIS: community-acquired pneumonia]` and commenced on `[DRUG: amoxicillin-clavulanate]` `[DOSAGE: 625mg TDS for 7 days]` and `[DRUG: azithromycin]` `[DOSAGE: 500mg OD for 5 days]`. He was advised to return if symptoms worsen or if `[SYMPTOM: fever]` persists beyond `[TEMPORAL: 72 hours]`.

---

## Entity Summary Table

| Entity | Tag | Notes |
|--------|-----|-------|
| productive cough | SYMPTOM | Full descriptive phrase tagged |
| fever | SYMPTOM | Appears twice; both instances tagged |
| right-sided chest pain that worsens on deep breathing | SYMPTOM | Full phrase including qualifier tagged as single entity |
| haemoptysis | NEGATION (inner: SYMPTOM) | Denied by patient |
| shortness of breath at rest | NEGATION (inner: SYMPTOM) | Denied; includes qualifier "at rest" |
| hypertension | DIAGNOSIS | Background/chronic condition |
| amlodipine | DRUG | Generic name |
| 10mg once daily | DOSAGE | Linked to amlodipine |
| No known drug allergies | NEGATION | Safety-critical flag; no inner entity |
| temperature | LAB | Bedside vital sign |
| 38.6°C | LAB_VALUE | Linked to temperature |
| respiratory rate | LAB | Bedside vital sign |
| 22 breaths/min | LAB_VALUE | Linked to respiratory rate; tachypnoeic — clinical note added |
| SpO2 | LAB | Pulse oximetry |
| 96% on room air | LAB_VALUE | Includes context (room air) — important for clinical interpretation |
| reduced air entry at the right base | SYMPTOM | Examination finding; ANATOMY (right base) embedded |
| dullness to percussion | SYMPTOM | Examination finding |
| Chest X-ray | LAB | Diagnostic investigation |
| right lower lobe consolidation | LAB_VALUE | Qualitative imaging result |
| community-acquired pneumonia | DIAGNOSIS | Primary diagnosis |
| amoxicillin-clavulanate | DRUG | Generic compound name |
| 625mg TDS for 7 days | DOSAGE | Includes duration |
| azithromycin | DRUG | Second antibiotic agent |
| 500mg OD for 5 days | DOSAGE | Includes duration |
| 72 hours | TEMPORAL | Follow-up trigger timepoint |

---

## Annotator Notes

- **RR 22 breaths/min:** Tachypnoeic finding — clinically significant as it contributes to CURB-65 severity scoring. Flagged in clinical note but not a separate annotation tag.
- **SpO2 96% on room air:** The qualifier "on room air" is medically important (distinguishes from supplemental oxygen context). Retained within the LAB_VALUE tag.
- **"right lower lobe consolidation":** Tagged as LAB_VALUE (qualitative imaging result) rather than DIAGNOSIS, as it is an imaging finding, not a clinician-stated diagnosis. The diagnosis (CAP) is separate.
- **Dual antibiotic regimen:** Both agents tagged separately. No overlap or conflict detected — atypical cover (azithromycin) alongside beta-lactam (co-amoxiclav) is consistent with CAP guidelines.
