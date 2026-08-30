---
hide:
  - toc
---

<div class="ba-meta-bar" markdown>
<span class="ba-badge ba-badge--id">CVH-CR-001</span> <span class="ba-badge ba-badge--version">Version 1.0</span> <span class="ba-badge ba-badge--status">Approved</span> <span class="ba-badge ba-badge--compliance">DPDP / HIPAA / GDPR</span>
</div>

# Change Request CR-001 - Patient Self-Registration

<div class="ba-table-scroll" markdown>

|             |                                                        |
|-------------|--------------------------------------------------------|
| Document ID | CVH-CR-001                                             |
| Version     | 1.0                                                    |
| Date        | July 2026                                              |
| Raised By   | Prashant Gore — BA & Digital Transformation Consultant |
| Change Type | Scope Addition — New Functional Capability             |
| Priority    | High — affects patient portal usability                |
| **Status**  | **Approved — Pending Implementation**                  |

## 1. Change Summary
|                        |                                                                                                                                                                                                                                                                                                                                     |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Field**              | **Detail**                                                                                                                                                                                                                                                                                                                          |
| Change Request ID      | CVH-CR-001                                                                                                                                                                                                                                                                                                                          |
| Change Title           | Patient Self-Registration and Portal Account Creation                                                                                                                                                                                                                                                                               |
| Originating Document   | CVH-BRD-001 v1.2 — Section 7.2 (Out of Scope)                                                                                                                                                                                                                                                                                       |
| Change Trigger         | Prototype testing revealed that patients have no mechanism to independently access the patient portal without System Administrator intervention, creating an operational bottleneck inconsistent with a modern hospital digital experience.                                                                                         |
| Business Justification | Current design requires Reception to register patients AND System Administrator to manually create and link portal accounts. This two-step administrative process is not scalable and degrades patient experience. Enabling patient self-registration aligns with ABDM/NDHM digital health principles and improves portal adoption. |

## 2. Current State vs Proposed State
|                           |                                                                           |                                                                    |
|---------------------------|---------------------------------------------------------------------------|--------------------------------------------------------------------|
| **Aspect**                | **Current State (v1.2)**                                                  | **Proposed State (Post-CR-001)**                                   |
| Patient registration      | Receptionist only — MOD-01                                                | Receptionist OR patient self-registration via public signup page   |
| Portal account creation   | System Administrator manually creates account and links to patient record | Auto-created on self-registration; no admin intervention required  |
| Patient ID generation     | Receptionist triggers — MOD-01                                            | System-generated on self-registration (same CVH-YYYY-NNNNN format) |
| First appointment booking | Receptionist books on patient behalf                                      | Receptionist books OR patient requests via portal (future Phase 2) |
| Consent capture           | At reception desk                                                         | During self-registration form (same DPDP/GDPR consent language)    |
| Password                  | System Administrator sets temporary password                              | Patient sets own password during self-registration                 |

## 3. Impact Assessment
**3.1 Affected Documents**

|                                  |             |                                                                                  |                                                      |
|----------------------------------|-------------|----------------------------------------------------------------------------------|------------------------------------------------------|
| **Document**                     | **ID**      | **Change Required**                                                              | **Sections Affected**                                |
| Business Requirements Document   | CVH-BRD-001 | Amendment — Section 7.1 (In-Scope), Section 7.2 (Out-of-Scope), Section 10 (FRs) | MOD-07 scope, BR-REQ-PAT new entries, Business Rules |
| Functional Requirements Document | CVH-FRD-001 | Amendment — MOD-07 section, Use Case UC-05 added                                 | Section 10 (MOD-07), UC-05, FR-PAT additions         |
| Requirements Traceability Matrix | CVH-RTM-001 | Amendment — new rows for CR-001 requirements                                     | Section 3 main matrix, Section 4 coverage summary    |
| System Test Cases                | CVH-STC-001 | Minor — new TC-PAT entries for self-registration                                 | Section 6 (Patient scenarios)                        |
| UAT Scripts                      | CVH-UAT-001 | Minor — new UAT-PAT scenario                                                     | Section 6 (Patient scenarios)                        |
| Prototype                        | CVH-DEV-001 | Code change — mod\_07.py, app.py                                                 | Self-registration page, public route                 |

**3.2 No Impact**

The following documents require NO changes: ERD (no new tables — patients and users tables already support this), SQD (existing auth flow covers new registration), RTM structure unchanged.

## 4. New Requirements — CR-001 Additions
**4.1 BRD Amendments**

The following items are ADDED to CVH-BRD-001 v1.2:

**Section 7.1 (In-Scope) — MOD-07 revised description:**

|                        |                                                                                                                                                          |                                            |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| **Module**             | **Revised Description**                                                                                                                                  | **Primary User**                           |
| MOD-07: Patient Portal | Patient self-service: self-registration with account creation, view appointments, access discharge summaries, update contact details, consent management | Patient (self-registered or admin-created) |

**Section 7.2 (Out of Scope) — Item REMOVED:**

*Remove: 'Patient self-registration' — this is now In-Scope per CVH-CR-001.*

**New Business Rules (Section 9) — ADDED:**

|             |                                                                                                                                                                                                                                                                     |
|-------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Rule ID** | **Business Rule**                                                                                                                                                                                                                                                   |
| BR-PAT-07   | A patient may self-register via the public portal signup page without requiring Receptionist or System Administrator action.                                                                                                                                        |
| BR-PAT-08   | Self-registered patients shall provide: Full Name, Date of Birth, Mobile Number, Gender, and confirm data processing consent. All standard duplicate-detection rules (BR-PAT-02) apply.                                                                             |
| BR-PAT-09   | On successful self-registration, the system shall automatically generate a Patient ID (CVH-YYYY-NNNNN), create a portal login account with the patient's mobile number as username, and require the patient to set a password meeting complexity rules (BR-SEC-02). |
| BR-PAT-10   | Self-registered patients may view their own appointments and portal information. Appointment booking remains a Receptionist function in this phase.                                                                                                                 |
| BR-PAT-11   | A patient who self-registers and subsequently visits in person shall be identified via the duplicate detection rule (BR-PAT-02). The Receptionist may link the walk-in visit to the existing self-registered record.                                                |

**4.2 FRD Amendments**

The following are ADDED to CVH-FRD-001 v1.1:

**New Use Case — UC-05: Patient Self-Registration**

|                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Element**      | **Detail**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Use Case ID      | UC-05                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Use Case Name    | Patient Self-Registration                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Actor            | Unregistered Patient (unauthenticated)                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Preconditions    | Patient has not previously registered. Application signup page is publicly accessible without login.                                                                                                                                                                                                                                                                                                                                                                                                      |
| Trigger          | Patient navigates to the portal and selects 'New Patient? Register Here'.                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Normal Flow      | 1\. Patient completes signup form: Full Name, DOB, Gender, Mobile, Email (optional), Password. 2. Patient confirms data processing consent. 3. System performs duplicate check (Name + DOB + Mobile). 4. No duplicate: system generates Patient ID, creates user account (username=mobile, role=Patient), links account to patient record. 5. Patient is automatically logged in and redirected to MOD-07 Patient Portal. 6. CREATE events logged to audit\_log for both patient record and user account. |
| Alternate Flow 1 | Duplicate detected: System informs patient a record may exist. Advises them to contact Reception to retrieve their Patient ID and request portal access.                                                                                                                                                                                                                                                                                                                                                  |
| Alternate Flow 2 | Password does not meet complexity rules: specific error message shown per BR-SEC-02. Form not submitted.                                                                                                                                                                                                                                                                                                                                                                                                  |
| Post-Conditions  | Patient record exists in patients table. Portal account exists in users table with role=Patient. Patient is logged in and can view MOD-07.                                                                                                                                                                                                                                                                                                                                                                |
| Exceptions       | Database error: generic error shown. No partial record written (transaction rollback).                                                                                                                                                                                                                                                                                                                                                                                                                    |

**New Functional Requirements — ADDED to MOD-07 section:**

|           |                                                                                                                                                               |               |              |                                                                                            |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------|--------------------------------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                                                                                    | **BR Source** | **Priority** | **Testability**                                                                            |
| FR-PAT-05 | System shall provide a publicly accessible self-registration page (no login required) linked from the main login screen.                                      | BR-PAT-07     | Must Have    | Access login page → verify 'Register' link visible without authentication                  |
| FR-PAT-06 | Self-registration form shall capture: Full Name, DOB, Gender, Mobile, Email (optional), Password, Consent. Duplicate detection (Name+DOB+Mobile) shall apply. | BR-PAT-08     | Must Have    | Register with existing Name+DOB+Mobile → duplicate warning shown                           |
| FR-PAT-07 | On successful self-registration, system shall auto-generate Patient ID, create portal account (username=mobile number, role=Patient), and log in the patient. | BR-PAT-09     | Must Have    | Complete registration → verify Patient ID generated, account created, auto-login to MOD-07 |
| FR-PAT-08 | Password set during self-registration shall meet complexity rules (BR-SEC-02). Inline error shown on failure.                                                 | BR-SEC-02     | Must Have    | Enter weak password → verify rejected with specific error message                          |

**4.3 RTM Additions**

|            |                               |           |                                             |           |            |              |               |                |            |
|------------|-------------------------------|-----------|---------------------------------------------|-----------|------------|--------------|---------------|----------------|------------|
| **Obj ID** | **Business Objective**        | **BR ID** | **BR Summary**                              | **FR ID** | **Module** | **Priority** | **TC ID**     | **UAT ID**     | **Status** |
| O-01       | Digitise patient registration | BR-PAT-07 | Patient self-registration via public portal | FR-PAT-05 | MOD-07     | Must Have    | TC-PAT-SR-001 | UAT-PAT-SR-001 | Planned    |
| O-01       |                               | BR-PAT-08 | Self-reg form with duplicate detection      | FR-PAT-06 | MOD-07     | Must Have    | TC-PAT-SR-002 | UAT-PAT-SR-002 | Planned    |
| O-01       |                               | BR-PAT-09 | Auto Patient ID + account + auto-login      | FR-PAT-07 | MOD-07     | Must Have    | TC-PAT-SR-003 | UAT-PAT-SR-003 | Planned    |
| O-04       | Deploy RBAC                   | BR-SEC-02 | Password complexity on self-registration    | FR-PAT-08 | MOD-07     | Must Have    | TC-PAT-SR-004 | UAT-PAT-SR-004 | Planned    |

## 5. Change Approval
|                       |               |                    |           |                                |
|-----------------------|---------------|--------------------|-----------|--------------------------------|
| **Role**              | **Name**      | **Decision**       | **Date**  | **Signature**                  |
| Dean / Business Owner | Dr. \[Name\]  | ☐ Approve ☐ Reject |           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |
| Business Analyst      | Prashant Gore | Approved           | July 2026 | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |
| Developer             | TBD           | ☐ Approve ☐ Reject |           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |

**END OF DOCUMENT**


</div>