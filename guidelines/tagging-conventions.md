# Tagging Conventions & Annotation Decisions

This document records the annotation conventions, team decisions, and edge case rulings used throughout this repository. It serves as the living style guide for consistent annotation.

---

## General Principles

1. **Tag the most informative span.** Always prefer the full descriptive phrase over the minimal entity. `[SYMPTOM: right-sided pleuritic chest pain]` is more useful than `[SYMPTOM: pain]`.

2. **Do not infer.** If the text does not state it, do not tag it. Annotators should not add entities based on clinical knowledge of what "should" be present.

3. **Separate entities, even when adjacent.** `[DRUG: amlodipine]` `[DOSAGE: 10mg OD]` — always two tags, never merged into one.

4. **Retain context within tags where clinically meaningful.** `[LAB_VALUE: 94% on room air]` — "on room air" changes the clinical interpretation and must be retained.

5. **Negation takes priority.** If an entity is negated, tag it as NEGATION and note the inner entity type — do not tag the inner entity as a standalone.

---

## Span Boundary Rules

| Scenario | Rule |
|----------|------|
| Symptom with location | Include location in SYMPTOM span: `[SYMPTOM: right-sided chest pain]` |
| Drug + route as one phrase | Tag drug name only; note route separately: `[DRUG: artesunate]` route=IV |
| Dosage split across sentence | Tag each component independently with a linking note |
| Compound diagnosis | Tag as single DIAGNOSIS entity: `[DIAGNOSIS: severe malaria with thrombocytopaenia]` |
| Diagnosis with qualifier | Include qualifier in tag: `[DIAGNOSIS: suspected pulmonary embolism]` |
| Imaging result (qualitative) | Tag as LAB_VALUE: `[LAB_VALUE: right lower lobe consolidation]` |
| Normal lab result | Tag LAB_VALUE even for normal results: `[LAB_VALUE: within normal limits]` |

---

## Negation Scope Rules

Negation scope extends to all entities following the negation marker within the same clause.

**Example:**  
*"No chest pain, dyspnoea, or palpitations."*  
→ All three are negated: `[NEGATION: chest pain]`, `[NEGATION: dyspnoea]`, `[NEGATION: palpitations]`

Negation scope ends at:
- A full stop or new sentence
- A conjunction indicating a positive finding ("but", "however", "although")
- A change of subject

---

## Disambiguation Decisions

### "Positive" and "Negative" Results
- *"Malaria RDT positive"* → `[LAB_VALUE: positive (Plasmodium falciparum)]` — qualitative result, NOT a negation context
- *"Blood culture negative"* → `[LAB_VALUE: negative]` — qualitative result, NOT annotated under NEGATION

### Drug Class vs. Specific Agent
- *"commenced on an antibiotic"* → `[DRUG: antibiotic]` — class-level; flag as LOW SPECIFICITY in metadata
- *"commenced on amoxicillin"* → `[DRUG: amoxicillin]` — specific agent; preferred

### Vital Signs vs. Laboratory Tests
Both are tagged as LAB + LAB_VALUE. Vital signs (BP, HR, RR, Temp, SpO2) are treated as bedside laboratory measurements in this schema.

### Past vs. Current Diagnoses
Both tagged as DIAGNOSIS. Temporal context (TEMPORAL tag) distinguishes them:
- *"previous myocardial infarction 4 years ago"* → `[DIAGNOSIS: myocardial infarction]` + `[TEMPORAL: 4 years ago]`
- *"presenting with pneumonia"* → `[DIAGNOSIS: pneumonia]` (current, no temporal qualifier needed)

---

## Inter-Annotator Agreement (IAA)

Target IAA for this annotation schema: **≥ 90% F1** across all entity types.

Common sources of disagreement:
- Span boundary disputes (full phrase vs. minimal span)
- Negation scope in complex sentences
- Drug class vs. specific agent tagging
- Whether an examination finding is a SYMPTOM or LAB_VALUE

Resolution process:
1. Flag disagreement
2. Both annotators discuss with reference to this guide
3. If unresolved, escalate to senior medical reviewer
4. Document final ruling in this file as a permanent convention

---

## Version History

| Version | Change | Date |
|---------|--------|------|
| 1.0 | Initial schema established | 2024 |
| 1.1 | Added negation scope rules | 2024 |
| 1.2 | Disambiguation: positive/negative results clarified | 2025 |
| 1.3 | Vital signs vs. lab tests ruling added | 2025 |

---

*Maintained by Isaac Ochekwu, MBBS*
