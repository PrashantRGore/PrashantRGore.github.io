---
hide:
  - toc
---

<div class="ba-meta-bar">
<span class="ba-badge ba-badge--id">CVH-FRD-001</span>
<span class="ba-badge ba-badge--version">Version 1.2</span>
<span class="ba-badge ba-badge--status">Baselined</span>
<span class="ba-badge ba-badge--compliance">DPDP / HIPAA / GDPR</span>
</div>

# Functional Requirements Document (FRD)

|                  |                                                        |
|------------------|--------------------------------------------------------|
| Document ID      | CVH-FRD-001                                            |
| Version          | 1.2 – CVH-CR-001 Amendment                             |
| Date             | July 2026                                              |
| Prepared By      | Prashant Gore – BA & Digital Transformation Consultant |
| Parent Document  | CVH-BRD-001 v1.3                                       |
| RTM Reference    | CVH-RTM-001 v1.1                                       |
| Status           | DRAFT – Under Review                                   |
| Technology Stack | Python \| Streamlit \| SQLite3 \| bcrypt \| Pandas     |
| Change Ref       | CVH-CR-001 – UC-05 and FR-PAT-05 to FR-PAT-08 added    |

> *DISCLAIMER: Prototype demonstration project only. No real patient data. Not for production clinical deployment.*

## 1. Document Control
**1.1 Version History**

|             |           |               |                                                                                                                                                              |            |
|-------------|-----------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **Version** | **Date**  | **Author**    | **Description**                                                                                                                                              | **Status** |
| 1.0         | June 2026 | Prashant Gore | Initial FRD                                                                                                                                                  | Superseded |
| 1.1         | June 2026 | Prashant Gore | Added: Use Case specs, MoSCoW priority, Error Handling, Security FR section, Testability column, BR-REQ-PR-02 corrected to combination logic                 | Superseded |
| 1.2         | July 2026 | Prashant Gore | CVH-CR-001: UC-05 added (Patient Self-Registration); FR-PAT-05 to FR-PAT-08 added to MOD-07; parent doc updated to BRD v1.3; Section 18 traceability updated | Draft      |

**1.2 Document Approvals**

|                            |               |                                    |           |
|----------------------------|---------------|------------------------------------|-----------|
| **Role**                   | **Name**      | **Signature**                      | **Date**  |
| Dean / Business Owner      | Dr. \[Name\]  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| Business Analyst           | Prashant Gore | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | July 2026 |
| Developer / Technical Lead | TBD           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |
| System Administrator       | TBD           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |           |

**1.3 Relationship to BRD**

This FRD defines HOW the system will behave to satisfy the WHAT defined in CVH-BRD-001 v1.3. Every FR traces to at least one BR. Full traceability maintained in CVH-RTM-001 v1.1.

## 2. System Overview
**2.1 Technology Stack**

|                       |                |                                               |                      |
|-----------------------|----------------|-----------------------------------------------|----------------------|
| **Component**         | **Technology** | **Purpose**                                   | **Version**          |
| Application Framework | Streamlit      | Web UI, routing, session management           | Latest stable (free) |
| Programming Language  | Python         | Business logic, validation, data processing   | 3.9+                 |
| Database              | SQLite3        | Local relational storage; Python built-in     | Built-in             |
| Password Security     | bcrypt         | Credential hashing; one-way irreversible      | Latest via pip       |
| Data Processing       | Pandas         | Report generation and tabular data operations | Latest via pip       |
| Version Control       | Git / GitHub   | Source code and documentation (public repo)   | Latest               |

**2.2 Application Architecture**

|                |                         |                                                                                                     |
|----------------|-------------------------|-----------------------------------------------------------------------------------------------------|
| **Layer**      | **Component**           | **Description**                                                                                     |
| Presentation   | Streamlit UI Pages      | Role-specific page rendering driven by session state; public signup page for unauthenticated access |
| Navigation     | app.py (Main Router)    | Reads session role; renders correct module; enforces RBAC; routes public signup page                |
| Business Logic | mod\_01.py … mod\_10.py | One file per module; forms, validation, business rules                                              |
| Data Access    | db\_utils.py            | Centralised SQLite connection handler; all DB operations here — replace to migrate DB               |
| Security       | auth.py                 | Login flow, bcrypt verification, session management, lockout, password reset                        |
| Database       | cvh\_hospital.db        | SQLite file; 10 tables                                                                              |

**2.3 User Roles & Module Access Matrix**

*✔ = Full Access \| R = Read Only \| — = No Access \| P = Public (no login required)*

|                               |             |                  |            |               |               |                |                 |
|-------------------------------|-------------|------------------|------------|---------------|---------------|----------------|-----------------|
| **Module**                    | **Patient** | **Receptionist** | **Doctor** | **Clinician** | **Sys Admin** | **Dean/Admin** | **Public**      |
| MOD-01 Patient Registration   | —           | ✔                | —          | —             | —             | ✔              | —               |
| MOD-02 Appointment Management | R           | ✔                | R          | —             | —             | ✔              | —               |
| MOD-03 Doctor Dashboard       | —           | —                | ✔          | —             | —             | —              | —               |
| MOD-04 Clinician Panel        | —           | —                | R          | ✔             | —             | —              | —               |
| MOD-05 Receptionist Desk      | —           | ✔                | —          | —             | —             | —              | —               |
| MOD-06 System Admin Dashboard | —           | —                | —          | —             | ✔             | —              | —               |
| MOD-07 Patient Portal         | ✔           | —                | —          | —             | —             | —              | P (signup only) |
| MOD-08 Dean/Admin Dashboard   | —           | —                | —          | —             | —             | ✔              | —               |
| MOD-09 Access Management      | —           | —                | —          | —             | ✔             | —              | —               |
| MOD-10 Audit & Compliance Log | —           | —                | —          | —             | ✔             | R              | —               |

## 3. Use Case Specifications
*Four primary use cases plus UC-05 added per CVH-CR-001.*

**UC-01: User Login**

|                  |                                                                                                                                                                                                                                                                                                                                                                                     |
|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Element**      | **Detail**                                                                                                                                                                                                                                                                                                                                                                          |
| Use Case ID      | UC-01                                                                                                                                                                                                                                                                                                                                                                               |
| Use Case Name    | User Login                                                                                                                                                                                                                                                                                                                                                                          |
| Actor            | Any registered user (all 6 roles)                                                                                                                                                                                                                                                                                                                                                   |
| Preconditions    | Account exists with status=Active. Application running.                                                                                                                                                                                                                                                                                                                             |
| Trigger          | User navigates to application URL.                                                                                                                                                                                                                                                                                                                                                  |
| Normal Flow      | 1\. Enter username and password. 2. System verifies username and account status=Active. 3. System validates password against bcrypt hash. 4. Doctor/System Administrator: simulated MFA screen displayed. 5. System creates session state (user\_id, role, login\_time, last\_activity). 6. LOGIN event logged (outcome=Success). 7. Router redirects to role-specific home module. |
| Alternate Flow 1 | Invalid credentials: failed\_login\_count incremented. At 3: account locked, LOCK event logged.                                                                                                                                                                                                                                                                                     |
| Alternate Flow 2 | Account Locked: Message shown. No credential check performed.                                                                                                                                                                                                                                                                                                                       |
| Alternate Flow 3 | Password expired: redirected to password reset screen before module access.                                                                                                                                                                                                                                                                                                         |
| Post-Conditions  | User authenticated; role-specific module rendered; 15-min timeout running.                                                                                                                                                                                                                                                                                                          |
| Exceptions       | DB unavailable: generic error shown. No session created.                                                                                                                                                                                                                                                                                                                            |

**UC-02: Patient Registration (Receptionist-driven)**

|                  |                                                                                                                                                                                                                                                                                                                                    |
|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Element**      | **Detail**                                                                                                                                                                                                                                                                                                                         |
| Use Case ID      | UC-02                                                                                                                                                                                                                                                                                                                              |
| Use Case Name    | New Patient Registration                                                                                                                                                                                                                                                                                                           |
| Actor            | Receptionist / Dean-Admin                                                                                                                                                                                                                                                                                                          |
| Preconditions    | Actor authenticated. Patient present at reception.                                                                                                                                                                                                                                                                                 |
| Trigger          | Actor selects Register New Patient from MOD-01.                                                                                                                                                                                                                                                                                    |
| Normal Flow      | 1\. Complete registration form (mandatory and optional fields). 2. Check consent checkbox. 3. Submit form. 4. System validates all mandatory fields. 5. System performs duplicate check: Name + DOB + Mobile. 6. No duplicate: Patient ID generated (CVH-YYYY-NNNNN). 7. Record saved; CREATE event logged; success message shown. |
| Alternate Flow 1 | Validation failure: fields highlighted; inline errors shown. No DB write.                                                                                                                                                                                                                                                          |
| Alternate Flow 2 | Duplicate detected: warning with existing Patient ID; actor overrides or cancels.                                                                                                                                                                                                                                                  |
| Alternate Flow 3 | Consent not given: submission blocked.                                                                                                                                                                                                                                                                                             |
| Post-Conditions  | Patient record active. Patient can be booked for appointment.                                                                                                                                                                                                                                                                      |
| Exceptions       | DB error on save: generic error; transaction rolled back.                                                                                                                                                                                                                                                                          |

**UC-03: Appointment Booking**

|                  |                                                                                                                                                                                                                                                                                                                       |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Element**      | **Detail**                                                                                                                                                                                                                                                                                                            |
| Use Case ID      | UC-03                                                                                                                                                                                                                                                                                                                 |
| Use Case Name    | Book Appointment                                                                                                                                                                                                                                                                                                      |
| Actor            | Receptionist / Dean-Admin                                                                                                                                                                                                                                                                                             |
| Preconditions    | Patient registered. Doctor available. Date not a holiday.                                                                                                                                                                                                                                                             |
| Trigger          | Actor selects Book Appointment from MOD-02.                                                                                                                                                                                                                                                                           |
| Normal Flow      | 1\. Search patient by ID or name. 2. Select doctor, date, visit type. 3. System loads available 20-min slots (excluding booked + holidays). 4. Actor selects slot and confirms. 5. System re-checks conflict and holiday at confirm time. 6. Appointment saved (status=Scheduled); CREATE event logged; ID displayed. |
| Alternate Flow 1 | Slot conflict: slot unavailable; error shown.                                                                                                                                                                                                                                                                         |
| Alternate Flow 2 | Doctor daily max reached: all slots unavailable; error shown.                                                                                                                                                                                                                                                         |
| Alternate Flow 3 | Patient not found: error shown; actor advised to register first.                                                                                                                                                                                                                                                      |
| Post-Conditions  | Appointment in table (status=Scheduled). Visible in queue and Doctor dashboard.                                                                                                                                                                                                                                       |
| Exceptions       | DB error: booking not saved; generic error shown.                                                                                                                                                                                                                                                                     |

**UC-04: Consultation & Prescription**

|                  |                                                                                                                                                                                                                                                                                                                                                                                                              |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Element**      | **Detail**                                                                                                                                                                                                                                                                                                                                                                                                   |
| Use Case ID      | UC-04                                                                                                                                                                                                                                                                                                                                                                                                        |
| Use Case Name    | Record Consultation and Generate Prescription                                                                                                                                                                                                                                                                                                                                                                |
| Actor            | Doctor                                                                                                                                                                                                                                                                                                                                                                                                       |
| Preconditions    | Appointment status=In-Progress. Doctor authenticated.                                                                                                                                                                                                                                                                                                                                                        |
| Trigger          | Doctor opens patient card from MOD-03 appointment list.                                                                                                                                                                                                                                                                                                                                                      |
| Normal Flow      | 1\. View patient demographics, medical history, vitals. 2. Enter Chief Complaint, Findings, Diagnosis, Treatment Plan. 3. Save consultation note (timestamped, author-tagged; is\_editable=1 for 24 hrs). 4. Add prescription lines (drug, dosage, frequency, duration). 5. Save prescription (linked to consultation\_id). 6. Click Complete Consultation: status=Completed; check-out triggered in MOD-05. |
| Alternate Flow 1 | No vitals: advisory shown; doctor proceeds.                                                                                                                                                                                                                                                                                                                                                                  |
| Alternate Flow 2 | Prescription before consultation: blocked with message.                                                                                                                                                                                                                                                                                                                                                      |
| Alternate Flow 3 | Record locked (&gt;24 hrs): fields read-only; message shown.                                                                                                                                                                                                                                                                                                                                                 |
| Post-Conditions  | Consultation and prescription saved. Appointment=Completed. Patient check-out available.                                                                                                                                                                                                                                                                                                                     |
| Exceptions       | DB error: transaction rolled back. Doctor advised to retry.                                                                                                                                                                                                                                                                                                                                                  |

**UC-05: Patient Self-Registration (CVH-CR-001)**

|                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Element**      | **Detail**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Use Case ID      | UC-05                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Use Case Name    | Patient Self-Registration                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Actor            | Unregistered Patient (unauthenticated)                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Preconditions    | Patient has no existing record. Public signup page accessible without login.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Trigger          | Patient selects New Patient? Register Here on the login page.                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Normal Flow      | 1\. Complete form: Full Name, DOB, Gender, Mobile, Email (optional), Password, Consent. 2. System validates all fields and password complexity (BR-SEC-02). 3. System performs duplicate check (Name + DOB + Mobile). 4. No duplicate: Patient ID auto-generated (CVH-YYYY-NNNNN). 5. Portal account created (username=mobile, role=Patient, linked to patient record). 6. Patient auto-logged in; redirected to MOD-07 Patient Portal. 7. CREATE events logged to audit\_log for patient record and user account. |
| Alternate Flow 1 | Duplicate detected: warning shown; patient advised to contact Reception.                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Alternate Flow 2 | Password fails complexity: specific error per BR-SEC-02; form not submitted.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Alternate Flow 3 | Mobile already exists as username: patient advised to log in or contact System Administrator.                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Post-Conditions  | Patient record in patients table. Portal account in users table (role=Patient). Patient logged in.                                                                                                                                                                                                                                                                                                                                                                                                                 |
| Exceptions       | DB error: generic message. Transaction rolled back. No partial record written.                                                                                                                                                                                                                                                                                                                                                                                                                                     |

## 4. MOD-09: Authentication & Access Management
**4.1 Login & Session Functional Requirements**

|           |                                                                                                     |                                                      |              |                         |                                                                 |
|-----------|-----------------------------------------------------------------------------------------------------|------------------------------------------------------|--------------|-------------------------|-----------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                          | **BR Source**                                        | **Priority** | **Acceptance Test Ref** | **Testability Note**                                            |
| FR-AM-01  | System shall authenticate all users via username and password before granting module access.        | BR-REQ-AM-01                                         | Must Have    | TC-AM-001               | Direct URL access without login → verify redirect to login page |
| FR-AM-02  | System shall enforce RBAC: each role accesses only designated modules; cross-role access denied.    | BR-REQ-AM-02                                         | Must Have    | TC-AM-002               | Login as each role; verify unavailable modules inaccessible     |
| FR-AM-03  | System shall expire sessions after 15 minutes of inactivity and require re-authentication.          | BR-REQ-AM-03                                         | Must Have    | TC-AM-003               | Idle 16 min; verify session cleared and login shown             |
| FR-AM-04  | System shall lock account after 3 consecutive failed logins; only System Administrator can unlock.  | BR-REQ-AM-04                                         | Must Have    | TC-AM-004               | 3 wrong passwords; verify locked; verify admin unlock works     |
| FR-AM-05  | System shall display simulated MFA for Doctor and System Administrator after password verification. | Prototype scope (no direct BR — simulated per PL-02) | Should Have  | TC-AM-005               | Login as Doctor; verify MFA screen; verify access after MFA     |

**4.2 Password Policy Functional Requirements**

|           |                                                                                         |               |              |                         |                                                              |
|-----------|-----------------------------------------------------------------------------------------|---------------|--------------|-------------------------|--------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                              | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                         |
| FR-AM-06  | Passwords shall be hashed using bcrypt (work factor 12); plaintext storage prohibited.  | BR-SEC-02     | Must Have    | TC-AM-006               | Inspect DB; verify no plaintext passwords                    |
| FR-AM-07  | Password complexity enforced: min 8 chars, 1 uppercase, 1 numeric, 1 special character. | BR-SEC-02     | Must Have    | TC-AM-007               | Attempt weak password; verify rejection and specific error   |
| FR-AM-08  | Passwords shall expire after 90 days; user prompted to reset before module access.      | BR-SEC-03     | Should Have  | TC-AM-008               | Set expiry to past; login; verify reset prompt before access |
| FR-AM-09  | Force password reset flag: if set, user must change password on next login.             | BR-SEC-03     | Must Have    | TC-AM-009               | Admin sets force reset; user logs in; verify reset flow      |

## 5. MOD-01: Patient Registration
**5.1 Functional Requirements**

|           |                                                                                                               |               |              |                         |                                                                                                |
|-----------|---------------------------------------------------------------------------------------------------------------|---------------|--------------|-------------------------|------------------------------------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                                    | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                                                           |
| FR-PR-01  | System shall provide digital registration form capturing all mandatory and optional patient fields.           | BR-REQ-PR-01  | Must Have    | TC-PR-001               | Complete registration; verify record created                                                   |
| FR-PR-02  | Duplicate detection: Full Name + DOB + Mobile combination. Mobile or email alone shall NOT trigger duplicate. | BR-REQ-PR-02  | Must Have    | TC-PR-002               | Register; re-register same Name+DOB+Mobile → warning. Same mobile different name → no warning. |
| FR-PR-03  | Consent checkbox mandatory; form submission blocked without consent.                                          | BR-REQ-PR-03  | Must Have    | TC-PR-003               | Submit without consent; verify blocked                                                         |
| FR-PR-04  | Receptionist and Dean-Admin can search, view, edit patient records; doctors/clinicians read-only.             | BR-REQ-PR-04  | Must Have    | TC-PR-004               | Login as Doctor; verify edit controls absent                                                   |
| FR-PR-05  | Ophthalmology medical history captured at registration; visible in Doctor Dashboard.                          | BR-REQ-PR-05  | Must Have    | TC-PR-005               | Register with history; verify visible in MOD-03                                                |

**5.2 Registration Form Field Specifications**

|                  |                |               |                                     |                                               |
|------------------|----------------|---------------|-------------------------------------|-----------------------------------------------|
| **Field**        | **Input Type** | **Mandatory** | **Validation Rule**                 | **Error Message**                             |
| First Name       | Text           | Yes           | 2–50 chars; letters and spaces only | First name must be 2–50 characters.           |
| Last Name        | Text           | Yes           | 2–50 chars; letters and spaces only | Last name must be 2–50 characters.            |
| Date of Birth    | Date picker    | Yes           | Past date; age 0–120                | Date of birth cannot be a future date.        |
| Gender           | Dropdown       | Yes           | Male/Female/Other/Prefer not to say | Please select a gender.                       |
| Mobile Number    | Text           | Yes           | Exactly 10 digits; numeric only     | Mobile must be exactly 10 digits.             |
| Email Address    | Text           | No            | Valid email format                  | Please enter a valid email address.           |
| Consent Checkbox | Checkbox       | Yes           | Must be checked                     | Consent is required to complete registration. |

## 6. MOD-02: Appointment Management
**6.1 Functional Requirements**

|           |                                                                                              |               |              |                         |                                                                      |
|-----------|----------------------------------------------------------------------------------------------|---------------|--------------|-------------------------|----------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                   | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                                 |
| FR-APT-01 | System shall show doctor availability by date with 20-min slots; enforce conflict detection. | BR-REQ-APT-01 | Must Have    | TC-APT-001              | Select doctor+date; verify slots; book; attempt same slot → rejected |
| FR-APT-02 | Conflict re-checked at confirm time to prevent race conditions.                              | BR-REQ-APT-01 | Must Have    | TC-APT-001              | Session state persists booking context; conflict checked at confirm  |
| FR-APT-03 | Appointment status tracked: Scheduled→Checked-In→In-Progress→Completed/Cancelled/No-Show.    | BR-REQ-APT-02 | Must Have    | TC-APT-002              | Walk through full lifecycle; verify each transition                  |
| FR-APT-04 | Emergency and Walk-In visit types supported.                                                 | BR-REQ-APT-03 | Must Have    | TC-APT-003              | Create Emergency; verify appears with designation                    |
| FR-APT-05 | Cancellation requires mandatory reason; Late Cancellation flagged if &lt;1 hr before slot.   | BR-REQ-APT-04 | Must Have    | TC-APT-004              | Cancel without reason → blocked; cancel within 1 hr → flag set       |
| FR-APT-06 | No-Show auto-assigned if patient not Checked-In within 15 min of slot time.                  | BR-REQ-APT-05 | Should Have  | TC-APT-005              | Past-time appointment without check-in → verify No-Show              |

**6.2 Appointment Status State Machine**

|                        |               |                                    |                                 |
|------------------------|---------------|------------------------------------|---------------------------------|
| **From Status**        | **To Status** | **Trigger**                        | **Authorised Role**             |
| (New)                  | Scheduled     | Appointment booked                 | Receptionist / Dean-Admin       |
| Scheduled              | Checked-In    | Patient arrives; check-in actioned | Receptionist                    |
| Checked-In             | In-Progress   | Doctor opens consultation          | Doctor                          |
| In-Progress            | Completed     | Doctor marks Complete              | Doctor                          |
| Scheduled / Checked-In | Cancelled     | Cancellation with reason           | Receptionist / Doctor / Patient |
| Scheduled              | No-Show       | Auto-assigned 15 min past slot     | System                          |

## 7. MOD-03: Doctor Dashboard
**7.1 Functional Requirements**

|           |                                                                                                      |               |              |                         |                                                                   |
|-----------|------------------------------------------------------------------------------------------------------|---------------|--------------|-------------------------|-------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                           | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                              |
| FR-CLN-01 | Doctor views today's appointments on login, sorted by time.                                          | BR-REQ-CLN-01 | Must Have    | TC-CLN-001              | Login as Doctor; verify today's list in time order                |
| FR-CLN-02 | Doctor accesses patient demographics, medical history, past visits, vitals from appointment card.    | BR-REQ-CLN-01 | Must Have    | TC-CLN-001              | Open patient card; verify all sections populated                  |
| FR-CLN-03 | Doctor enters structured consultation note: Chief Complaint, Findings, Diagnosis, Treatment Plan.    | BR-REQ-CLN-01 | Must Have    | TC-CLN-002              | Enter and save; verify record with doctor\_id and timestamp in DB |
| FR-CLN-04 | Doctor generates prescription linked to consultation; prescription blocked if no consultation saved. | BR-REQ-CLN-02 | Must Have    | TC-CLN-002              | Save prescription; verify linked to consultation\_id              |
| FR-CLN-05 | Consultation records lock after 24 hours; fields read-only; save controls hidden.                    | BR-REQ-CLN-04 | Must Have    | TC-CLN-004              | Set timestamp &gt;24 hrs past; attempt edit; verify locked        |
| FR-CLN-06 | Investigation orders created and linked to specific patient visit.                                   | BR-REQ-CLN-05 | Should Have  | TC-CLN-005              | Create order; verify linked to appointment\_id                    |

## 8. MOD-04: Clinician Panel
**8.1 Functional Requirements**

|           |                                                                                   |               |              |                         |                                                                     |
|-----------|-----------------------------------------------------------------------------------|---------------|--------------|-------------------------|---------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                        | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                                |
| FR-CLN-07 | Clinician views assigned patient list for current day (Scheduled/Checked-In).     | BR-REQ-CLN-03 | Must Have    | TC-CLN-003              | Login as Clinician; verify today's patient list                     |
| FR-CLN-08 | Clinician records vitals: Visual Acuity (both eyes), IOP (both eyes), BP, Weight. | BR-REQ-CLN-03 | Must Have    | TC-CLN-003              | Enter vitals; verify saved and visible in Doctor Dashboard          |
| FR-CLN-09 | IOP &gt;21 mmHg triggers amber advisory; record saves normally.                   | BR-REQ-CLN-03 | Should Have  | TC-CLN-003              | Enter IOP=25; verify amber flag shown; save succeeds                |
| FR-CLN-10 | Vitals visible to treating Doctor in MOD-03 consultation view.                    | BR-REQ-CLN-03 | Must Have    | TC-CLN-003              | Record vitals as Clinician; login as Doctor; verify in patient card |

## 9. MOD-05: Receptionist Desk
**9.1 Functional Requirements**

|           |                                                                               |               |              |                         |                                                                     |
|-----------|-------------------------------------------------------------------------------|---------------|--------------|-------------------------|---------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                    | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                                |
| FR-REC-01 | Receptionist views today's full appointment queue sorted by time.             | BR-REQ-APT-02 | Must Have    | TC-APT-002              | Login as Receptionist; verify queue populated and sorted            |
| FR-REC-02 | Receptionist checks in patients (window: 30 min before to 15 min after slot). | BR-REQ-APT-02 | Must Have    | TC-APT-002              | Early check-in → blocked. Within window → Checked-In.               |
| FR-REC-03 | Receptionist cancels/reschedules appointments; mandatory reason required.     | BR-REQ-APT-04 | Must Have    | TC-APT-004              | Cancel without reason → blocked; with reason → status+audit updated |

## 10. MOD-06: System Administrator Dashboard
**10.1 Functional Requirements**

|           |                                                                                                 |               |              |                         |                                                                                    |
|-----------|-------------------------------------------------------------------------------------------------|---------------|--------------|-------------------------|------------------------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                      | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                                               |
| FR-IT-01  | System Administrator creates, edits, deactivates, unlocks user accounts; assigns/changes roles. | BR-REQ-IT-01  | Must Have    | TC-IT-001               | Create user; verify login. Deactivate; verify blocked. Unlock; verify login works. |
| FR-IT-02  | Audit log viewer: filter by date, user, action type, module, outcome; export to CSV.            | BR-REQ-IT-02  | Must Have    | TC-IT-002               | Perform actions; verify entries; test filters; export CSV                          |
| FR-IT-03  | System health indicators: sessions, user counts, today's appointments, errors, DB counts.       | BR-REQ-IT-03  | Should Have  | TC-IT-003               | Navigate to health panel; verify all 5 indicators present                          |
| FR-IT-04  | System Administrator configures hospital holiday/closed dates; dates excluded from booking.     | BR-APT-08     | Should Have  | TC-IT-004               | Add holiday; attempt booking on that date → blocked                                |

## 11. MOD-07: Patient Portal
**11.1 Functional Requirements**

|           |                                                                                                                                             |               |              |                         |                                                                          |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------|---------------|--------------|-------------------------|--------------------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                                                                  | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                                     |
| FR-PAT-01 | Patient views only their own appointments; RBAC enforced at query level.                                                                    | BR-REQ-PR-04  | Must Have    | TC-PR-004               | Login as Patient; verify only own appointments visible                   |
| FR-PAT-02 | Patient views Diagnosis and Treatment Plan summary for completed visits (not full clinical notes).                                          | BR-REQ-CLN-01 | Should Have  | TC-CLN-001              | Login as Patient; verify summary visible; full notes absent              |
| FR-PAT-03 | Patient updates own contact details (mobile, email); change logged in audit\_log.                                                           | BR-REQ-PR-04  | Should Have  | TC-PR-004               | Update mobile; verify saved; verify UPDATE in audit log                  |
| FR-PAT-04 | Patient views consent status and submits consent withdrawal request; System Administrator notified.                                         | DPDP-01       | Should Have  | TC-SEC-001              | Submit withdrawal; verify admin flag in MOD-06 dashboard                 |
| FR-PAT-05 | Public self-registration page accessible without authentication; linked from login screen. (CVH-CR-001)                                     | BR-PAT-07     | Must Have    | TC-PAT-SR-001           | Access app without login; verify Register link visible                   |
| FR-PAT-06 | Self-registration form: Full Name, DOB, Gender, Mobile, Password, Consent; duplicate detection applied. (CVH-CR-001)                        | BR-PAT-08     | Must Have    | TC-PAT-SR-002           | Register with existing Name+DOB+Mobile → duplicate warning shown         |
| FR-PAT-07 | On successful self-registration: auto-generate Patient ID, create account (username=mobile, role=Patient), auto-login patient. (CVH-CR-001) | BR-PAT-09     | Must Have    | TC-PAT-SR-003           | Complete registration → verify Patient ID, account, auto-login to MOD-07 |
| FR-PAT-08 | Password set during self-registration must meet complexity rules (BR-SEC-02); inline error on failure. (CVH-CR-001)                         | BR-SEC-02     | Must Have    | TC-PAT-SR-004           | Enter weak password → verify rejected with specific error                |

## 12. MOD-08: Dean & Admin Dashboard
**12.1 Functional Requirements**

|           |                                                                                                                                             |                  |              |                         |                                                                 |
|-----------|---------------------------------------------------------------------------------------------------------------------------------------------|------------------|--------------|-------------------------|-----------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                                                                                  | **BR Source**    | **Priority** | **Acceptance Test Ref** | **Testability Note**                                            |
| FR-RPT-01 | Dean dashboard shows KPI cards: Today's appointments, Completion Rate, No-Show Rate, Total Patients, New Registrations, Doctor Utilisation. | O-08             | Should Have  | TC-RPT-001              | Login as Dean; verify all KPI cards present with correct values |
| FR-RPT-02 | Daily Appointment Summary report with date range and doctor filters; table + chart.                                                         | RPT-01           | Should Have  | TC-RPT-001              | Run report; verify matches appointments table                   |
| FR-RPT-03 | Doctor Utilisation report; table + bar chart.                                                                                               | RPT-02           | Should Have  | TC-RPT-002              | Run report; verify utilisation % correct                        |
| FR-RPT-04 | No-Show and Cancellation report; table + chart.                                                                                             | RPT-04           | Should Have  | TC-RPT-004              | Create no-show; run report; verify entry appears                |
| FR-RPT-05 | Audit Activity and Compliance Status reports accessible to System Administrator and Dean.                                                   | RPT-05, RPT-06   | Should Have  | TC-RPT-005              | Login as each role; verify report access per permissions        |
| FR-RPT-06 | All reports support CSV export.                                                                                                             | RPT-01 to RPT-07 | Could Have   | TC-RPT-006              | Click export; verify valid CSV downloaded                       |

## 13. MOD-10: Audit & Compliance Log
**13.1 Functional Requirements**

|           |                                                                                         |               |              |                         |                                                               |
|-----------|-----------------------------------------------------------------------------------------|---------------|--------------|-------------------------|---------------------------------------------------------------|
| **FR ID** | **Functional Requirement**                                                              | **BR Source** | **Priority** | **Acceptance Test Ref** | **Testability Note**                                          |
| FR-AUD-01 | Every user action logged: User ID, Action Type, Module, Record Ref, Timestamp, Outcome. | BR-REQ-IT-02  | Must Have    | TC-IT-002               | Perform 5 actions; verify all 5 in audit\_log                 |
| FR-AUD-02 | Audit log read-only for all roles including System Administrator.                       | BR-REQ-IT-02  | Must Have    | TC-IT-002               | Login as System Administrator; verify no edit/delete controls |
| FR-AUD-03 | Failed logins logged outcome=Failed; account lock events logged action\_type=LOCK.      | BR-SEC-04     | Must Have    | TC-AM-004               | Trigger lockout; verify LOCK event in audit log               |
| FR-AUD-04 | Duplicate override at registration logged as DUPLICATE\_OVERRIDE with reason.           | BR-PAT-02     | Must Have    | TC-PR-002               | Trigger override; verify DUPLICATE\_OVERRIDE in audit log     |

## 14. Error Handling Specifications
*All error messages must be informative without exposing system internals, stack traces, or database details.*

|                                  |                                       |                                                                |                                                                                                      |                               |
|----------------------------------|---------------------------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------|-------------------------------|
| **Scenario**                     | **Trigger**                           | **System Behaviour**                                           | **User Message**                                                                                     | **Logged?**                   |
| Database unavailable             | SQLite connection fails               | Transaction rolled back; no partial write                      | Service temporarily unavailable. Please try again.                                                   | Yes – outcome=Failed          |
| Session timeout                  | Inactivity &gt;15 min                 | Session cleared; redirect to login                             | Your session has expired. Please log in again.                                                       | Yes – LOGOUT, outcome=Timeout |
| Duplicate patient                | Name+DOB+Mobile match on registration | Warning with existing Patient ID; actor may override or cancel | A patient with this name, DOB and mobile already exists. Patient ID: \[ID\].                         | Yes if overridden             |
| Appointment conflict             | Slot booked for same doctor+date+time | Booking rejected                                               | This slot is already booked. Please select a different time.                                         | No                            |
| Doctor daily maximum             | Count ≥ configured max                | All remaining slots unavailable                                | This doctor has reached the maximum appointments for this date.                                      | No                            |
| Account locked                   | failed\_login\_count = 3              | account\_status=Locked; further login blocked                  | Your account is locked. Contact your System Administrator.                                           | Yes – LOCK event              |
| Expired password                 | expiry\_date &lt; today on login      | Redirect to reset screen before any module access              | Your password has expired. Please set a new password.                                                | No                            |
| Consultation record locked       | is\_editable=0                        | Fields read-only; save controls hidden                         | This record is locked. Contact System Administrator for amendments.                                  | Yes – READ if accessed        |
| Consent not given                | Consent unchecked on registration     | Submit blocked                                                 | Consent to data processing is required.                                                              | No                            |
| Prescription before consultation | No saved consultation                 | Prescription save blocked                                      | Please save the consultation note before generating a prescription.                                  | No                            |
| Unauthorised module access       | RBAC violation                        | Redirect to home module                                        | You do not have access to this section.                                                              | Yes – READ, outcome=Failed    |
| Self-reg duplicate mobile        | Mobile already a username             | Registration blocked with advisory                             | A portal account with this mobile already exists. Please log in or contact the System Administrator. | No                            |

## 15. Security Functional Requirements
*Ties BRD security business rules (CVH-BRD-001 v1.3 Section 9.4) to system implementation behaviours.*

|           |                                                                                          |              |                                                                                  |              |                       |
|-----------|------------------------------------------------------------------------------------------|--------------|----------------------------------------------------------------------------------|--------------|-----------------------|
| **FR ID** | **Security Requirement**                                                                 | **BRD Rule** | **Implementation Behaviour**                                                     | **Priority** | **TC Ref**            |
| FR-SEC-01 | Unique username per user account; no shared credentials.                                 | BR-SEC-01    | username field UNIQUE constraint; duplicate rejected at creation                 | Must Have    | TC-SEC-003, TC-IT-001 |
| FR-SEC-02 | Password complexity enforced at account creation, self-registration, and password reset. | BR-SEC-02    | Regex validation: min 8 chars, 1 uppercase, 1 numeric, 1 special char            | Must Have    | TC-AM-007             |
| FR-SEC-03 | Password expiry every 90 days.                                                           | BR-SEC-03    | password\_expiry\_date checked on login; force reset if expired                  | Should Have  | TC-AM-008             |
| FR-SEC-04 | Account lockout after 3 consecutive failed logins.                                       | BR-SEC-04    | failed\_login\_count incremented; account\_status=Locked at 3; LOCK event logged | Must Have    | TC-AM-004             |
| FR-SEC-05 | Session timeout after 15 minutes of inactivity.                                          | BR-SEC-05    | last\_activity checked on every page load; session cleared if &gt;15 min         | Must Have    | TC-AM-003             |
| FR-SEC-06 | No concurrent login sessions for same account.                                           | BR-SEC-06    | Prototype: session\_state scoping; production: token registry                    | Should Have  | TC-SEC-010            |
| FR-SEC-07 | Inactive accounts (90 days no login) flagged and suspended.                              | BR-SEC-07    | last\_login\_timestamp checked; flagged in System Administrator dashboard        | Should Have  | TC-IT-001             |
| FR-SEC-08 | Patient consent withdrawal processed and System Administrator alerted.                   | BR-SEC-08    | Consent flag set; withdrawal event logged; alert in MOD-06 dashboard             | Should Have  | TC-SEC-008            |
| FR-SEC-09 | All SQL queries parameterised; no string interpolation in SQL.                           | T-NFR-04     | db\_utils.py uses ? placeholders exclusively                                     | Must Have    | TC-SEC-011            |
| FR-SEC-10 | Error messages do not expose system internals.                                           | T-NFR-05     | All exceptions handled; generic messages returned; no stack traces in UI         | Must Have    | TC-SEC-009            |

## 16. Database Schema
**16.1 Entity Relationship Overview**

Six core tables. patients (1) → appointments (many) → consultations (1) → prescriptions (many). appointments (1) → vitals (0..1). users linked as doctor\_id in appointments and recorded\_by in vitals. All user actions link to audit\_log. patients.linked\_user\_id FK → users.user\_id for portal access.

*Full ERD: CVH-ERD-001 v1.0*

**16.2 Table Definitions**

**patients**

|                            |          |                           |                                                       |
|----------------------------|----------|---------------------------|-------------------------------------------------------|
| **Column**                 | **Type** | **Constraints**           | **Notes**                                             |
| patient\_id                | TEXT     | PRIMARY KEY               | CVH-YYYY-NNNNN                                        |
| first\_name                | TEXT     | NOT NULL                  |                                                       |
| last\_name                 | TEXT     | NOT NULL                  |                                                       |
| date\_of\_birth            | TEXT     | NOT NULL                  | YYYY-MM-DD                                            |
| gender                     | TEXT     | NOT NULL                  |                                                       |
| mobile\_number             | TEXT     | NOT NULL                  | 10-digit string                                       |
| email\_address             | TEXT     |                           | Optional                                              |
| address\_line              | TEXT     |                           |                                                       |
| city                       | TEXT     |                           |                                                       |
| pincode                    | TEXT     |                           | 6-digit string                                        |
| emergency\_contact\_name   | TEXT     |                           |                                                       |
| emergency\_contact\_number | TEXT     |                           |                                                       |
| known\_allergies           | TEXT     |                           |                                                       |
| current\_medications       | TEXT     |                           |                                                       |
| existing\_eye\_conditions  | TEXT     |                           |                                                       |
| blood\_group               | TEXT     |                           |                                                       |
| consent\_given             | INTEGER  | NOT NULL DEFAULT 0        | 1=Yes, 0=No                                           |
| consent\_date              | TEXT     |                           | ISO 8601 datetime                                     |
| registration\_date         | TEXT     | NOT NULL                  | ISO 8601 datetime                                     |
| record\_status             | TEXT     | NOT NULL DEFAULT 'Active' | Active / Deactivated                                  |
| linked\_user\_id           | TEXT     |                           | FK → users.user\_id; set on self-reg or admin linking |

**users**

|                        |          |                           |                                                                       |
|------------------------|----------|---------------------------|-----------------------------------------------------------------------|
| **Column**             | **Type** | **Constraints**           | **Notes**                                                             |
| user\_id               | TEXT     | PRIMARY KEY               | USR-NNNNN                                                             |
| username               | TEXT     | NOT NULL UNIQUE           | Mobile number for self-registered patients                            |
| full\_name             | TEXT     | NOT NULL                  |                                                                       |
| password\_hash         | TEXT     | NOT NULL                  | bcrypt hash                                                           |
| role                   | TEXT     | NOT NULL                  | Patient/Receptionist/Doctor/Clinician/System Administrator/Dean-Admin |
| account\_status        | TEXT     | NOT NULL DEFAULT 'Active' | Active/Locked/Suspended/Deactivated                                   |
| failed\_login\_count   | INTEGER  | NOT NULL DEFAULT 0        | 0–3                                                                   |
| password\_expiry\_date | TEXT     |                           | YYYY-MM-DD                                                            |
| force\_password\_reset | INTEGER  | DEFAULT 0                 | 1=must reset on next login                                            |
| last\_login\_timestamp | TEXT     |                           | ISO 8601 datetime                                                     |
| created\_by            | TEXT     |                           | FK → users.user\_id or SELF-REG                                       |
| created\_date          | TEXT     | NOT NULL                  | ISO 8601 datetime                                                     |

**appointments**

|                      |          |                              |                                 |
|----------------------|----------|------------------------------|---------------------------------|
| **Column**           | **Type** | **Constraints**              | **Notes**                       |
| appointment\_id      | TEXT     | PRIMARY KEY                  | APT-YYYY-NNNNN                  |
| patient\_id          | TEXT     | NOT NULL, FK → patients      |                                 |
| doctor\_id           | TEXT     | NOT NULL, FK → users         | Doctor role only                |
| appointment\_date    | TEXT     | NOT NULL                     | YYYY-MM-DD                      |
| appointment\_time    | TEXT     | NOT NULL                     | HH:MM 24hr; 20-min blocks       |
| visit\_type          | TEXT     | NOT NULL                     | New/Follow-Up/Emergency/Walk-In |
| appointment\_status  | TEXT     | NOT NULL DEFAULT 'Scheduled' |                                 |
| notes                | TEXT     |                              |                                 |
| cancellation\_reason | TEXT     |                              | Mandatory if Cancelled          |
| booked\_by\_user     | TEXT     | NOT NULL, FK → users         |                                 |
| booking\_timestamp   | TEXT     | NOT NULL                     | ISO 8601 datetime               |

**consultations**

|                       |          |                                    |                                  |
|-----------------------|----------|------------------------------------|----------------------------------|
| **Column**            | **Type** | **Constraints**                    | **Notes**                        |
| consultation\_id      | TEXT     | PRIMARY KEY                        | CON-YYYY-NNNNN                   |
| appointment\_id       | TEXT     | NOT NULL UNIQUE, FK → appointments | One consultation per appointment |
| patient\_id           | TEXT     | NOT NULL, FK → patients            |                                  |
| doctor\_id            | TEXT     | NOT NULL, FK → users               | Treating doctor                  |
| chief\_complaint      | TEXT     | NOT NULL                           |                                  |
| examination\_findings | TEXT     | NOT NULL                           |                                  |
| diagnosis             | TEXT     | NOT NULL                           |                                  |
| management\_plan      | TEXT     | NOT NULL                           |                                  |
| follow\_up\_required  | INTEGER  | DEFAULT 0                          | 1=Yes                            |
| follow\_up\_date      | TEXT     |                                    | Required if follow\_up=1         |
| created\_timestamp    | TEXT     | NOT NULL                           | ISO 8601 datetime                |
| is\_editable          | INTEGER  | NOT NULL DEFAULT 1                 | 0 after 24 hrs                   |

**prescriptions**

|                       |          |                              |                   |
|-----------------------|----------|------------------------------|-------------------|
| **Column**            | **Type** | **Constraints**              | **Notes**         |
| prescription\_id      | TEXT     | PRIMARY KEY                  | RX-YYYY-NNNNN     |
| consultation\_id      | TEXT     | NOT NULL, FK → consultations |                   |
| patient\_id           | TEXT     | NOT NULL, FK → patients      |                   |
| drug\_name            | TEXT     | NOT NULL                     |                   |
| dosage                | TEXT     | NOT NULL                     |                   |
| frequency             | TEXT     | NOT NULL                     |                   |
| duration              | TEXT     | NOT NULL                     |                   |
| special\_instructions | TEXT     |                              |                   |
| prescribed\_date      | TEXT     | NOT NULL                     | ISO 8601 datetime |

**vitals**

|                        |          |                             |                              |
|------------------------|----------|-----------------------------|------------------------------|
| **Column**             | **Type** | **Constraints**             | **Notes**                    |
| vitals\_id             | TEXT     | PRIMARY KEY                 | VIT-NNNNN                    |
| appointment\_id        | TEXT     | NOT NULL, FK → appointments |                              |
| patient\_id            | TEXT     | NOT NULL, FK → patients     |                              |
| recorded\_by           | TEXT     | NOT NULL, FK → users        | Clinician/Nurse role only    |
| visual\_acuity\_re     | TEXT     | NOT NULL                    | Snellen notation             |
| visual\_acuity\_le     | TEXT     | NOT NULL                    | Snellen notation             |
| iop\_re                | REAL     |                             | mmHg 1–60; amber flag &gt;21 |
| iop\_le                | REAL     |                             | mmHg 1–60; amber flag &gt;21 |
| blood\_pressure        | TEXT     |                             | NNN/NN mmHg                  |
| weight\_kg             | REAL     |                             | 1–300 kg                     |
| pre\_procedure\_notes  | TEXT     |                             |                              |
| post\_procedure\_notes | TEXT     |                             |                              |
| vitals\_timestamp      | TEXT     | NOT NULL                    | ISO 8601 datetime            |

**audit\_log**

|                    |          |                           |                                                                                |
|--------------------|----------|---------------------------|--------------------------------------------------------------------------------|
| **Column**         | **Type** | **Constraints**           | **Notes**                                                                      |
| log\_id            | INTEGER  | PRIMARY KEY AUTOINCREMENT | Never deleted or modified                                                      |
| user\_id           | TEXT     | NOT NULL                  | FK → users.user\_id                                                            |
| action\_type       | TEXT     | NOT NULL                  | LOGIN/LOGOUT/CREATE/READ/UPDATE/DELETE/LOCK/UNLOCK/DUPLICATE\_OVERRIDE         |
| module             | TEXT     | NOT NULL                  | MOD-01 to MOD-10                                                               |
| record\_reference  | TEXT     |                           | Entity ID; NULL for system events; polymorphic — not enforced as relational FK |
| action\_timestamp  | TEXT     | NOT NULL                  | ISO 8601 HH:MM:SS precision                                                    |
| ip\_address        | TEXT     |                           | localhost in prototype                                                         |
| outcome            | TEXT     | NOT NULL                  | Success / Failed                                                               |
| additional\_detail | TEXT     |                           | Context or reason                                                              |

## 17. Technical Non-Functional Requirements
*Moved from BRD per BA review. Business NFRs in CVH-BRD-001 v1.3 Section 11.*

|            |                   |                                                                                                                     |                                                                   |
|------------|-------------------|---------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| **Req ID** | **Category**      | **Specification**                                                                                                   | **Acceptance Criteria**                                           |
| T-NFR-01   | Maintainability   | One Python file per module. Module-level docstrings and inline comments on all non-trivial logic.                   | Code review confirms module separation; all files have docstrings |
| T-NFR-02   | Portability       | Application runs via: pip install -r requirements.txt then streamlit run app.py. No proprietary dependencies.       | Successful installation on clean environment                      |
| T-NFR-03   | Scalability       | All DB queries in db\_utils.py only; parameterised statements. Future DB swap requires modifying db\_utils.py only. | DB replacement test: only db\_utils.py changes needed             |
| T-NFR-04   | SQL Security      | All SQL queries use ? placeholders. No user input interpolated directly into SQL strings.                           | Code review + basic injection test during UAT                     |
| T-NFR-05   | Error Handling    | All DB operations in try-except. User-facing messages must not expose stack traces or internal details.             | Error simulation; verify no stack traces in UI                    |
| T-NFR-06   | Session Integrity | Session state validated on every page load. Direct URL access without valid session → redirect to login.            | Direct URL access test; verify redirect                           |

## 18. BRD-to-FRD Traceability Summary (v1.2)
*Full chain in CVH-RTM-001 v1.1. Column FR ID (v1.2) — includes all requirements through CVH-CR-001.*

|                  |                                                   |                                 |                    |
|------------------|---------------------------------------------------|---------------------------------|--------------------|
| **BRD Req ID**   | **BRD Requirement (Summary)**                     | **FR ID (v1.2)**                | **FRD Section**    |
| BR-REQ-PR-01     | Digital patient registration                      | FR-PR-01                        | Section 5.1        |
| BR-REQ-PR-02     | Combination duplicate detection (Name+DOB+Mobile) | FR-PR-02                        | Section 5.1, 5.2   |
| BR-REQ-PR-03     | Consent; submission blocked without it            | FR-PR-03                        | Section 5.1        |
| BR-REQ-PR-04     | Record retrieval and role-restricted editing      | FR-PR-04, FR-PAT-01             | Sections 5.1, 11.1 |
| BR-REQ-PR-05     | Ophthalmology medical history captured            | FR-PR-05                        | Section 5.1        |
| BR-REQ-APT-01    | Digital scheduling with conflict detection        | FR-APT-01, FR-APT-02            | Section 6.1        |
| BR-REQ-APT-02    | Appointment status lifecycle                      | FR-APT-03, FR-REC-01, FR-REC-02 | Sections 6.1, 9.1  |
| BR-REQ-APT-03    | Emergency and walk-in                             | FR-APT-04                       | Section 6.1        |
| BR-REQ-APT-04    | Cancellation/reschedule with reason               | FR-APT-05, FR-REC-03            | Sections 6.1, 9.1  |
| BR-REQ-APT-05    | No-show identification                            | FR-APT-06                       | Section 6.1        |
| BR-REQ-CLN-01    | Structured consultation notes                     | FR-CLN-01 to FR-CLN-03          | Section 7.1        |
| BR-REQ-CLN-02    | Digital prescription linked to consultation       | FR-CLN-04                       | Section 7.1        |
| BR-REQ-CLN-03    | Clinician vitals recording                        | FR-CLN-07 to FR-CLN-10          | Section 8.1        |
| BR-REQ-CLN-04    | Immutable audit trail (24-hr lock)                | FR-CLN-05                       | Section 7.1        |
| BR-REQ-CLN-05    | Investigation orders linked to visit              | FR-CLN-06                       | Section 7.1        |
| BR-REQ-AM-01     | Authentication before access                      | FR-AM-01                        | Section 4.1        |
| BR-REQ-AM-02     | RBAC minimum necessary access                     | FR-AM-02                        | Sections 4.1, 2.3  |
| BR-REQ-AM-03     | Session timeout                                   | FR-AM-03, FR-SEC-05             | Sections 4.1, 15   |
| BR-REQ-AM-04     | Account lockout                                   | FR-AM-04, FR-SEC-04             | Sections 4.1, 15   |
| BR-REQ-IT-01     | User account management                           | FR-IT-01                        | Section 10.1       |
| BR-REQ-IT-02     | Tamper-evident audit log                          | FR-AUD-01 to FR-AUD-04          | Section 13.1       |
| BR-REQ-IT-03     | System health dashboard                           | FR-IT-03                        | Section 10.1       |
| BR-PAT-07        | Patient self-registration via public page         | FR-PAT-05                       | Section 11.1       |
| BR-PAT-08        | Self-reg form with duplicate detection            | FR-PAT-06                       | Section 11.1       |
| BR-PAT-09        | Auto Patient ID + account + auto-login            | FR-PAT-07                       | Section 11.1       |
| BR-SEC-02        | Password complexity at self-registration          | FR-PAT-08                       | Section 11.1       |
| RPT-01 to RPT-07 | Management reporting                              | FR-RPT-01 to FR-RPT-06          | Section 12.1       |

## 19. Sign-Off & Next Steps
**19.1 FRD v1.2 Approval Criteria**

|                                                         |                    |            |
|---------------------------------------------------------|--------------------|------------|
| **Criterion**                                           | **Owner**          | **Status** |
| All FR specifications verified against CVH-BRD-001 v1.3 | Prashant Gore      | Pending    |
| UC-05 (self-registration) flow reviewed by Dean         | Dean               | Pending    |
| Error handling confirmed by Developer                   | Developer          | Pending    |
| Security FR section reviewed by Compliance Officer      | Compliance Officer | Pending    |
| DB schema approved by Developer                         | Developer          | Pending    |
| FRD v1.2 signed off by Dean                             | Dean               | Pending    |

**19.2 Next Documents**

|                                  |                  |            |
|----------------------------------|------------------|------------|
| **Document**                     | **ID**           | **Status** |
| Requirements Traceability Matrix | CVH-RTM-001 v1.1 | Complete   |
| Entity Relationship Diagram      | CVH-ERD-001 v1.0 | Complete   |
| Sequence Diagrams                | CVH-SQD-001 v1.1 | Complete   |
| System Test Cases                | CVH-STC-001 v1.1 | Complete   |
| UAT Scripts                      | CVH-UAT-001 v1.1 | Complete   |
| Prototype                        | CVH-DEV-001 v1.0 | Complete   |

**END OF DOCUMENT**
