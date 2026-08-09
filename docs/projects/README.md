---
hide:
  - toc
---

# AI Projects

Personal AI projects, proof-of-concepts, and experiments exploring potential applications in Pharmacovigilance and Life Sciences.

!!! warning "Research Disclaimer"
    These are personal portfolio projects built to explore and demonstrate AI concepts in pharmacovigilance. They are **not validated for production or clinical use** and should not be interpreted as deployable systems. Results reported reflect experimental performance on my evaluation datasets — not evidence of production effectiveness.

---

## Projects

<div class="project-card" markdown>

### 🤖 MLM Triage Agent

**Exploring agentic RAG for Medical Literature Monitoring triage automation**

A proof-of-concept agentic Retrieval-Augmented Generation (RAG) pipeline that explores how medical literature triage for pharmacovigilance relevance could potentially be automated. The system ingests scientific publications, evaluates them for adverse event relevance, and routes outputs for human review. Built to examine whether agentic AI architectures could meaningfully reduce the manual burden of MLM screening.

| Detail | Value |
|---|---|
| **Language** | Python / Jupyter Notebook |
| **Core Technology** | RAG · Agentic AI · NLP |
| **PV Domain** | Literature Surveillance / MLM |
| **Type** | Proof-of-Concept |

[View on GitHub →](https://github.com/PrashantRGore/mlm-triage-agent){ .md-button .md-button--primary }

</div>

---

<div class="project-card" markdown>

### 💊 Drug Causality BERT

**Experimenting with automated causality assessment and PBRER Section 11 drafting**

A fine-tuned BERT model that explores automated determination of causality between a drug and adverse event, with an attempt at generating a PBRER Section 11 narrative. Built to investigate whether transformer-based NLP could assist with one of the most subjective and time-consuming steps in ICSR processing. Results are experimental and not validated for clinical or regulatory use.

| Detail | Value |
|---|---|
| **Language** | Python |
| **Core Technology** | BERT · NLP · Transformers |
| **PV Domain** | ICSR Processing · Causality Assessment |
| **Output** | Experimental PBRER Section 11 draft |
| **Type** | Proof-of-Concept |

[View on GitHub →](https://github.com/PrashantRGore/drug-causality-bert){ .md-button .md-button--primary }

</div>

---

<div class="project-card" markdown>

### 💊 Drug Causality BERT v2

**Second iteration with extended PBRER Section 11 Summary generation**

An improved version of the causality model exploring enhanced drug-event relationship classification and extended report generation covering the full PBRER Section 11 Summary. This iteration addressed limitations I observed in v1 around completeness and clinical narrative quality. All outputs remain experimental.

| Detail | Value |
|---|---|
| **Language** | Python |
| **Core Technology** | BERT · NLP · Transformers |
| **PV Domain** | ICSR Processing · Aggregate Reporting |
| **Output** | Experimental PBRER Section 11 Summary draft |
| **Type** | Proof-of-Concept |

[View on GitHub →](https://github.com/PrashantRGore/drug-causality-bert-v2){ .md-button .md-button--primary }

</div>

---

<div class="project-card" markdown>

### 📡 PV Signal ML

**Exploring ML-augmented pharmacovigilance signal detection**

A research prototype exploring pharmacovigilance signal detection algorithms including disproportionality analysis, ML-based case triage, and regulatory compliance concepts aligned with ICH E2E and GVP Module IX. Built to investigate whether machine learning could complement traditional statistical signal detection methods. Educational and portfolio project only — not validated for production use.

| Detail | Value |
|---|---|
| **Language** | Python |
| **Core Technology** | ML · Statistical Signal Detection · NLP |
| **PV Domain** | Signal Detection · Regulatory Compliance |
| **Regulatory Alignment** | Concepts aligned with ICH E2E · GVP Module IX |
| **Type** | Research Prototype |

[View on GitHub →](https://github.com/PrashantRGore/PV_Signal_ML){ .md-button .md-button--primary }

</div>

---

## Technology Stack

| Category | Tools & Frameworks |
|---|---|
| **Language** | Python |
| **NLP / AI** | BERT, Transformers, RAG, LangChain concepts |
| **Data** | Jupyter Notebook, Pandas, NumPy |
| **PV Domain** | MedDRA, PBRER, ICSR, GVP, ICH E2E |
| **Cloud** | Google Cloud Platform (GCP), Azure |

[View All Repositories →](https://github.com/PrashantRGore){ .md-button }

