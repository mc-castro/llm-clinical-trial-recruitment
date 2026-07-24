# LLM-Based Framework for Automated Clinical Trial Recruitment

This repository contains the implementation of the framework proposed in:

**"Architecture for Clinical Trial Patient Screening Using Large Language Models"**

The proposed framework aims to automate patient recruitment in clinical trials by combining Large Language Models (LLMs) with clinical trial protocols and Electronic Health Records (EHRs).

The framework consists of two main modules:

1. **Eligibility Criteria Extraction**  
   Extracts and structures inclusion and exclusion criteria from clinical trial protocols.

2. **Semantic Patient Matching**  
   Compares structured eligibility criteria against patient records to identify potentially eligible participants and generate clinical justifications.

The proposed architecture is designed as a parameterized pipeline, allowing the use of different clinical trial repositories, EHR sources, and language models without requiring modifications to the overall workflow.

---

# Framework Overview

The workflow receives two main sources of information:

- **Clinical trial protocols**, containing free-text eligibility requirements.
- **Electronic Health Records (EHRs)**, containing structured and unstructured patient information.


The complete architecture is illustrated below:

![Framework Architecture](docs/architecture.png)

---

# Repository Structure
```
notebooks/
│
├── 01_data/
│   └── 01_mimic_preprocessing.ipynb
│
├── 02_framework/
│   ├── 02_parsing_protocols_and_extraction.ipy
│   └── 03_clinical_patient_matching.ipynb
│
└── 03_evaluation/
    ├── 04_prepare_extraction_evaluation_sample.ipynb
    ├── 05_evaluate_extraction_with_llm_judge.ipynb
    ├── 06_analyze_extraction_results.ipynb
    ├── 07_evaluate_patient_matching_with_llm_judge.ipynb
    ├── 08_cross_model_matching_agreement.ipynb
    └── 09_generate_paper_results.ipynb
```

---

# Pipeline Components

## 1. Clinical Trial Protocol Processing

Clinical trial protocols are obtained from public repositories, particularly ClinicalTrials.gov.

The framework focuses exclusively on the **eligibility section** of each protocol, which contains:

- Inclusion criteria
- Exclusion criteria

The extraction module transforms these free-text requirements into a structured representation that can be used for patient matching.

Notebook:
notebooks/01_data/01_protocol_preprocessing.ipynb

---

## 2. Patient Representation

Patient information is represented as a combination of structured and unstructured clinical attributes.

The framework supports different EHR schemas, provided that the patient information can be transformed into a textual representation containing relevant clinical evidence.

Example attributes include:

- Demographics
- Diagnoses
- Procedures
- Laboratory measurements
- Clinical notes

Notebook:
notebooks/01_data/02_patient_preprocessing.ipynb

---

## 3. Eligibility Criteria Extraction

The first module uses an LLM to analyze the eligibility section of clinical trial protocols and generate structured inclusion and exclusion criteria.

Notebook: notebooks/02_framework/03_eligibility_extraction.ipynb


---

## 4. Semantic Patient Matching

The second module receives:

- Structured eligibility criteria
- Patient representations

The LLM evaluates whether each patient satisfies the study requirements and produces:

- Eligibility decision
- Clinical justification

Notebook:
notebooks/02_framework/04_semantic_patient_matching.ipynb


---

# Evaluation

The framework was evaluated through two main experiments.

## Eligibility Criteria Extraction Evaluation

The extraction module was assessed by comparing LLM-generated eligibility representations against human annotations.

Metrics include:

- Precision
- Recall
- Cohen's Kappa agreement

Notebook:
notebooks/03_evaluation/05_extraction_evaluation.ipynb


---

## Semantic Patient Matching Evaluation

The matching module was evaluated using an LLM-based clinical audit process.

The evaluation includes:

- Correct eligibility decisions
- False positive analysis
- Missing clinical evidence analysis
- Cross-model agreement analysis

Notebooks:
notebooks/03_evaluation/06_matching_evaluation.ipynb
notebooks/03_evaluation/07_matching_agreement_analysis.ipynb


---

# Dataset Availability

## Clinical Trial Protocols

Clinical trial protocols are publicly available and can be accessed through:

ClinicalTrials.gov

The protocol data used in the experiments are included in:
data/protocols/


---

## Electronic Health Records

Patient-level data are **not included in this repository due to privacy and data usage restrictions**.

The experiments described in the paper were conducted using the:

**MIMIC-IV-Ext Cardiac Disease dataset**

Researchers interested in reproducing the experiments must obtain appropriate access to the dataset and provide a compatible patient representation.


---

# Installation

Clone this repository:

```bash
git clone https://github.com/mc-castro/llm-clinical-trial-recruitment.git

cd llm-clinical-trial-recruitment
```
Install dependencies:
```bash
pip install -r requirements.txt
```