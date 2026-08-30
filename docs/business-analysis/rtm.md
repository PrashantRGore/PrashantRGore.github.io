---
hide:
  - toc
---

<div class="ba-meta-bar" markdown>
<span class="ba-badge ba-badge--id">CVH-RTM-001</span> <span class="ba-badge ba-badge--version">Version 1.1</span> <span class="ba-badge ba-badge--status">Baselined</span> <span class="ba-badge ba-badge--compliance">DPDP / HIPAA / GDPR</span>
</div>

# Requirements Traceability Matrix (RTM)

<div class="ba-table-scroll" markdown>

|                    |                                                                  |
|--------------------|------------------------------------------------------------------|
| Document ID        | CVH-RTM-001                                                      |
| Version            | 1.1 – CVH-CR-001 Amendment                                       |
| Date               | July 2026                                                        |
| Prepared By        | Prashant Gore – BA & Digital Transformation Consultant           |
| Parent Documents   | CVH-BRD-001 v1.3 \| CVH-FRD-001 v1.2                             |
| Total Requirements | 44 (40 original + 4 from CVH-CR-001; FR-SEC-10 added under O-06) |
| Status             | DRAFT – Under Review                                             |

> *DISCLAIMER: Prototype demonstration project only. No real patient data. Not for production clinical deployment.*

## 1. Purpose & Scope
This RTM provides end-to-end linkage from Business Objectives through Business Requirements and Functional Requirements to Test Cases and UAT Scenarios.

|                                  |                  |                                                       |
|----------------------------------|------------------|-------------------------------------------------------|
| **Document**                     | **ID**           | **Role in Chain**                                     |
| Business Requirements Document   | CVH-BRD-001 v1.3 | Defines WHAT the business needs (Objectives + BR IDs) |
| Functional Requirements Document | CVH-FRD-001 v1.2 | Defines HOW the system will behave (FR IDs)           |
| Requirements Traceability Matrix | CVH-RTM-001 v1.1 | Maps: Objective → BR → FR → TC → UAT                  |
| System Test Cases                | CVH-STC-001 v1.1 | QA test steps, expected results, pass/fail criteria   |
| UAT Scripts                      | CVH-UAT-001 v1.1 | Business acceptance scenarios by role representatives |
| Change Request                   | CVH-CR-001 v1.0  | Governs scope addition: Patient Self-Registration     |

## 2. Status Key & Conventions
|            |                                                    |
|------------|----------------------------------------------------|
| **Status** | **Meaning**                                        |
| Planned    | Requirement identified; test case not yet designed |
| Designed   | Test case documented in CVH-STC-001 v1.1           |
| Executed   | Test case run against prototype                    |
| Passed     | Acceptance criteria met                            |
| Failed     | Defect raised                                      |
| Deferred   | Deferred to future phase                           |

*Priority: Must Have = regulatory/core operational \| Should Have = significant value \| Could Have = desirable enhancement*

*FR IDs reference CVH-FRD-001 v1.2. TC IDs reference CVH-STC-001 v1.1. UAT IDs reference CVH-UAT-001 v1.1.*

*record\_reference in audit\_log is a polymorphic reference (not a relational FK) — may reference any business entity.*

## 3. Requirements Traceability Matrix
|            |                                           |               |                                                                                     |                                            |                |              |                          |                                                                               |            |
|------------|-------------------------------------------|---------------|-------------------------------------------------------------------------------------|--------------------------------------------|----------------|--------------|--------------------------|-------------------------------------------------------------------------------|------------|
| **Obj ID** | **Business Objective**                    | **BR ID**     | **BR Requirement (Summary)**                                                        | **FR ID**                                  | **Module**     | **Priority** | **TC ID**                | **UAT ID**                                                                    | **Status** |
| O-01       | Digitise patient registration             | BR-REQ-PR-01  | Digital patient registration capturing all required information                     | FR-PR-01                                   | MOD-01         | Must Have    | TC-PR-001                | UAT-PR-001                                                                    | Planned    |
| O-01       |                                           | BR-REQ-PR-02  | Unique patient identification via combination duplicate detection (Name+DOB+Mobile) | FR-PR-02                                   | MOD-01         | Must Have    | TC-PR-002                | UAT-PR-002                                                                    | Planned    |
| O-01       |                                           | BR-REQ-PR-03  | Patient consent captured; registration blocked without consent                      | FR-PR-03                                   | MOD-01         | Must Have    | TC-PR-003                | UAT-PR-003                                                                    | Planned    |
| O-01       |                                           | BR-REQ-PR-04  | Record retrieval and role-restricted editing; patient views own records in portal   | FR-PR-04, FR-PAT-01, FR-PAT-03             | MOD-01, MOD-07 | Must Have    | TC-PR-004                | UAT-PR-004, UAT-PAT-001, UAT-PAT-003                                          | Planned    |
| O-01       |                                           | BR-REQ-PR-05  | Ophthalmology medical history captured at registration                              | FR-PR-05                                   | MOD-01         | Must Have    | TC-PR-005                | UAT-PR-005                                                                    | Planned    |
| O-02       | Implement appointment management          | BR-REQ-APT-01 | Digital scheduling with real-time availability and conflict detection               | FR-APT-01, FR-APT-02                       | MOD-02         | Must Have    | TC-APT-001               | UAT-APT-001                                                                   | Planned    |
| O-02       |                                           | BR-REQ-APT-02 | Appointment status tracked across full patient journey (incl. No-Show)              | FR-APT-03, FR-APT-06, FR-REC-01, FR-REC-02 | MOD-02, MOD-05 | Must Have    | TC-APT-002, TC-APT-005   | UAT-APT-002                                                                   | Planned    |
| O-02       |                                           | BR-REQ-APT-03 | Emergency and walk-in accommodation outside standard queue                          | FR-APT-04                                  | MOD-02         | Must Have    | TC-APT-003               | UAT-APT-001                                                                   | Planned    |
| O-02       |                                           | BR-REQ-APT-04 | Cancellation and reschedule with mandatory reason; Late Cancellation flag           | FR-APT-05, FR-REC-03                       | MOD-02, MOD-05 | Must Have    | TC-APT-004               | UAT-APT-003                                                                   | Planned    |
| O-02       |                                           | BR-REQ-APT-05 | No-show identification; auto-assigned 15 min after slot time                        | FR-APT-06                                  | MOD-02         | Should Have  | TC-APT-005               | UAT-APT-002                                                                   | Planned    |
| O-03       | Enable electronic clinical documentation  | BR-REQ-CLN-01 | Structured consultation notes; patient views Diagnosis + Plan summary in portal     | FR-CLN-01, FR-CLN-02, FR-CLN-03, FR-PAT-02 | MOD-03, MOD-07 | Must Have    | TC-CLN-001               | UAT-CLN-001, UAT-CLN-002, UAT-CLN-003, UAT-PAT-002                            | Planned    |
| O-03       |                                           | BR-REQ-CLN-02 | Digital prescription linked to consultation; blocked if no consultation saved       | FR-CLN-04                                  | MOD-03         | Must Have    | TC-CLN-002               | UAT-CLN-004                                                                   | Planned    |
| O-03       |                                           | BR-REQ-CLN-03 | Clinician records patient vitals prior to consultation; Doctors read-only           | FR-CLN-07, FR-CLN-08, FR-CLN-09, FR-CLN-10 | MOD-04         | Must Have    | TC-CLN-003               | UAT-CLN-007, UAT-CLN-008                                                      | Planned    |
| O-03       |                                           | BR-REQ-CLN-04 | Clinical records maintain immutable audit trail; 24-hour edit lock                  | FR-CLN-05                                  | MOD-03         | Must Have    | TC-CLN-004               | UAT-CLN-006                                                                   | Planned    |
| O-03       |                                           | BR-REQ-CLN-05 | Investigation orders raised and linked to specific patient visit                    | FR-CLN-06                                  | MOD-03         | Should Have  | TC-CLN-005               | (No dedicated UAT scenario — verified implicitly via TC-CLN-005)              | Planned    |
| O-04       | Deploy Role-Based Access Control          | BR-REQ-AM-01  | All users authenticated before portal access                                        | FR-AM-01                                   | MOD-09         | Must Have    | TC-AM-001                | UAT-AM-002                                                                    | Planned    |
| O-04       |                                           | BR-REQ-AM-02  | RBAC enforcing minimum necessary access per role                                    | FR-AM-02                                   | MOD-09         | Must Have    | TC-AM-002                | UAT-AM-001, UAT-SEC-002                                                       | Planned    |
| O-04       |                                           | BR-REQ-AM-03  | Session timeout after 15 minutes of inactivity                                      | FR-AM-03, FR-SEC-05                        | MOD-09         | Must Have    | TC-AM-003                | UAT-AM-004                                                                    | Planned    |
| O-04       |                                           | BR-REQ-AM-04  | Account lockout after 3 consecutive failed logins                                   | FR-AM-04, FR-SEC-04                        | MOD-09         | Must Have    | TC-AM-004                | UAT-AM-003                                                                    | Planned    |
| O-04       | (CR-001)                                  | BR-SEC-02     | Password complexity enforced at self-registration, creation, and reset              | FR-PAT-08, FR-AM-07                        | MOD-07, MOD-09 | Must Have    | TC-PAT-SR-004, TC-AM-007 | UAT-PAT-SR-003                                                                | Planned    |
| O-05       | Build IT admin & compliance monitoring    | BR-REQ-IT-01  | System Administrator manages user accounts and roles centrally                      | FR-IT-01                                   | MOD-06         | Must Have    | TC-IT-001                | UAT-IT-001, UAT-IT-004                                                        | Planned    |
| O-05       |                                           | BR-REQ-IT-02  | Complete tamper-evident audit log of all system activity                            | FR-AUD-01, FR-AUD-02, FR-IT-02             | MOD-10         | Must Have    | TC-IT-002                | UAT-IT-002, UAT-SEC-003                                                       | Planned    |
| O-05       |                                           | BR-REQ-IT-03  | System health indicators and holiday configuration visible to System Administrator  | FR-IT-03, FR-IT-04                         | MOD-06         | Should Have  | TC-IT-003, TC-IT-004     | UAT-IT-003                                                                    | Planned    |
| O-06       | Implement compliance-aware data practices | DPDP-01       | Consent captured and recorded at registration and self-registration                 | FR-PR-03, FR-PAT-04, FR-SEC-08             | MOD-01, MOD-07 | Must Have    | TC-SEC-001               | UAT-SEC-001                                                                   | Planned    |
| O-06       |                                           | DPDP-02       | Data accuracy enforced via field validation                                         | FR-PR-02, FR-PAT-06                        | MOD-01         | Must Have    | TC-SEC-002               | UAT-UX-002                                                                    | Planned    |
| O-06       |                                           | DPDP-07       | Security safeguards against data breach                                             | FR-SEC-03, FR-AM-03                        | MOD-09         | Must Have    | TC-AM-003                | UAT-AM-004                                                                    | Planned    |
| O-06       |                                           | HIPAA-02      | Audit controls — all system activity recorded and reviewable                        | FR-AUD-01, FR-IT-02                        | MOD-10         | Must Have    | TC-IT-002                | UAT-SEC-003                                                                   | Planned    |
| O-06       |                                           | HIPAA-05      | Minimum necessary — RBAC limits PHI access per role                                 | FR-AM-02, FR-SEC-05                        | MOD-09         | Must Have    | TC-AM-002                | UAT-SEC-002                                                                   | Planned    |
| O-06       |                                           | HIPAA-06      | Data integrity — consultation records protected from alteration after 24 hrs        | FR-CLN-05                                  | MOD-03         | Must Have    | TC-CLN-004               | UAT-CLN-006                                                                   | Planned    |
| O-06       |                                           | GDPR-06       | Data Protection by Design embedded in architecture                                  | FR-AM-02, FR-SEC-07                        | MOD-09         | Must Have    | TC-AM-002                | UAT-AM-001                                                                    | Planned    |
| O-06       |                                           | FR-SEC-10     | Error messages must not expose system internals, stack traces, or DB details        | FR-SEC-10                                  | All            | Must Have    | TC-SEC-009               | UAT-SEC-004                                                                   | Planned    |
| O-07       | Deliver role-appropriate user experience  | NFR-05        | Role-specific UI — users see only designated modules (BRD §11)                      | FR-AM-02                                   | MOD-09         | Should Have  | TC-UX-001                | UAT-UX-001                                                                    | Planned    |
| O-07       |                                           | NFR-06        | Field-level validation with actionable error messages (BRD §11)                     | FR-PR-02, FR-PAT-06                        | MOD-01 to 10   | Should Have  | TC-UX-002                | UAT-UX-002                                                                    | Planned    |
| O-07       |                                           | T-NFR-02      | Application accessible across modern web browsers (FRD §17)                         | T-NFR-02                                   | All            | Should Have  | TC-UX-003                | UAT-UX-003                                                                    | Planned    |
| O-08       | Management reporting dashboards           | RPT-01        | Daily appointment summary report                                                    | FR-RPT-01, FR-RPT-02                       | MOD-08         | Should Have  | TC-RPT-001               | UAT-RPT-001                                                                   | Planned    |
| O-08       |                                           | RPT-02        | Doctor utilisation report                                                           | FR-RPT-03                                  | MOD-08         | Should Have  | TC-RPT-002               | UAT-RPT-002                                                                   | Planned    |
| O-08       |                                           | RPT-03        | Patient registration summary                                                        | FR-RPT-03                                  | MOD-08         | Should Have  | TC-RPT-003               | UAT-RPT-004                                                                   | Planned    |
| O-08       |                                           | RPT-04        | No-show and cancellation report                                                     | FR-RPT-04                                  | MOD-08         | Should Have  | TC-RPT-004               | UAT-RPT-003                                                                   | Planned    |
| O-08       |                                           | RPT-05        | Audit activity report (System Administrator and Dean)                               | FR-RPT-05                                  | MOD-08         | Should Have  | TC-RPT-005               | UAT-RPT-005                                                                   | Planned    |
| O-08       |                                           | RPT-06        | Compliance status summary                                                           | FR-RPT-05                                  | MOD-08         | Should Have  | TC-RPT-006               | UAT-RPT-005                                                                   | Planned    |
| O-08       |                                           | RPT-07        | Patient demographics summary                                                        | FR-RPT-06                                  | MOD-08         | Could Have   | TC-RPT-007               | (No dedicated UAT scenario — demographics partially within UAT-RPT-002 scope) | Planned    |
| O-01       | Patient Self-Registration (CVH-CR-001)    | BR-PAT-07     | Patient self-registration via public portal page                                    | FR-PAT-05                                  | MOD-07         | Must Have    | TC-PAT-SR-001            | UAT-PAT-SR-001                                                                | Planned    |
| O-01       |                                           | BR-PAT-08     | Self-reg form with combination duplicate detection (Name+DOB+Mobile)                | FR-PAT-06                                  | MOD-07         | Must Have    | TC-PAT-SR-002            | UAT-PAT-SR-002                                                                | Planned    |
| O-01       |                                           | BR-PAT-09     | Auto Patient ID + account creation + auto-login on self-registration                | FR-PAT-07                                  | MOD-07         | Must Have    | TC-PAT-SR-003            | UAT-PAT-SR-003, UAT-PAT-SR-004                                                | Planned    |

## 4. Coverage Summary
**4.1 Requirements by Business Objective**

|                                  |                                                                    |                                             |                                        |                                                              |               |                 |                |
|----------------------------------|--------------------------------------------------------------------|---------------------------------------------|----------------------------------------|--------------------------------------------------------------|---------------|-----------------|----------------|
| **Business Objective**           | **BR / Compliance IDs**                                            | **FR IDs**                                  | **TC IDs**                             | **UAT IDs**                                                  | **Must Have** | **Should Have** | **Could Have** |
| O-01: Patient Registration       | BR-REQ-PR-01 to 05, BR-PAT-07 to 09 (8 BRs)                        | FR-PR-01 to 05, FR-PAT-05 to 08             | TC-PR-001 to 005, TC-PAT-SR-001 to 004 | UAT-PR-001 to 005, UAT-PAT-001 to 003, UAT-PAT-SR-001 to 004 | 8             | 0               | 0              |
| O-02: Appointment Management     | BR-REQ-APT-01 to 05 (5 BRs)                                        | FR-APT-01 to 06, FR-REC-01 to 03            | TC-APT-001 to 005                      | UAT-APT-001 to 003                                           | 4             | 1               | 0              |
| O-03: Clinical Documentation     | BR-REQ-CLN-01 to 05 (5 BRs)                                        | FR-CLN-01 to 10                             | TC-CLN-001 to 006                      | UAT-CLN-001 to 008                                           | 4             | 1               | 0              |
| O-04: Role-Based Access Control  | BR-REQ-AM-01 to 04, BR-SEC-02 (5 BRs)                              | FR-AM-01 to 09, FR-PAT-08, FR-SEC-04/05     | TC-AM-001 to 009, TC-PAT-SR-004        | UAT-AM-001 to 004, UAT-PAT-SR-004                            | 5             | 0               | 0              |
| O-05: IT & Compliance Monitoring | BR-REQ-IT-01 to 03 (3 BRs)                                         | FR-IT-01 to 04, FR-AUD-01 to 04             | TC-IT-001 to 004                       | UAT-IT-001 to 004                                            | 2             | 1               | 0              |
| O-06: Compliance-Aware Practices | DPDP-01/02/07, HIPAA-02/05/06, GDPR-06, FR-SEC-10 (8 BRs/controls) | FR-SEC-01 to 10, FR-PR-03, FR-PAT-04        | TC-SEC-001 to 011                      | UAT-SEC-001 to 004                                           | 8             | 0               | 0              |
| O-07: User Experience            | NFR-05, NFR-06, T-NFR-02 (3 NFRs)                                  | FR-AM-02, T-NFR-02                          | TC-UX-001 to 003                       | UAT-UX-001 to 003                                            | 0             | 3               | 0              |
| O-08: Management Reporting       | RPT-01 to 07 (7 RPTs)                                              | FR-RPT-01 to 06                             | TC-RPT-001 to 007                      | UAT-RPT-001 to 005                                           | 0             | 6               | 1              |
| TOTAL                            | 44 Business Requirements                                           | 65 FRs in FRD v1.2 (44 BRs/controls traced) | 55 TC IDs                              | 43 UAT IDs                                                   | 31            | 12              | 1              |

**4.2 Module Coverage**

|            |                        |                                                |                                 |
|------------|------------------------|------------------------------------------------|---------------------------------|
| **Module** | **Name**               | **Requirements Covered**                       | **Key FR IDs**                  |
| MOD-01     | Patient Registration   | BR-REQ-PR-01 to 05, DPDP-01/02                 | FR-PR-01 to 05, FR-SEC-01/02    |
| MOD-02     | Appointment Management | BR-REQ-APT-01 to 05                            | FR-APT-01 to 06                 |
| MOD-03     | Doctor Dashboard       | BR-REQ-CLN-01/02/04/05, HIPAA-06               | FR-CLN-01 to 06, FR-SEC-06      |
| MOD-04     | Clinician Panel        | BR-REQ-CLN-03                                  | FR-CLN-07 to 10                 |
| MOD-05     | Receptionist Desk      | BR-REQ-APT-02/04                               | FR-REC-01 to 03                 |
| MOD-06     | System Admin Dashboard | BR-REQ-IT-01/03                                | FR-IT-01, FR-IT-03, FR-IT-04    |
| MOD-07     | Patient Portal         | BR-REQ-PR-04, BR-PAT-07 to 09, DPDP-01         | FR-PAT-01 to 08                 |
| MOD-08     | Dean/Admin Dashboard   | RPT-01 to 07                                   | FR-RPT-01 to 06                 |
| MOD-09     | Access Management      | BR-REQ-AM-01 to 04, DPDP-07, HIPAA-05, GDPR-06 | FR-AM-01 to 09, FR-SEC-03 to 10 |
| MOD-10     | Audit & Compliance Log | BR-REQ-IT-02, HIPAA-02                         | FR-AUD-01 to 04, FR-IT-02       |

**4.3 Change Request CR-001 Coverage**

|            |                                          |                                                     |                                            |                      |                       |
|------------|------------------------------------------|-----------------------------------------------------|--------------------------------------------|----------------------|-----------------------|
| **CR ID**  | **Change**                               | **New BRs**                                         | **New FRs**                                | **New TCs**          | **New UATs**          |
| CVH-CR-001 | Patient Self-Registration added to scope | BR-PAT-07, BR-PAT-08, BR-PAT-09, BR-SEC-02 (reused) | FR-PAT-05, FR-PAT-06, FR-PAT-07, FR-PAT-08 | TC-PAT-SR-001 to 004 | UAT-PAT-SR-001 to 004 |

## 5. End-to-End Traceability Examples
|                                    |                                                                            |
|------------------------------------|----------------------------------------------------------------------------|
| **Domain**                         | **Traceability Chain**                                                     |
| Patient Registration               | O-01 → BR-REQ-PR-01 → FR-PR-01 → MOD-01 → TC-PR-001 → UAT-PR-001           |
| Patient Self-Registration (CR-001) | O-01 → BR-PAT-07 → FR-PAT-05 → MOD-07 → TC-PAT-SR-001 → UAT-PAT-SR-001     |
| Appointment Conflict Prevention    | O-02 → BR-REQ-APT-01 → FR-APT-01 → MOD-02 → TC-APT-001 → UAT-APT-001       |
| Consultation Note Integrity        | O-03 → BR-REQ-CLN-04 → FR-CLN-05 → MOD-03 → TC-CLN-004 → UAT-CLN-004       |
| Clinician Vitals Recording         | O-03 → BR-REQ-CLN-03 → FR-CLN-07 to 10 → MOD-04 → TC-CLN-003 → UAT-CLN-003 |
| Access Control Enforcement         | O-04 → BR-REQ-AM-02 → FR-AM-02 → MOD-09 → TC-AM-002 → UAT-AM-002           |
| Audit Log Completeness             | O-05 → BR-REQ-IT-02 → FR-AUD-01 → MOD-10 → TC-IT-002 → UAT-IT-002          |
| DPDP Consent Compliance            | O-06 → DPDP-01 → FR-PR-03 → MOD-01 → TC-SEC-001 → UAT-SEC-001              |
| Management Reporting               | O-08 → RPT-04 → FR-RPT-04 → MOD-08 → TC-RPT-004 → UAT-RPT-004              |

**END OF DOCUMENT**


</div>