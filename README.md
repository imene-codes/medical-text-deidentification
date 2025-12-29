# medical-text-deidentification
Privacy-preserving de-identification of medical text using context-aware age generalization and PHI masking for safe LLM-based healthcare applications
# Medical Text De-identification & Privacy Preservation

## Overview
This project implements a **privacy-preserving de-identification pipeline** for medical text.
It is designed as part of a **cloud-based LLM system for medical record summarization**, ensuring that sensitive personal information is removed or generalized before downstream NLP tasks.

The focus is on **context-aware de-identification**, avoiding common pitfalls such as over-masking numerical clinical information.

---

## Why De-identification Matters
Medical texts may contain **Protected Health Information (PHI)** that can lead to patient re-identification.
This project balances:
- 🔐 Privacy protection
- 🧠 Clinical meaning preservation
- ⚙️ Practical deployment constraints

---

## Dataset
- **Source:** TimSchopf/medical_abstracts (Hugging Face)
- **Type:** Scientific medical abstracts and case reports
- **Input:** Preprocessed text from Project 1
- **Output:** De-identified medical text saved as CSV

> Note: Scientific abstracts generally contain low PHI risk. However, case-report style texts may include individual-level demographic information.

---

## Methodology

### 1. PHI Masking
Rule-based masking using regular expressions for:
- Emails
- Phone numbers
- Identifiers

### 2. Context-aware Age Handling
Instead of masking all numbers, age is generalized **only when it refers to an individual patient**, such as:
- `17-year-old`
- `aged 67`
- `54 years old`

Population-level age expressions (e.g. *patients younger than 40 years*) are preserved.

Age is generalized into buckets:
- `[AGE_CHILD]`
- `[AGE_YOUNG_ADULT]`
- `[AGE_MIDDLE_ADULT]`
- `[AGE_SENIOR]`
- `[AGE_90_PLUS]`

### 3. Optional Gender Masking
For case-report texts, gender terms may be generalized:
- `girl → [GENDER_FEMALE]`
- `man → [GENDER_MALE]`

---

## Example

**Original**
