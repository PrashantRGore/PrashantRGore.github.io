---
hide:
  - toc
---

<div class="ba-meta-bar">
<span class="ba-badge ba-badge--id">CVH-BRD-001</span>
<span class="ba-badge ba-badge--version">Version 1.3</span>
<span class="ba-badge ba-badge--status">Baselined</span>
<span class="ba-badge ba-badge--compliance">DPDP / HIPAA / GDPR</span>
</div>

# Business Requirements Document (BRD)

|              |                                                                       |
|--------------|-----------------------------------------------------------------------|
| Document ID  | CVH-BRD-001                                                           |
| Version      | 1.3 – CR-001 Amendment (Patient Self-Registration)                    |
| Date         | July 2026                                                             |
| Prepared By  | Prashant Gore – Business Analyst & Digital Transformation Consultant  |
| Status       | DRAFT – Under Review                                                  |
| Client       | ClearVision Eye Hospital – Office of the Dean                         |
| Jurisdiction | India (Primary: DPDP Act 2023) \| Reference: HIPAA \| Reference: GDPR |
| Change Ref   | CVH-CR-001 – Patient Self-Registration added to scope                 |

> *DISCLAIMER: Prototype demonstration project only. No real patient data. Not for production clinical deployment.*

## 1. Document Control
**1.1 Version History**

|             |           |               |                                                                                                                          |            |
|-------------|-----------|---------------|--------------------------------------------------------------------------------------------------------------------------|------------|
| **Version** | **Date**  | **Author**    | **Description**                                                                                                          | **Status** |
| 1.0         | June 2026 | Prashant Gore | Initial BRD                                                                                                              | Superseded |
| 1.1         | June 2026 | Prashant Gore | Post Senior BA Review: Business Case, Business Rules, Risks, Compliance, Reporting added                                 | Superseded |
| 1.2         | June 2026 | Prashant Gore | Second revision: System Administrator terminology; BR-PAT-02 combination logic; Data Dictionary appendix added           | Superseded |
| 1.3         | July 2026 | Prashant Gore | CVH-CR-001: Patient self-registration added to scope; MOD-07 revised; BR-PAT-07 to BR-PAT-11 added; Out of Scope updated | Draft      |

**1.2 Document Approvals**

|                       |               |                                    |           |
|-----------------------|---------------|------------------------------------|-----------|
| **Role**              | **Name**      | **Signature**                      | **Date**  |
| Dean / Business Owner | Dr. \[Name\]  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| Business Analyst      | Prashant Gore | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | July 2026 |
| IT Lead               | TBD           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| Compliance Officer    | TBD           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| Information Security  | TBD           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |

**1.3 Document Purpose**

This BRD defines WHAT the business of ClearVision Eye Hospital requires. It does not prescribe HOW the solution shall be technically implemented. Technology platform specifics are documented in the FRD (CVH-FRD-001 v1.2).

## 2. Executive Summary
ClearVision Eye Hospital currently operates through manual processes and disconnected workflows. The Dean has initiated a digital transformation programme commissioning a Hospital Management and Patient Experience Portal. This BRD captures business needs, stakeholder requirements, compliance obligations, business rules, and scope boundaries. It is the single source of truth for all downstream documents including FRD, RTM, User Stories, UAT Test Plan, and STC.

## 3. Business Problem Statement
**3.1 Current State (As-Is)**

-   Patient registration is manual — 20–25 minute average wait; data duplication errors common.

-   Appointment scheduling relies on spreadsheets — no conflict detection or digital tracking.

-   Doctor availability not centrally managed — over-booking and idle slots result.

-   Clinical documentation is paper-based — no audit trail; disconnected from patient records.

-   No access control — any staff can access any record; regulatory exposure.

-   IT department has no visibility of system activity or security events.

-   Discharge, billing, and follow-up workflows are fully manual.

**3.2 Business Impact Assessment**

|                                   |                                                       |              |                               |
|-----------------------------------|-------------------------------------------------------|--------------|-------------------------------|
| **Pain Point**                    | **Business Impact**                                   | **Severity** | **Affected Stakeholder**      |
| Manual patient registration       | 20–25 min average wait; data duplication              | Critical     | Patients, Receptionist        |
| No digital appointment management | Missed appointments; double-bookings; revenue leakage | Critical     | Patients, Doctors, Admin      |
| Paper clinical records            | Medical error risk; no audit trail                    | Critical     | Doctors, Clinicians, Patients |
| No access control                 | Regulatory non-compliance risk                        | Critical     | All users, Compliance         |
| No IT monitoring                  | Zero security visibility                              | High         | IT Staff, Compliance          |
| Manual billing/discharge          | Delayed collections; reconciliation errors            | High         | Admin, Finance                |

**3.3 Desired Future State (To-Be)**

-   Instant digital patient registration — self-registration or Receptionist-driven — with unique Patient ID.

-   Real-time appointment scheduling with automated conflict prevention and status tracking.

-   Structured electronic clinical documentation linked to patient profiles with full audit trail.

-   Granular RBAC enforcing minimum necessary access principles.

-   IT Administrator visibility of system activity and security events.

-   Compliance-aligned data handling referencing DPDP Act 2023, HIPAA, and GDPR.

-   Management-level operational and compliance reporting dashboards.

## 4. Business Case
**4.1 Strategic Alignment**

-   Patient-Centric Care: Reduce friction across all patient touchpoints.

-   Operational Excellence: Eliminate manual bottlenecks and administrative errors.

-   Regulatory Readiness: Demonstrate compliance posture under applicable regulations.

-   Digital Maturity: Foundation for future AI, PACS, and HL7/FHIR integration.

**4.2 Anticipated Business Benefits**

|                           |                      |                       |                                |
|---------------------------|----------------------|-----------------------|--------------------------------|
| **Benefit**               | **Baseline (As-Is)** | **Target**            | **Measurement**                |
| Patient registration time | 20–25 minutes        | &lt; 3 minutes        | Timed UAT                      |
| Appointment utilisation   | \~65% (manual gaps)  | ≥ 90%                 | Booking vs slot ratio          |
| Duplicate patient records | Uncontrolled         | Zero duplicates       | Validation rule enforcement    |
| Data access compliance    | No controls          | Full RBAC enforcement | Access audit log review        |
| Management reporting      | Manual, ad hoc       | Automated dashboards  | Report generation verification |

**4.3 Project Costs**

All tools, frameworks, and libraries are free and open-source. No monetary investment required. No paid subscriptions at any stage of the prototype.

## 5. Project Objectives & Success Criteria
**5.1 Primary Objectives**

|            |                                           |                                              |             |                                   |
|------------|-------------------------------------------|----------------------------------------------|-------------|-----------------------------------|
| **Obj ID** | **Objective**                             | **Measurable Outcome**                       | **MoSCoW**  | **Rationale**                     |
| O-01       | Digitise patient registration             | Registration time &lt;3 min; zero duplicates | Must Have   | Primary patient experience driver |
| O-02       | Implement appointment management          | Zero double-bookings; 100% digital           | Must Have   | Core operational requirement      |
| O-03       | Enable electronic clinical documentation  | All records digital with full audit trail    | Must Have   | Patient safety + compliance       |
| O-04       | Deploy Role-Based Access Control          | Each user accesses only designated modules   | Must Have   | Regulatory obligation             |
| O-05       | Build IT admin and compliance monitoring  | System activity visible to IT Admin          | Should Have | Operational governance            |
| O-06       | Implement compliance-aware data practices | DPDP/HIPAA/GDPR controls demonstrated        | Must Have   | Portfolio + regulatory            |
| O-07       | Deliver role-appropriate user experience  | Positive UAT feedback from all roles         | Should Have | User adoption enabler             |
| O-08       | Management reporting dashboards           | Operational KPIs visible to Dean             | Should Have | Strategic decision-making         |

**5.2 Project Success Criteria**

|        |                                                   |                            |
|--------|---------------------------------------------------|----------------------------|
| **ID** | **Success Criterion**                             | **Verification Method**    |
| SC-01  | All user roles access only designated modules     | Role-segregated UAT        |
| SC-02  | Patient registration completed in &lt;3 minutes   | Timed UAT                  |
| SC-03  | Zero double-bookings in scheduling testing        | Negative UAT test          |
| SC-04  | Clinical records stored with user + timestamp     | UAT + DB record inspection |
| SC-05  | All user actions captured in audit log            | Audit log review post-UAT  |
| SC-06  | Compliance controls implemented as per Section 12 | Compliance walkthrough     |
| SC-07  | UAT sign-off from at least one rep per role group | Signed UAT form            |

## 6. Stakeholder Register
**6.1 Stakeholder Identification & RACI**

|        |                                  |                            |                                                    |                      |                     |
|--------|----------------------------------|----------------------------|----------------------------------------------------|----------------------|---------------------|
| **ID** | **Stakeholder / Group**          | **Role**                   | **Interest / Concern**                             | **RACI**             | **Scope Status**    |
| S-01   | Dean                             | Business Owner / Sponsor   | Efficiency, patient experience, compliance, budget | Accountable          | In Scope            |
| S-02   | Patients                         | End User (External)        | Registration, appointments, data privacy           | Consulted / Informed | In Scope            |
| S-03   | Receptionist                     | End User (Internal)        | Simplified workflows, reduced manual effort        | Consulted            | In Scope            |
| S-04   | Doctors / Ophthalmologists       | End User (Clinical)        | Patient history, documentation, scheduling         | Consulted            | In Scope            |
| S-05   | Clinicians / Nurses              | End User (Clinical)        | Vitals entry, procedure tracking                   | Consulted            | In Scope            |
| S-06   | IT Staff / System Administrator  | End User + Technical Owner | Access control, security, system health            | Responsible          | In Scope            |
| S-07   | Hospital Administration          | Internal Stakeholder       | Reporting, billing oversight                       | Consulted            | In Scope            |
| S-08   | Finance / Billing                | Internal Stakeholder       | Revenue tracking, billing accuracy                 | Informed             | Future Scope        |
| S-09   | Medical Records                  | Internal Stakeholder       | Record integrity, archival compliance              | Informed             | Future Scope        |
| S-10   | Compliance Committee             | Governance                 | Regulatory alignment, audit readiness              | Consulted            | In Scope            |
| S-11   | Information Security             | Technical Governance       | Access controls, incident response                 | Consulted            | In Scope            |
| S-12   | Legal                            | Risk & Liability           | Data breach liability, consent validity            | Informed             | In Scope (Advisory) |
| S-13   | Pharmacy                         | Internal Stakeholder       | Prescription fulfilment, dispensing                | Informed             | Future Scope        |
| S-14   | Patients' Representatives        | External Governance        | Patient rights, accessibility, grievance           | Informed             | Future Scope        |
| S-15   | Business Analyst (Prashant Gore) | Delivery – BA Lead         | Requirements, documentation, UAT                   | Responsible          | In Scope            |
| S-16   | Developer                        | Delivery – Technical       | Architecture, build, deployment                    | Responsible          | In Scope            |

## 7. Project Scope
**7.1 In-Scope Modules**

|               |                        |                                                                                                                                   |                                            |
|---------------|------------------------|-----------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------|
| **Module ID** | **Module Name**        | **Description**                                                                                                                   | **Primary User Group**                     |
| MOD-01        | Patient Registration   | Digital patient onboarding (Receptionist-driven); unique ID; medical history; consent capture                                     | Receptionist / Dean-Admin                  |
| MOD-02        | Appointment Management | Calendar booking; conflict prevention; status tracking; queue management                                                          | Receptionist / Patient / Doctor            |
| MOD-03        | Doctor Dashboard       | Schedule view; patient record access; consultation notes; e-prescription                                                          | Doctor                                     |
| MOD-04        | Clinician Panel        | Vitals recording; pre/post-procedure notes; assigned patient list                                                                 | Clinician / Nurse                          |
| MOD-05        | Receptionist Desk      | Check-in/out; queue management; appointment modification                                                                          | Receptionist                               |
| MOD-06        | System Admin Dashboard | User management; RBAC configuration; audit log viewer; system health                                                              | System Administrator                       |
| MOD-07        | Patient Portal         | Self-registration; view appointments; access discharge summaries; update contact; consent management (CVH-CR-001: self-reg added) | Patient (self-registered or admin-created) |
| MOD-08        | Dean / Admin Dashboard | Operational KPIs; reporting; compliance status                                                                                    | Dean / Administration                      |
| MOD-09        | Access Management      | Authentication; session management; RBAC enforcement across all modules                                                           | All Users / IT Staff                       |
| MOD-10        | Audit & Compliance Log | System-wide activity logging supporting regulatory audit requirements                                                             | System Administrator / Compliance          |

**7.2 Out of Scope**

-   Real-time integration with laboratory or radiology information systems (LIS/RIS/PACS)

-   Insurance claim processing or third-party payer integrations

-   Telemedicine or video consultation functionality

-   Native mobile application (iOS or Android) — web-responsive prototype only

-   Pharmacy dispensing and inventory management

-   Payroll, HR, or financial reporting modules

-   Real patient data — all prototype data is synthetically generated

-   Production infrastructure, cloud hosting, or enterprise deployment

*Note: Patient self-registration was previously Out of Scope. This was moved In-Scope per CVH-CR-001 (July 2026).*

**7.3 Future Scope (Phase 2+)**

|                                             |                                   |           |
|---------------------------------------------|-----------------------------------|-----------|
| **Future Capability**                       | **Business Driver**               | **Phase** |
| AI-assisted triage and diagnosis support    | Clinical decision support         | Phase 2   |
| HL7/FHIR integration (interoperability)     | ABDM/NDHM compliance              | Phase 2   |
| PACS integration for imaging                | Link radiology to patient records | Phase 2   |
| Mobile application (iOS/Android)            | Patient mobility and self-service | Phase 3   |
| Telemedicine / video consultation           | Remote patient access             | Phase 3   |
| Insurance and third-party payer integration | Revenue cycle management          | Phase 3   |
| Pharmacy and inventory management           | End-to-end clinical workflow      | Phase 2   |
| National Health ID (ABHA) integration       | ABDM compliance for India         | Phase 2   |
| Advanced analytics and AI dashboards        | Predictive capacity planning      | Phase 3   |

## 8. Prototype Scope & Known Limitations
|        |                         |                                   |                                                      |
|--------|-------------------------|-----------------------------------|------------------------------------------------------|
| **ID** | **Area**                | **Prototype Behaviour**           | **Production Requirement**                           |
| PL-01  | Data Encryption         | Not encrypted at rest             | AES-256 at rest; TLS in transit                      |
| PL-02  | MFA                     | Simulated (UI demonstration only) | Live MFA via authenticator app or SMS OTP            |
| PL-03  | Email/SMS Notifications | Triggers logged only; not sent    | Integration with approved SMS/email gateway          |
| PL-04  | Data Volume             | Synthetic small dataset           | Production load testing required                     |
| PL-05  | Concurrency             | Single-user prototype sessions    | Multi-user concurrent access with session management |
| PL-06  | Database                | Lightweight local DB              | Enterprise DB with backup, replication, failover     |
| PL-07  | Audit Retention         | Local DB; no auto-purge           | Automated retention with purge schedule              |
| PL-08  | Accessibility           | Basic usability                   | Full WCAG 2.1 AA compliance validation               |
| PL-09  | Browser Compatibility   | Modern browsers only              | Cross-browser and device testing                     |
| PL-10  | Real PHI                | Synthetic data only               | Full data governance and PHI handling protocols      |

## 9. Business Rules
**9.1 Patient Management Rules**

|             |                                                                                                                                                                                                     |
|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Rule ID** | **Business Rule**                                                                                                                                                                                   |
| BR-PAT-01   | A patient's Date of Birth must result in an age between 0 and 120 years. Negative age is not permitted.                                                                                             |
| BR-PAT-02   | Duplicate detection uses a combination of Full Name + Date of Birth + Mobile Number. Mobile number or email alone shall NOT trigger a duplicate alert, as family members may share contact details. |
| BR-PAT-03   | A Patient ID, once generated, shall never be modified or reused, even if the patient record is deactivated.                                                                                         |
| BR-PAT-04   | Patient demographic data may only be edited by Receptionist or Dean-Admin roles. Doctors and Clinicians have read-only access to demographics.                                                      |
| BR-PAT-05   | Patient consent for data processing must be captured and recorded at the point of registration or self-registration. Registration shall not be completed without consent.                           |
| BR-PAT-06   | A patient record may be deactivated but not permanently deleted via the standard interface. Permanent deletion requires a formal Right to Erasure request processed by System Administrator.        |
| BR-PAT-07   | A patient may self-register via the public portal signup page without Receptionist or System Administrator action. (Added: CVH-CR-001)                                                              |
| BR-PAT-08   | Self-registering patients shall provide: Full Name, Date of Birth, Mobile Number, Gender, and data processing consent. Duplicate detection (BR-PAT-02) applies.                                     |
| BR-PAT-09   | On successful self-registration, the system shall auto-generate a Patient ID (CVH-YYYY-NNNNN), create a portal account (username=mobile, role=Patient), and log in the patient automatically.       |
| BR-PAT-10   | Self-registered patients may view appointments and portal information. Appointment booking remains a Receptionist function in the current phase.                                                    |
| BR-PAT-11   | A patient who self-registers and subsequently visits in person shall be identified via duplicate detection (BR-PAT-02). The Receptionist may link the visit to the existing self-registered record. |

**9.2 Appointment Rules**

|             |                                                                                                                                                      |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Rule ID** | **Business Rule**                                                                                                                                    |
| BR-APT-01   | A doctor shall not be booked for more than one appointment in the same time slot. Conflict detection mandatory.                                      |
| BR-APT-02   | Standard appointment duration is 20 minutes. Time slots allocated in 20-minute blocks.                                                               |
| BR-APT-03   | A doctor shall not exceed the configured maximum appointments per day (default: 24 per 8-hour day; configurable by System Administrator).            |
| BR-APT-04   | One patient shall not hold more than one active (Scheduled) appointment with the same doctor on the same date.                                       |
| BR-APT-05   | Emergency appointments may be inserted outside normal queue order. Only Receptionist and Doctor roles may designate an appointment as Emergency.     |
| BR-APT-06   | Appointment cancellation must capture a mandatory reason. Cancellations within 1 hour of the appointment time shall be flagged as Late Cancellation. |
| BR-APT-07   | Walk-in patients shall be accommodated via a Walk-In designation. Walk-in queue managed separately from pre-booked appointments.                     |
| BR-APT-08   | Appointments cannot be booked on dates designated as hospital holidays or closed hours. Configurable by System Administrator.                        |
| BR-APT-09   | A No-Show status shall be assigned to appointments where the patient has not checked in within 15 minutes of the scheduled time.                     |

**9.3 Clinical Documentation Rules**

|             |                                                                                                                                           |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Rule ID** | **Business Rule**                                                                                                                         |
| BR-CLN-01   | Consultation notes may only be entered by the treating Doctor assigned to that appointment.                                               |
| BR-CLN-02   | Consultation notes are editable for 24 hours from the time of entry. After 24 hours, records become read-only to protect audit integrity. |
| BR-CLN-03   | A prescription shall not be issued without a corresponding consultation note being saved.                                                 |
| BR-CLN-04   | Vitals may be entered only by Clinician and Nurse roles. Doctors have read-only access to vitals.                                         |
| BR-CLN-05   | Investigation orders shall be linked to the specific patient visit. An investigation order without a linked visit is not permitted.       |

**9.4 Access and Security Rules**

|             |                                                                                                                                                                                            |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Rule ID** | **Business Rule**                                                                                                                                                                          |
| BR-SEC-01   | Each system user shall have a unique username. Shared credentials are not permitted.                                                                                                       |
| BR-SEC-02   | Passwords shall meet minimum complexity: minimum 8 characters, at least one uppercase letter, one numeral, and one special character. Applies to all accounts including self-registration. |
| BR-SEC-03   | Passwords shall expire every 90 days. Users prompted to reset on login after expiry.                                                                                                       |
| BR-SEC-04   | An account shall be automatically locked after 3 consecutive failed login attempts. Only System Administrator may unlock.                                                                  |
| BR-SEC-05   | User sessions shall expire after 15 minutes of inactivity. Re-authentication required to resume.                                                                                           |
| BR-SEC-06   | Only one active session per user account permitted at any time.                                                                                                                            |
| BR-SEC-07   | Inactive user accounts (no login for 90 days) shall be flagged and suspended pending System Administrator review.                                                                          |
| BR-SEC-08   | A patient's consent may be withdrawn at any time. Upon withdrawal, the record shall be flagged and access restricted pending compliance review.                                            |

## 10. Functional Requirements
*Requirements in business language. MoSCoW prioritised. Detailed system behaviour in FRD (CVH-FRD-001 v1.2).*

*Prioritisation Rationale: Must Have = regulatory/safety/core operational. Should Have = significant value, not MVP blocker. Could Have = desirable enhancement.*

**10.1 Patient Registration (MOD-01)**

|              |                                                                                                                    |              |                                                                               |                                                                                                                                       |
|--------------|--------------------------------------------------------------------------------------------------------------------|--------------|-------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **Req ID**   | **Business Requirement**                                                                                           | **Priority** | **Rationale**                                                                 | **Acceptance Criteria**                                                                                                               |
| BR-REQ-PR-01 | Business requires digital patient registration capturing all clinically and administratively relevant information. | Must Have    | Eliminates paper registration; reduces wait time.                             | Patient record created; mandatory fields validated; Patient ID generated; record retrievable.                                         |
| BR-REQ-PR-02 | Business requires unique patient identification to prevent duplicate records.                                      | Must Have    | Duplicate records cause clinical risk and billing errors.                     | System warns if Full Name + DOB + Mobile combination matches existing record. Mobile or email alone does NOT trigger duplicate alert. |
| BR-REQ-PR-03 | Business requires patient consent to data processing captured at point of registration.                            | Must Have    | DPDP Act 2023 / GDPR Article 7 obligation.                                    | Consent flag recorded; registration not completable without consent.                                                                  |
| BR-REQ-PR-04 | Business requires ability to retrieve and update patient records post-registration.                                | Must Have    | Demographics change over time; clinical accuracy requirement.                 | Record searchable by Patient ID, name, or mobile; updates save correctly.                                                             |
| BR-REQ-PR-05 | Business requires capture of ophthalmology-relevant medical history at registration.                               | Must Have    | Doctors require prior conditions, allergies, medications before consultation. | Medical history visible in Doctor Dashboard.                                                                                          |

**10.2 Appointment Management (MOD-02)**

|               |                                                             |              |                                                       |                                                                                                   |
|---------------|-------------------------------------------------------------|--------------|-------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **Req ID**    | **Business Requirement**                                    | **Priority** | **Rationale**                                         | **Acceptance Criteria**                                                                           |
| BR-REQ-APT-01 | Digital appointment scheduling with real-time availability. | Must Have    | Eliminates double-bookings and manual errors.         | Appointments bookable; conflict detected and rejected; availability real-time.                    |
| BR-REQ-APT-02 | Appointment status tracked across full patient journey.     | Must Have    | Enables queue management and operational reporting.   | Status transitions (Scheduled→Checked-In→In-Progress→Completed/Cancelled/No-Show) work correctly. |
| BR-REQ-APT-03 | Emergency and walk-in accommodation outside standard queue. | Must Have    | Clinical priority; patient safety obligation.         | Emergency and Walk-In types available; queue adjustable by authorised role.                       |
| BR-REQ-APT-04 | Cancellation and reschedule with mandatory reason capture.  | Must Have    | Operational requirement; supports no-show analysis.   | Reason mandatory; cancellation and reschedule functions available; audit record created.          |
| BR-REQ-APT-05 | No-show identification and recording.                       | Should Have  | Supports utilisation reporting and capacity planning. | No-Show status auto-assigned per BR-APT-09; reportable.                                           |

**10.3 Clinical Documentation (MOD-03 / MOD-04)**

|               |                                                                             |              |                                                             |                                                                          |
|---------------|-----------------------------------------------------------------------------|--------------|-------------------------------------------------------------|--------------------------------------------------------------------------|
| **Req ID**    | **Business Requirement**                                                    | **Priority** | **Rationale**                                               | **Acceptance Criteria**                                                  |
| BR-REQ-CLN-01 | Treating doctors record structured consultation notes linked to each visit. | Must Have    | Patient safety; continuity of care; regulatory audit.       | Notes saved against correct visit; author and timestamp recorded.        |
| BR-REQ-CLN-02 | Digital prescription linked to consultation record.                         | Must Have    | Replaces paper prescriptions; improves patient safety.      | Prescription linked to consultation; visible to patient on portal.       |
| BR-REQ-CLN-03 | Clinician records patient vitals prior to consultation.                     | Must Have    | Vitals are prerequisite clinical data for treating doctor.  | Vitals recorded by Clinician; visible to Doctor in consultation view.    |
| BR-REQ-CLN-04 | Clinical records maintain immutable audit trail.                            | Must Have    | HIPAA / DPDP compliance; clinical governance.               | Records locked after 24 hours; all access events logged.                 |
| BR-REQ-CLN-05 | Investigation orders raised and linked to patient visit.                    | Should Have  | Clinical workflow continuity; patient history completeness. | Investigation order created; linked to visit; visible in patient record. |

**10.4 Access Management (MOD-09)**

|              |                                                   |              |                                                            |                                                                        |
|--------------|---------------------------------------------------|--------------|------------------------------------------------------------|------------------------------------------------------------------------|
| **Req ID**   | **Business Requirement**                          | **Priority** | **Rationale**                                              | **Acceptance Criteria**                                                |
| BR-REQ-AM-01 | All users authenticated before any portal access. | Must Have    | Fundamental access control and data protection.            | Unauthenticated access to any module not possible.                     |
| BR-REQ-AM-02 | RBAC enforcing minimum necessary access per user. | Must Have    | Regulatory obligation: DPDP Act / HIPAA minimum necessary. | Each role accesses only designated modules; cross-role access denied.  |
| BR-REQ-AM-03 | Session timeout after 15 minutes of inactivity.   | Must Have    | Security obligation aligned with HIPAA access control.     | Sessions expire after 15 min; re-authentication required.              |
| BR-REQ-AM-04 | Account lockout after 3 failed login attempts.    | Must Have    | Security requirement per BR-SEC-04.                        | Account locked at 3 failed attempts; System Administrator unlock only. |

**10.5 System Administration & Audit (MOD-06 / MOD-10)**

|              |                                                                            |              |                                                          |                                                                                  |
|--------------|----------------------------------------------------------------------------|--------------|----------------------------------------------------------|----------------------------------------------------------------------------------|
| **Req ID**   | **Business Requirement**                                                   | **Priority** | **Rationale**                                            | **Acceptance Criteria**                                                          |
| BR-REQ-IT-01 | System Administrator manages user accounts and role assignments centrally. | Must Have    | Governance and access control management.                | System Administrator can create, modify, deactivate accounts and reassign roles. |
| BR-REQ-IT-02 | Complete tamper-evident audit log of all system activity.                  | Must Have    | HIPAA audit control; DPDP Act accountability obligation. | Every user action logged; log is read-only to non-IT roles.                      |
| BR-REQ-IT-03 | System health indicators visible to System Administrator.                  | Should Have  | Operational governance; incident detection.              | Dashboard displays session count, recent errors, database status.                |

**10.6 Patient Portal — Self-Registration (MOD-07, CVH-CR-001)**

|                  |                                                                              |              |                                                                      |                                                                                                      |
|------------------|------------------------------------------------------------------------------|--------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **Req ID**       | **Business Requirement**                                                     | **Priority** | **Rationale**                                                        | **Acceptance Criteria**                                                                              |
| BR-REQ-PAT-SR-01 | Patient self-registration via public portal page without admin intervention. | Must Have    | Removes operational bottleneck; improves patient digital experience. | Patient completes signup; Patient ID auto-generated; portal account created; patient auto-logged in. |
| BR-REQ-PAT-SR-02 | Password set by patient at self-registration must meet complexity rules.     | Must Have    | Security obligation per BR-SEC-02.                                   | Weak password rejected with specific inline error. Strong password accepted.                         |
| BR-REQ-PAT-SR-03 | Duplicate detection applied during self-registration.                        | Must Have    | Prevents duplicate patient records from self-reg path.               | Duplicate Name+DOB+Mobile combination shows warning; patient advised to contact Reception.           |

**10.7 Reporting Requirements (MOD-08)**

|               |                               |                                                      |                                  |                   |
|---------------|-------------------------------|------------------------------------------------------|----------------------------------|-------------------|
| **Report ID** | **Report Name**               | **Description**                                      | **Audience**                     | **Frequency**     |
| RPT-01        | Daily Appointment Summary     | Total appointments by status per day                 | Dean, Admin, Doctors             | Daily             |
| RPT-02        | Doctor Utilisation Report     | Appointments per doctor vs available slots           | Dean, Admin                      | Weekly            |
| RPT-03        | Patient Registration Summary  | New registrations, returning, total active           | Admin                            | Weekly            |
| RPT-04        | No-Show & Cancellation Report | Count and trend of no-shows and late cancellations   | Admin, Dean                      | Weekly            |
| RPT-05        | Audit Activity Report         | Login activity, data access, failed attempts         | System Administrator, Compliance | Daily / On demand |
| RPT-06        | Compliance Status Summary     | Consent flags, access deviations, audit completeness | Compliance Committee, Dean       | Monthly           |
| RPT-07        | Patient Demographics Summary  | Age distribution, gender, visit frequency            | Admin, Dean                      | Monthly           |

## 11. Non-Functional Requirements
*Technology platform specifics excluded — in FRD (CVH-FRD-001 v1.2) Section 17.*

|            |                  |                                                                                                          |                                                                    |
|------------|------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|
| **Req ID** | **Category**     | **Business Requirement**                                                                                 | **Acceptance Criteria**                                            |
| NFR-01     | Performance      | System shall support expected concurrent users without degradation during peak hours.                    | Responsive under simulated concurrent usage during UAT.            |
| NFR-02     | Security         | User credentials stored using industry-standard irreversible hashing.                                    | No plaintext passwords retrievable from any storage.               |
| NFR-03     | Security         | All user actions recorded in tamper-evident audit log accessible only to authorised roles.               | Audit log populated; non-IT roles cannot modify entries.           |
| NFR-04     | Availability     | Prototype consistently available for demonstration and UAT across delivery period.                       | No unscheduled downtime during planned review sessions.            |
| NFR-05     | Usability        | Role-specific interface — users not exposed to modules outside their access entitlement.                 | Role-segregated navigation verified for all six role types in UAT. |
| NFR-06     | Usability        | Field-level validation with specific, actionable error messages identifying field and corrective action. | Tested via structured negative UAT test cases per form.            |
| NFR-07     | Accessibility    | Application navigable across modern web browsers without specialised plugins.                            | Verified across Chrome, Firefox, and Edge.                         |
| NFR-08     | Data Persistence | All data entered persists across application restarts.                                                   | Data survival confirmed after simulated restart during UAT.        |
| NFR-09     | Compliance       | Documented compliance controls (DPDP/HIPAA/GDPR) demonstrable within prototype.                          | Compliance walkthrough traceable to BRD Section 12.                |

## 12. Compliance Requirements
ClearVision Eye Hospital is an Indian institution. The DPDP Act 2023 is the primary regulation. HIPAA and GDPR referenced for portfolio completeness targeting global Life Sciences consulting roles.

**12.1 India – DPDP Act 2023 (Primary)**

|                |                                    |                                                                    |                                                                                    |                                     |
|----------------|------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------|-------------------------------------|
| **Control ID** | **DPDP Provision**                 | **Requirement**                                                    | **Implementation Approach**                                                        | **Status**                          |
| DPDP-01        | Section 6 – Consent                | Process data only on free, specific, informed, unambiguous consent | Consent checkbox at registration and self-registration; recorded in patient record | Demonstrated within prototype scope |
| DPDP-02        | Section 8 – Accuracy               | Data Fiduciary ensures data accuracy and completeness              | Field validation at registration; edit controls restricted to authorised roles     | Demonstrated within prototype scope |
| DPDP-03        | Section 9 – Storage Limitation     | Data not retained beyond necessary period                          | Retention policy documented (Section 12.4); auto-deletion not in prototype         | Documented                          |
| DPDP-04        | Section 11 – Right of Erasure      | Data Principal has right to erasure                                | System Administrator deletion workflow; Right to Erasure process documented        | Partially demonstrated              |
| DPDP-05        | Section 12 – Grievance Redressal   | Publish contact for grievance redressal                            | Disclaimer and contact reference in application UI                                 | Documented                          |
| DPDP-06        | Section 4 – Purpose Limitation     | Data processed only for specified lawful purpose                   | System collects clinically relevant data only; no profiling                        | Demonstrated within prototype scope |
| DPDP-07        | Section 8(7) – Security Safeguards | Reasonable security safeguards to prevent breach                   | Password hashing, RBAC, session timeout, audit logging                             | Demonstrated within prototype scope |

**12.2 USA – HIPAA (Reference)**

|                |                                   |                                       |                                                                 |                                                     |
|----------------|-----------------------------------|---------------------------------------|-----------------------------------------------------------------|-----------------------------------------------------|
| **Control ID** | **HIPAA Reference**               | **Requirement**                       | **Implementation Approach**                                     | **Status**                                          |
| HIPAA-01       | §164.312(a)(1) – Access Control   | Unique user ID per system user        | Unique username and User ID per account                         | Demonstrated within prototype scope                 |
| HIPAA-02       | §164.312(b) – Audit Controls      | Record and examine system activity    | Audit log captures User ID, action, module, timestamp           | Demonstrated within prototype scope                 |
| HIPAA-03       | §164.312(a)(2)(iii) – Auto Logoff | Session timeout after inactivity      | 15-minute session timeout enforced                              | Demonstrated within prototype scope                 |
| HIPAA-04       | §164.312(d) – Authentication      | Verify user identity before access    | bcrypt hashing; simulated MFA for Doctor/System Administrator   | Demonstrated within prototype scope (MFA simulated) |
| HIPAA-05       | §164.502(b) – Minimum Necessary   | Limit access to minimum necessary PHI | RBAC enforces role-specific data access                         | Demonstrated within prototype scope                 |
| HIPAA-06       | §164.312(c)(1) – Data Integrity   | Protect PHI from improper alteration  | Consultation records locked after 24 hours; audit log read-only | Demonstrated within prototype scope                 |
| HIPAA-07       | §164.312(a)(2)(iv) – Encryption   | Encryption at rest and in transit     | Known gap — not implemented in prototype. Production: AES-256.  | Documented Gap                                      |

**12.3 EU – GDPR (Reference)**

|                |                  |                                    |                                                                       |                                     |
|----------------|------------------|------------------------------------|-----------------------------------------------------------------------|-------------------------------------|
| **Control ID** | **GDPR Article** | **Requirement**                    | **Implementation Approach**                                           | **Status**                          |
| GDPR-01        | Article 5(1)(a)  | Lawfulness, fairness, transparency | Consent captured at registration with plain-language statement        | Demonstrated within prototype scope |
| GDPR-02        | Article 5(1)(b)  | Purpose limitation                 | System collects only clinical and administrative data; no profiling   | Demonstrated within prototype scope |
| GDPR-03        | Article 5(1)(c)  | Data minimisation                  | Registration fields restricted to necessary; optional fields labelled | Demonstrated within prototype scope |
| GDPR-04        | Article 7        | Consent                            | Checkbox with specific informed consent language; status recorded     | Demonstrated within prototype scope |
| GDPR-05        | Article 17       | Right to Erasure                   | System Administrator deletion workflow documented                     | Partially demonstrated              |
| GDPR-06        | Article 25       | Data Protection by Design          | RBAC, minimal data collection, audit logging by design                | Demonstrated within prototype scope |
| GDPR-07        | Article 32       | Security of Processing             | Password hashing, session timeout, audit logs, RBAC                   | Demonstrated within prototype scope |

**12.4 Data Retention Policy Reference**

|                             |                                            |                                     |                                                     |
|-----------------------------|--------------------------------------------|-------------------------------------|-----------------------------------------------------|
| **Data Category**           | **Retention Period**                       | **Basis**                           | **Prototype Status**                                |
| Patient demographic records | 7 years post last visit                    | Standard medical record retention   | Documented; not automated in prototype              |
| Clinical consultation notes | 10 years                                   | Ophthalmology clinical standard     | Documented; not automated in prototype              |
| Audit logs                  | 6 years minimum                            | HIPAA minimum / DPDP accountability | Documented; manual management in prototype          |
| User account records        | 30 days post deactivation                  | Data minimisation principle         | Documented; manual deletion by System Administrator |
| Patient consent records     | Duration of patient relationship + 3 years | DPDP / GDPR obligation              | Demonstrated in patient record                      |

## 13. Integration Requirements
*All integrations listed are Future Scope — not in current prototype.*

|                    |                          |                                             |               |           |
|--------------------|--------------------------|---------------------------------------------|---------------|-----------|
| **Integration ID** | **System / Service**     | **Purpose**                                 | **Direction** | **Phase** |
| INT-01             | SMS Gateway              | Appointment confirmations, reminders, OTP   | Outbound      | Phase 2   |
| INT-02             | Email Service            | Appointment confirmation, discharge summary | Outbound      | Phase 2   |
| INT-03             | LIS (Laboratory)         | Investigation order and result exchange     | Bidirectional | Phase 2   |
| INT-04             | PACS / Radiology         | Imaging order and retrieval                 | Bidirectional | Phase 2   |
| INT-05             | HL7 / FHIR               | Health system interoperability              | Bidirectional | Phase 2   |
| INT-06             | ABDM / ABHA              | National Health ID linkage                  | Bidirectional | Phase 2   |
| INT-07             | Enterprise IdP (LDAP/AD) | Authentication integration                  | Inbound       | Phase 3   |
| INT-08             | Billing / Finance System | Consultation fee and reconciliation         | Outbound      | Phase 3   |
| INT-09             | Insurance / TPA Portal   | Claim and pre-authorisation                 | Bidirectional | Phase 3   |

## 14. Assumptions
**14.1 Business Assumptions**

|         |                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------|
| **Ref** | **Assumption**                                                                                       |
| A-01    | Dean and key stakeholders available for requirements validation and UAT as scheduled.                |
| A-02    | All user role groups will participate in UAT before project sign-off.                                |
| A-03    | Hospital has basic internet connectivity and modern computing hardware for demonstration.            |
| A-04    | Doctors will complete consultation documentation digitally during the patient visit.                 |
| A-05    | Receptionists have sufficient computer literacy to operate a web-based interface.                    |
| A-06    | Patients have an active mobile number and/or email at the time of registration or self-registration. |
| A-07    | Dean has reviewed and approved the module list in Section 7.1 as the agreed scope boundary.          |
| A-08    | Synthetic data will be used for all prototype testing and demonstration.                             |

**14.2 Technical Assumptions**

|         |                                                                                            |
|---------|--------------------------------------------------------------------------------------------|
| **Ref** | **Assumption**                                                                             |
| A-09    | All technology is free, open-source; no paid subscriptions at any stage of the prototype.  |
| A-10    | Prototype runs locally or via repository clone; no live cloud hosting required.            |
| A-11    | A reviewer can follow the documented installation procedure independently.                 |
| A-12    | The database is acceptable for prototype data volumes and will not lose data during demos. |

## 15. Risk Register
|             |                                                  |                 |            |            |                                                                               |
|-------------|--------------------------------------------------|-----------------|------------|------------|-------------------------------------------------------------------------------|
| **Risk ID** | **Risk Description**                             | **Probability** | **Impact** | **Rating** | **Mitigation**                                                                |
| RSK-01      | Stakeholder unavailability for validation or UAT | Medium          | High       | High       | Schedule workshops with advance notice; document assumptions                  |
| RSK-02      | Scope creep post-BRD sign-off                    | High            | High       | Critical   | Formal change control; all changes require written approval and BRD amendment |
| RSK-03      | DPDP Act implementing rules may evolve           | Medium          | Medium     | Medium     | Build to current known obligations; review trigger on regulatory update       |
| RSK-04      | Part-time development creates timeline risk      | High            | Medium     | High       | Phased MVP delivery; core modules first; milestones agreed in advance         |
| RSK-05      | Free tools may constrain certain features        | Low             | Medium     | Low        | Scope designed around known free tool capabilities; limitations documented    |
| RSK-06      | Prototype misrepresented as production-ready     | Low             | High       | Medium     | Prominent disclaimer in UI, all docs, and repository README                   |
| RSK-07      | Real personal data accidentally introduced       | Low             | Critical   | High       | Strict synthetic data policy; no real PHI in any module                       |

## 16. Project Constraints
|         |                                                                 |                                                                 |
|---------|-----------------------------------------------------------------|-----------------------------------------------------------------|
| **Ref** | **Constraint**                                                  | **Impact**                                                      |
| C-01    | No monetary investment — all tools must be free and open-source | Technology selection limited to open-source stack only          |
| C-02    | No paid cloud hosting or SaaS subscriptions                     | Prototype runs locally; public repository used for distribution |
| C-03    | No production clinical deployment                               | All testing with synthetic data; production gaps in Section 8   |
| C-04    | Part-time development availability                              | Phased delivery; MVP first with enhancements in iterations      |
| C-05    | MFA simulated only                                              | Security demonstration; noted as prototype limitation           |

## 17. Glossary & Acronyms
|                    |                                                                                                  |
|--------------------|--------------------------------------------------------------------------------------------------|
| **Term / Acronym** | **Definition**                                                                                   |
| ABHA               | Ayushman Bharat Health Account — India's national digital health identifier                      |
| ABDM               | Ayushman Bharat Digital Mission — India's national digital health ecosystem                      |
| BA                 | Business Analyst                                                                                 |
| BRD                | Business Requirements Document — captures WHAT the business needs (this document)                |
| CR                 | Change Request — formal document governing scope changes post-BRD sign-off                       |
| DPDP Act           | Digital Personal Data Protection Act 2023 — India's primary data protection legislation          |
| FRD                | Functional Requirements Document — captures HOW the system shall behave                          |
| GDPR               | General Data Protection Regulation — EU personal data protection framework                       |
| HIPAA              | Health Insurance Portability and Accountability Act — USA health data protection standard        |
| HL7 / FHIR         | Health Level 7 / Fast Healthcare Interoperability Resources — healthcare data exchange standards |
| IOP                | Intraocular Pressure — clinical eye health measurement (glaucoma indicator)                      |
| MFA                | Multi-Factor Authentication — secondary identity verification post-login                         |
| MoSCoW             | Prioritisation method: Must Have / Should Have / Could Have / Won't Have                         |
| MVP                | Minimum Viable Product — smallest version delivering core business value                         |
| NDHM               | National Digital Health Mission — predecessor to ABDM                                            |
| PACS               | Picture Archiving and Communication System — radiology imaging management                        |
| PHI                | Protected Health Information — individually identifiable health information (HIPAA)              |
| RACI               | Responsibility matrix: Responsible / Accountable / Consulted / Informed                          |
| RBAC               | Role-Based Access Control — access rights by assigned user role                                  |
| RTM                | Requirements Traceability Matrix — links business requirements to FRs, test cases, and UAT       |
| SDLC               | Software Development Life Cycle                                                                  |
| UAT                | User Acceptance Testing — validation by end users before sign-off                                |
| VA                 | Visual Acuity — measure of the eye's ability to distinguish detail at a distance                 |

## 18. Sign-Off & Next Steps
**18.1 Approval Criteria**

|                                                                  |                    |            |
|------------------------------------------------------------------|--------------------|------------|
| **Criterion**                                                    | **Owner**          | **Status** |
| All stakeholder review comments submitted and incorporated       | Prashant Gore      | Pending    |
| Business Rules (Section 9) confirmed by Business Owner           | Dean               | Pending    |
| Scope boundaries (Sections 7.1, 7.2, 7.3) agreed and signed      | Dean / IT Lead     | Pending    |
| Compliance framework (Section 12) accepted by Compliance Officer | Compliance Officer | Pending    |
| Risk Register (Section 15) reviewed and owners assigned          | Dean / IT Lead     | Pending    |
| All mandatory approvals obtained (Section 1.2)                   | All Approvers      | Pending    |

**18.2 Downstream Document Plan**

|                                        |                  |            |
|----------------------------------------|------------------|------------|
| **Document**                           | **ID**           | **Status** |
| Functional Requirements Document (FRD) | CVH-FRD-001 v1.2 | Complete   |
| Requirements Traceability Matrix (RTM) | CVH-RTM-001 v1.1 | Complete   |
| Entity Relationship Diagram (ERD)      | CVH-ERD-001 v1.0 | Complete   |
| Sequence Diagrams (SQD)                | CVH-SQD-001 v1.1 | Complete   |
| System Test Cases (STC)                | CVH-STC-001 v1.1 | Complete   |
| UAT Scripts                            | CVH-UAT-001 v1.1 | Complete   |
| Change Request (CR)                    | CVH-CR-001 v1.0  | Complete   |
| Streamlit Prototype                    | CVH-DEV-001 v1.0 | Complete   |

**END OF DOCUMENT**

> **Appendix A: Data Dictionary**

*Key business data entities. Technical specifications in FRD (CVH-FRD-001 v1.2) Section 16. M=Mandatory \| O=Optional \| S=System Generated*

**A.1 Patient**

|                           |                     |         |                                     |                      |                                                            |
|---------------------------|---------------------|---------|-------------------------------------|----------------------|------------------------------------------------------------|
| **Field**                 | **Label**           | **M/O** | **Validation**                      | **Business Rule**    | **Notes**                                                  |
| patient\_id               | Patient ID          | S       | CVH-YYYY-NNNNN                      | BR-PAT-01, BR-PAT-03 | Never modified or reused                                   |
| first\_name               | First Name          | M       | Text 2–50 chars                     | —                    | No numerics                                                |
| last\_name                | Last Name           | M       | Text 2–50 chars                     | —                    | No numerics                                                |
| date\_of\_birth           | Date of Birth       | M       | Past date; age 0–120                | BR-PAT-02            | Used in combination duplicate check                        |
| gender                    | Gender              | M       | Male/Female/Other/Prefer not to say | —                    | Dropdown                                                   |
| mobile\_number            | Mobile Number       | M       | 10-digit numeric                    | BR-PAT-02            | Used in combination duplicate check; username for self-reg |
| email\_address            | Email               | O       | Valid email format                  | BR-PAT-02            | Optional; used in duplicate check where provided           |
| known\_allergies          | Known Allergies     | O       | Free text max 500 chars             | BR-CLN-01            | Visible in Doctor Dashboard                                |
| current\_medications      | Current Medications | O       | Free text max 500 chars             | BR-CLN-01            | Visible in Doctor Dashboard                                |
| existing\_eye\_conditions | Eye Conditions      | O       | Free text max 500 chars             | BR-CLN-01            | Ophthalmology history                                      |
| blood\_group              | Blood Group         | O       | A+/A-/B+/B-/O+/O-/AB+/AB-/Unknown   | —                    | Dropdown                                                   |
| consent\_given            | Consent             | M       | Boolean                             | BR-PAT-05, DPDP-01   | Registration blocked if No                                 |
| record\_status            | Status              | S       | Active / Deactivated                | BR-PAT-06            | Default: Active                                            |
| linked\_user\_id          | Portal User ID      | S       | FK → users.user\_id                 | BR-PAT-09            | Set on self-registration or admin linking                  |

**A.2 Appointment**

|                      |                     |                |                                                              |                      |                                    |
|----------------------|---------------------|----------------|--------------------------------------------------------------|----------------------|------------------------------------|
| **Field**            | **Label**           | **M/O**        | **Validation**                                               | **Business Rule**    | **Notes**                          |
| appointment\_id      | Appointment ID      | S              | APT-YYYY-NNNNN                                               | —                    | System generated; unique           |
| patient\_id          | Patient ID          | M              | FK → patients                                                | —                    | Must be active patient             |
| doctor\_id           | Doctor ID           | M              | FK → users (Doctor role)                                     | BR-APT-01            | Doctor role only                   |
| appointment\_date    | Date                | M              | Future date; no holidays                                     | BR-APT-08            | No closed dates                    |
| appointment\_time    | Time                | M              | HH:MM; 20-min blocks                                         | BR-APT-01, BR-APT-02 | Conflict check on save             |
| visit\_type          | Visit Type          | M              | New/Follow-Up/Emergency/Walk-In                              | BR-APT-05            | Dropdown                           |
| appointment\_status  | Status              | S              | Scheduled/Checked-In/In-Progress/Completed/Cancelled/No-Show | BR-APT-09            | System or authorised role updates  |
| cancellation\_reason | Cancellation Reason | M if cancelled | Text max 300 chars                                           | BR-APT-06            | Late Cancellation flagged &lt;1 hr |

**A.3 User Account**

|                        |                 |         |                                                                       |                      |                                            |
|------------------------|-----------------|---------|-----------------------------------------------------------------------|----------------------|--------------------------------------------|
| **Field**              | **Label**       | **M/O** | **Validation**                                                        | **Business Rule**    | **Notes**                                  |
| user\_id               | User ID         | S       | USR-NNNNN                                                             | BR-SEC-01            | Never reused                               |
| username               | Username        | M       | Alphanumeric 5–20 chars; unique                                       | BR-SEC-01            | Mobile number for self-registered patients |
| password\_hash         | Password        | M       | Hashed; complexity enforced                                           | BR-SEC-02            | Plaintext never stored                     |
| role                   | Role            | M       | Patient/Receptionist/Doctor/Clinician/System Administrator/Dean-Admin | BR-REQ-AM-02         | Drives module access                       |
| account\_status        | Status          | S       | Active/Locked/Suspended/Deactivated                                   | BR-SEC-04, BR-SEC-07 | Locked at 3 failed attempts                |
| failed\_login\_count   | Failed Attempts | S       | Integer 0–3                                                           | BR-SEC-04            | Reset on successful login                  |
| last\_login\_timestamp | Last Login      | S       | ISO 8601 datetime                                                     | BR-SEC-07            | Inactivity detection at 90 days            |

**A.4 Consultation Note**

|                       |                 |         |                            |                   |                                  |
|-----------------------|-----------------|---------|----------------------------|-------------------|----------------------------------|
| **Field**             | **Label**       | **M/O** | **Validation**             | **Business Rule** | **Notes**                        |
| consultation\_id      | Consultation ID | S       | CON-YYYY-NNNNN             | —                 | System generated                 |
| appointment\_id       | Appointment ID  | M       | FK → appointments (UNIQUE) | —                 | One consultation per appointment |
| doctor\_id            | Doctor ID       | M       | FK → users                 | BR-CLN-01         | Treating doctor only             |
| chief\_complaint      | Chief Complaint | M       | Free text max 500 chars    | BR-CLN-01         | Presenting symptom               |
| examination\_findings | Findings        | M       | Free text max 1000 chars   | BR-CLN-01         | Clinical findings                |
| diagnosis             | Diagnosis       | M       | Free text max 200 chars    | BR-CLN-01         | Primary diagnosis                |
| management\_plan      | Treatment Plan  | M       | Free text max 1000 chars   | BR-CLN-01         | Actions and follow-up            |
| is\_editable          | Editable        | S       | Boolean                    | BR-CLN-02         | False after 24 hrs from creation |

**A.5 Vitals**

|                    |                  |         |                        |                   |                        |
|--------------------|------------------|---------|------------------------|-------------------|------------------------|
| **Field**          | **Label**        | **M/O** | **Validation**         | **Business Rule** | **Notes**              |
| vitals\_id         | Vitals ID        | S       | VIT-NNNNN              | —                 | System generated       |
| appointment\_id    | Appointment ID   | M       | FK → appointments      | BR-CLN-04         | Pre-consultation entry |
| recorded\_by       | Recorded By      | S       | FK → users             | BR-CLN-04         | Clinician/Nurse only   |
| visual\_acuity\_re | VA Right Eye     | M       | Snellen: 6/6, 6/9 etc. | —                 |                        |
| visual\_acuity\_le | VA Left Eye      | M       | Snellen: 6/6, 6/9 etc. | —                 |                        |
| iop\_re            | IOP Right (mmHg) | O       | Numeric 1–60           | —                 | Amber flag &gt;21      |
| iop\_le            | IOP Left (mmHg)  | O       | Numeric 1–60           | —                 | Amber flag &gt;21      |
| blood\_pressure    | Blood Pressure   | O       | NNN/NN mmHg            | —                 | Systolic/Diastolic     |

**A.6 Audit Log**

|                   |           |         |                                                                        |                   |                               |
|-------------------|-----------|---------|------------------------------------------------------------------------|-------------------|-------------------------------|
| **Field**         | **Label** | **M/O** | **Validation**                                                         | **Business Rule** | **Notes**                     |
| log\_id           | Log ID    | S       | AUTOINCREMENT                                                          | —                 | Sequential; never deleted     |
| user\_id          | User ID   | S       | FK → users                                                             | BR-REQ-IT-02      | Action performer              |
| action\_type      | Action    | S       | LOGIN/LOGOUT/CREATE/READ/UPDATE/DELETE/LOCK/UNLOCK/DUPLICATE\_OVERRIDE | BR-REQ-IT-02      | Standardised codes            |
| module            | Module    | S       | MOD-01 to MOD-10                                                       | BR-REQ-IT-02      | Portal module reference       |
| action\_timestamp | Timestamp | S       | ISO 8601 HH:MM:SS                                                      | BR-REQ-IT-02      | UTC precision                 |
| outcome           | Outcome   | S       | Success / Failed                                                       | BR-SEC-04         | Failed logins trigger lockout |
