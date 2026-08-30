---
hide:
  - toc
---

# BA Portfolio

<div class="ba-project-card" markdown>

<div class="ba-project-header" markdown>
<div>
<h2>ClearVision Eye Hospital</h2>
<h3>EMR &amp; Patient Portal Digital Transformation</h3>
</div>
<div class="ba-badge-group" markdown>
<span class="ba-badge ba-badge--sector">Healthcare / EMR</span>
<span class="ba-badge ba-badge--type">Portfolio Project</span>
<span class="ba-badge ba-badge--compliance">DPDP · HIPAA · GDPR</span>
</div>
</div>

ClearVision Eye Hospital (CVH) is a fictional mid-size ophthalmology hospital used as the basis for this end-to-end BA portfolio. The project scope covers the design and documentation of a **Hospital Management System (HMS)** and **Patient Experience Portal** — digitising patient registration, appointment management, clinical documentation, billing, and compliance reporting.

All documents were authored by **Prashant Gore** as a demonstration of full-lifecycle Business Analysis: from stakeholder elicitation and requirements definition through to system test design, UAT scripting, and change control.

!!! note "Disclaimer"
    This is a prototype demonstration project only. No real patient data was used. Documents are not intended for production clinical deployment.

</div>

---

## Document Suite

<div class="ba-doc-grid" markdown>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">01</span>

### [BRD v1.3 — Business Requirements](brd.md)

Defines **what** the business of ClearVision requires. Covers business problem statement, stakeholder register, business objectives, business rules, compliance obligations, scope, and data dictionary.

`CVH-BRD-001` · Baselined

[Open Document →](brd.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">02</span>

### [FRD v1.2 — Functional Requirements](frd.md)

Defines **how** the system will behave. Module-by-module functional specifications covering all 7 HMS modules plus Patient Portal, with UI behaviour, validation rules, and data flow.

`CVH-FRD-001` · Baselined

[Open Document →](frd.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">03</span>

### [RTM v1.1 — Requirements Traceability Matrix](rtm.md)

End-to-end linkage from **Business Objectives → Business Requirements → Functional Requirements → Test Cases → UAT Scenarios**. Covers 44 requirements including CR-001 amendments.

`CVH-RTM-001` · Baselined

[Open Document →](rtm.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">04</span>

### [STC v1.1 — System Test Cases](stc.md)

QA test scripts covering all functional modules. Each test case includes preconditions, step-by-step actions, expected results, and pass/fail criteria.

`CVH-STC-001` · Baselined

[Open Document →](stc.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">05</span>

### [UAT v1.1 — User Acceptance Testing](uat.md)

Business acceptance scenarios authored for each user role (Receptionist, Doctor, Admin, Patient, IT). Includes entry/exit criteria and sign-off framework.

`CVH-UAT-001` · Baselined

[Open Document →](uat.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">06</span>

### [CR-001 v1.0 — Change Request](cr.md)

Formal change request governing the addition of **Patient Self-Registration** to scope. Covers impact analysis across BRD, FRD, RTM, and test artefacts.

`CVH-CR-001` · Approved

[Open Document →](cr.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">07</span>

### [ERD v1.0 — Entity Relationship Diagram](erd.md)

Interactive entity-relationship diagram depicting the full CVH data model — all tables, primary keys, foreign keys, and relationships across all HMS modules.

`CVH-ERD-001` · Baselined

[Open Document →](erd.md){ .md-button .md-button--primary }

</div>

<div class="ba-doc-card" markdown>

<span class="ba-doc-num">08</span>

### [SQD v1.1 — System Sequence Diagrams](sqd.md)

Interactive sequence diagrams illustrating actor-to-system message flows for all key workflows: registration, appointments, consultations, billing, and more.

`CVH-SQD-001` · Baselined

[Open Document →](sqd.md){ .md-button .md-button--primary }

</div>

</div>
