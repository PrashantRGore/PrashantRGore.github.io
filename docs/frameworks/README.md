---
hide:
  - toc
---

# Frameworks

Conceptual frameworks and working models I have developed from my observations of Life Sciences, Pharmacovigilance, and AI adoption in regulated environments.

!!! note "Important framing"
    These are my personal working frameworks — tools I use to think about and discuss complex problems in PV digital transformation. They are not regulatory guidance, validated industry standards, or formal compliance frameworks. Where I describe what organisations "should" do, I mean it as my professional opinion, not as a mandate.

---

## Framework Library

<div class="framework-card" markdown>

### 1. Digital PV Transformation Framework™

**My proposed architecture for approaching pharmacovigilance digital transformation**

A sequential, phase-gated model that I believe should enforce business architecture before technology selection — to help prevent the most common failure mode I observe in PV transformation: digitizing broken processes rather than re-engineering them.

```
BUSINESS PROBLEM
     ↓
TRANSFORMATION DISCOVERY SPRINT™
     ↓
STANDARDIZE  →  Process Integrity Model™
     ↓
DIGITIZE     →  Unified Data Fabric
     ↓
AUTOMATE     →  Automation Continuum™
     ↓
PREDICT      →  Predictive Operating Model™
     ↓
CONTINUOUS GOVERNANCE
```

**When I think it applies:** At the initiation of any safety database migration, AI implementation, or PV operating model redesign — before any vendor is engaged.

</div>

---

<div class="framework-card" markdown>

### 2. Process Integrity Model™

**A diagnostic for exploring root causes of transformation failure**

A structured diagnostic model I developed to identify two systemic patterns I observe in PV digital transformation failure: strategic ambiguity ("cow path" syndrome) and the absence of unified Master Data Management governance.

| Pattern | Symptom | Proposed Intervention |
|---|---|---|
| **Strategic Ambiguity** | Requirements mirror the current legacy system | Enterprise Process Pruning Method™ — strip every process step that does not support a Critical to Quality factor or regulatory mandate |
| **Absent MDM Governance** | Multiple conflicting product dictionaries, duplicate patient records, inconsistent coding | Establish a single source of truth for all master data before safety database go-live |

**When I think it applies:** Requirements gathering phase of any PV system implementation.

</div>

---

<div class="framework-card" markdown>

### 3. The Automation Continuum™

**A tiered model for matching automation technology to task complexity**

A conceptual model intended to help avoid over-engineering low-risk tasks with AI, or under-automating high-volume deterministic work. Each tier maps to a PV function and its associated validation considerations.

| Tier | Technology | PV Application | Control Consideration |
|---|---|---|---|
| **Tier 1** | Rule-Based RPA | E2B gateway submission, structured data entry, duplicate detection | Process mapping, exception handling logs |
| **Tier 2** | Cognitive AI / NLP / OCR | Case intake from unstructured sources, literature screening, foreign language translation | OCR accuracy validation, translation confidence thresholds |
| **Tier 3** | Predictive ML | Signal detection, causality scoring, risk stratification | Algorithmic bias monitoring, model drift detection |
| **Tier 4** | Generative AI | PSUR/PBRER narrative drafting, aggregate report sections | Source traceability, human-in-the-loop medical review |

**When I think it applies:** Technology selection and validation planning phases.

</div>

---

<div class="framework-card" markdown>

### 4. AI-Native PV Architecture Canvas™

**A two-phase model for approaching AI-first PV architecture**

A conceptual approach that separates process pruning from architecture design — attempting to decouple strategic objectives from legacy habits before any automation is deployed.

**Phase 1 — Enterprise Process Pruning Method™**

Before drafting a User Requirement Specification, I suggest mapping every PV process and applying pruning using Lean Six Sigma and Quality by Design principles. The question I recommend asking of every process step:

- Does it directly support a Critical to Quality factor?
- Does it meet a strict regulatory mandate?
- Does it directly contribute to a patient safety outcome?

If the answer to all three is no, it is a candidate for elimination.

**Phase 2 — Automation Continuum™ Deployment**

After pruning, match each remaining process to the appropriate automation tier. Mismatching the technology to the task complexity is, in my observation, one of the most common and costly mistakes in PV technology implementation.

**When I think it applies:** Architecture design phase, prior to writing URS or SOW documents.

</div>

---

<div class="framework-card" markdown>

### 5. Transformation Readiness Canvas™

**A pre-vendor diagnostic tool I use during transformation discovery**

A structured assessment intended to evaluate legacy processes against a proposed Target Operating Model before any software vendor is engaged. The goal is to prevent organisations from entering vendor negotiations without a defensible, re-engineered process baseline.

| PV Domain | Assess Current State | Define Target State | Map Automation Tier | Define GxP Controls |
|---|---|---|---|---|
| Case Intake & Triage | ☐ | ☐ | ☐ | ☐ |
| ICSR Processing | ☐ | ☐ | ☐ | ☐ |
| Signal Detection | ☐ | ☐ | ☐ | ☐ |
| Aggregate Reporting | ☐ | ☐ | ☐ | ☐ |
| Regulatory Submissions | ☐ | ☐ | ☐ | ☐ |
| Literature Surveillance | ☐ | ☐ | ☐ | ☐ |

**When I think it applies:** The 60-day window before formal vendor RFP distribution.

</div>

---

<div class="framework-card" markdown>

### 6. Predictive Operating Model™

**My conceptual target state for a mature, AI-native PV operation**

A model describing what I believe a well-transformed PV operation could look like — where AI models ingest real-time data streams to help forecast safety signals earlier than traditional retrospective methods allow.

**Maturity progression I propose:**

| Level | Label | Defining Characteristic |
|---|---|---|
| 1 | **Reactive** | Manual, paper-based, siloed, retrospective |
| 2 | **Managed** | Digitized but heavily customized; paved cow paths |
| 3 | **Standardized** | Globally harmonized SOPs; out-of-the-box SaaS; unified MDM |
| 4 | **Digital** | Touchless case processing; API-first; AI governance in place |
| 5 | **Predictive** | Agentic AI; real-time signal forecasting; continuous GVP compliance |

In my view, organisations should define a credible 3-year roadmap from their current maturity level toward Level 4 or 5 as a reasonable medium-term ambition.

</div>

---

!!! info "Applying These Frameworks"
    These frameworks are conceptual starting points for discussion and exploration, not prescriptive playbooks. I am happy to discuss how they might be adapted to specific contexts.

    [Get in Touch →](../contact/README.md){ .md-button .md-button--primary }
