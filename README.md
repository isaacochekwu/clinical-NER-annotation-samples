# Clinical NER Annotation Samples

**Author:** Isaac Ochekwu, MBBS | AI Evaluation Specialist  
**Focus:** Named Entity Recognition • Healthcare NLP • Medical Text Annotation

---

## Overview

This repository contains sample annotated medical text demonstrating Named Entity Recognition (NER) tagging for healthcare NLP applications. The samples are drawn from my experience annotating clinical datasets to support medical AI training pipelines.

NER is the process of identifying and classifying specific entities (symptoms, diagnoses, medications, lab values, etc.) within unstructured clinical text. High-quality NER annotation is foundational to building reliable medical AI systems that can extract structured information from free-text clinical notes.

---

## Repository Structure

```
clinical-ner-annotation-samples/
├── README.md                         ← You are here
├── schema/
│   └── entity-types.md              ← Full entity type definitions and tagging rules
├── samples/
│   ├── ner-sample-1.md              ← Outpatient clinical note annotation
│   ├── ner-sample-2.md              ← Emergency department note annotation
│   └── ner-sample-3.md              ← Discharge summary annotation
└── guidelines/
    └── tagging-conventions.md       ← Annotation rules, edge cases, and decisions
```

---

## Entity Types Used

| Tag | Entity Type | Example |
|-----|------------|---------|
| `[SYMPTOM]` | Patient-reported or observed symptom | chest pain, shortness of breath |
| `[DIAGNOSIS]` | Confirmed or suspected diagnosis | pneumonia, hypertension |
| `[DRUG]` | Medication name (generic or brand) | amlodipine, Augmentin |
| `[DOSAGE]` | Drug dose amount and frequency | 10mg OD, 500mg BD |
| `[LAB]` | Laboratory test name | serum creatinine, FBC |
| `[LAB_VALUE]` | Numeric result of a lab test | 3.1 mmol/L, 112 µmol/L |
| `[PROCEDURE]` | Clinical procedure or investigation | ECG, chest X-ray, blood culture |
| `[ANATOMY]` | Body part or organ | right lower lobe, left ventricle |
| `[TEMPORAL]` | Time reference | 3 days, since last week, on admission |
| `[SEVERITY]` | Qualifier describing intensity | mild, severe, moderate |
| `[NEGATION]` | Negated finding | no chest pain, denied fever |

---

## Background

I am a fully licensed Medical Doctor (MBBS, University of Jos, 2021) with clinical experience across tertiary and secondary healthcare institutions in Nigeria. My annotation work draws directly on clinical training, enabling accurate identification of medical entities in context — including disambiguation of terms that carry different meanings in different clinical settings.

For example: "positive" in *"the patient tested positive for malaria"* vs. *"positive family history of hypertension"* requires contextual clinical knowledge to annotate correctly — something that distinguishes a medically trained annotator from a general NLP annotator.

---

## Tools & Workflows

Annotation work has been performed using standard annotation interfaces and documented in structured formats. Familiarity with:
- Label Studio
- Prodigy (annotation framework)
- Markdown-based annotation for documentation purposes (as used in this repo)
- Google Sheets-based annotation tracking
- Annotation guideline compliance and inter-annotator agreement (IAA) measurement

---

## Contact

- **Email:** ochekwuisaac333@gmail.com
- **LinkedIn:** [linkedin.com/in/isaac-ochekwu](https://linkedin.com/in/isaac-ochekwu)
- **GitHub:** [github.com/isaacochekwu](https://github.com/isaacochekwu)
