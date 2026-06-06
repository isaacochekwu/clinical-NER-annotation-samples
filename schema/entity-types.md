# Entity Type Definitions & Tagging Rules

This document defines all entity types used in clinical NER annotation, including rules for edge cases and disambiguation.

---

## SYMPTOM

**Definition:** Any subjective complaint reported by the patient or objective sign observed/documented by a clinician.

**Rules:**
- Tag the full symptom phrase, including descriptors: `[SYMPTOM: productive cough]` not just `[SYMPTOM: cough]`
- Include laterality where stated: `[SYMPTOM: right-sided chest pain]`
- Do NOT tag symptoms that are negated here — use `[NEGATION]` wrapping instead

**Examples:**
- `[SYMPTOM: fever]`
- `[SYMPTOM: shortness of breath on exertion]`
- `[SYMPTOM: progressive lower limb swelling]`

---

## DIAGNOSIS

**Definition:** A confirmed or suspected clinical diagnosis documented by a clinician.

**Rules:**
- Include qualifiers: `[DIAGNOSIS: suspected pulmonary embolism]`
- Distinguish between working diagnosis and confirmed diagnosis in your notes, even if both use the same tag
- Chronic background conditions count: `[DIAGNOSIS: Type 2 Diabetes Mellitus]`

**Examples:**
- `[DIAGNOSIS: community-acquired pneumonia]`
- `[DIAGNOSIS: hypertensive urgency]`
- `[DIAGNOSIS: iron deficiency anaemia]`

---

## DRUG

**Definition:** Any medication, whether prescribed, over-the-counter, or herbal, mentioned in the text.

**Rules:**
- Tag both generic and brand names: `[DRUG: Augmentin]`, `[DRUG: co-amoxiclav]`
- Do not merge DRUG and DOSAGE into one tag — they are always separate entities
- Include drug class references only if a specific agent is implied: "commenced on an ACE inhibitor" — tag `[DRUG: ACE inhibitor]` with a note that entity is class-level

**Examples:**
- `[DRUG: amlodipine]`
- `[DRUG: metformin]`
- `[DRUG: lisinopril]`

---

## DOSAGE

**Definition:** The amount and/or frequency of a drug dose.

**Rules:**
- Always annotate in proximity to its DRUG entity
- Include route where stated: `[DOSAGE: 500mg IV TDS]`
- If dose and frequency are separated in text, tag each component individually

**Examples:**
- `[DOSAGE: 10mg OD]`
- `[DOSAGE: 1.2g IV TDS]`
- `[DOSAGE: 40mg once daily for 5 days]`

---

## LAB

**Definition:** The name of a laboratory investigation or diagnostic test.

**Rules:**
- Tag the test name separately from its result
- Include imaging and bedside investigations: ECG, CXR, urinalysis
- Do not tag if referenced only as a category ("blood tests were done") without naming the test

**Examples:**
- `[LAB: full blood count]`
- `[LAB: serum electrolytes]`
- `[LAB: chest X-ray]`
- `[LAB: random blood glucose]`

---

## LAB_VALUE

**Definition:** A numeric or qualitative result associated with a named investigation.

**Rules:**
- Always pair with its LAB entity in annotation notes
- Include units: `[LAB_VALUE: 112 µmol/L]`
- Qualitative results count: `[LAB_VALUE: right lower lobe consolidation]`

**Examples:**
- `[LAB_VALUE: 198/112 mmHg]`
- `[LAB_VALUE: 38.9°C]`
- `[LAB_VALUE: normal sinus rhythm]`

---

## PROCEDURE

**Definition:** Any clinical intervention, diagnostic procedure, or therapeutic procedure.

**Rules:**
- Include both diagnostic and therapeutic procedures
- Distinguish from LAB where possible: an ECG ordered as a test = LAB; an ECG performed and interpreted = PROCEDURE (context-dependent)
- Surgical procedures, infusions, and clinical assessments all qualify

**Examples:**
- `[PROCEDURE: blood culture]`
- `[PROCEDURE: IV cannulation]`
- `[PROCEDURE: oxygen supplementation via face mask]`

---

## ANATOMY

**Definition:** Any body part, organ, system, or anatomical location referenced in the text.

**Rules:**
- Include laterality as part of the tag: `[ANATOMY: right lower lobe]`
- Tag anatomy even when embedded in a diagnosis phrase if it adds structural information
- Do not double-tag anatomy that is already fully captured within a DIAGNOSIS tag unless annotating for anatomy-specific downstream tasks

**Examples:**
- `[ANATOMY: right lower lobe]`
- `[ANATOMY: left ventricle]`
- `[ANATOMY: renal cortex]`

---

## TEMPORAL

**Definition:** Any time reference relating to the clinical timeline — onset, duration, frequency, or relation to an event.

**Rules:**
- Tag relative and absolute time references
- Include vague temporal markers: "recently", "for some time" — flag these as LOW PRECISION in notes
- Document temporal anchors (e.g., "on admission", "at day 3") to support timeline reconstruction

**Examples:**
- `[TEMPORAL: 3 days]`
- `[TEMPORAL: since last week]`
- `[TEMPORAL: on admission]`
- `[TEMPORAL: over the past 6 months]`

---

## SEVERITY

**Definition:** Any qualifier that describes the intensity, grade, or degree of a symptom, diagnosis, or finding.

**Rules:**
- Tag as a separate entity from the symptom or diagnosis it modifies
- Include functional impact descriptors: "limiting daily activities" qualifies as severity context
- Graded scales count: `[SEVERITY: Grade II]`, `[SEVERITY: NYHA Class III]`

**Examples:**
- `[SEVERITY: mild]`
- `[SEVERITY: severe]`
- `[SEVERITY: moderate-to-severe]`

---

## NEGATION

**Definition:** A negated clinical finding — something explicitly stated as absent or denied.

**Rules:**
- Wrap the negated entity within the NEGATION tag and retain the inner entity type in annotation notes
- Negation scope matters — "no chest pain or shortness of breath" negates both entities
- Common negation markers: no, denied, absent, not reported, without, rules out

**Examples:**
- `[NEGATION: no chest pain]` — inner entity: SYMPTOM
- `[NEGATION: denied fever]` — inner entity: SYMPTOM
- `[NEGATION: no known drug allergies]` — inner entity: contextual safety flag

---

## Edge Cases & Disambiguation

| Scenario | Ruling |
|----------|--------|
| "Hypertension on amlodipine" | DIAGNOSIS + DRUG — two separate tags |
| "BP 198/112 mmHg" | LAB (BP) + LAB_VALUE (198/112 mmHg) |
| "Right-sided pleuritic chest pain" | Single SYMPTOM tag for full phrase |
| "No significant past medical history" | NEGATION — no inner entity tag unless specific conditions follow |
| "Commenced on antibiotics" | DRUG at class level — flag as low specificity |
| "Reviewed in 2 weeks" | TEMPORAL — clinical follow-up timeline |
