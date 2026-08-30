---
hide:
  - toc
---

<div class="ba-meta-bar" markdown>
<span class="ba-badge ba-badge--id">CVH-STC-001</span> <span class="ba-badge ba-badge--version">Version 1.1</span> <span class="ba-badge ba-badge--status">Baselined</span> <span class="ba-badge ba-badge--compliance">DPDP / HIPAA / GDPR</span>
</div>

# System Test Cases (STC)

<div class="ba-table-scroll" markdown>

|                  |                                                                           |
|------------------|---------------------------------------------------------------------------|
| Document ID      | CVH-STC-001                                                               |
| Version          | 1.1 – CVH-CR-001 Amendment                                                |
| Date             | July 2026                                                                 |
| Prepared By      | Prashant Gore – BA & Digital Transformation Consultant                    |
| Parent Documents | CVH-BRD-001 v1.3 \| CVH-FRD-001 v1.2 \| CVH-RTM-001 v1.1                  |
| Total Test Cases | 55 (51 original + 4 from CVH-CR-001) — see Section 2 for domain breakdown |
| Status           | DRAFT – Awaiting Execution                                                |

> *DISCLAIMER: Prototype demonstration project only. No real patient data. Not for production clinical deployment.*

## 1. Document Control
|             |           |               |                                                                                                                                                                                                                                       |            |
|-------------|-----------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **Version** | **Date**  | **Author**    | **Description**                                                                                                                                                                                                                       | **Status** |
| 1.0         | June 2026 | Prashant Gore | Initial STC — 39 test cases                                                                                                                                                                                                           | Superseded |
| 1.1         | July 2026 | Prashant Gore | CVH-CR-001: TC-PAT-SR-001 to 004 added; TC-SEC-011 added for FR-SEC-09 (SQL Injection); total corrected to 55 unique test cases; TC-AM-009 corrected to FR-AM-09 (Force Password Reset); Section 8 header range updated to TC-SEC-011 | Draft      |

*Test case structure: ID \| Name \| Module \| FR Reference \| Priority \| Preconditions \| Test Steps \| Expected Result \| Negative Test \| Status*

*FR-AM-06 to FR-AM-09 are defined in FRD v1.2 Section 4.2 (Password Policy). FR-AM-01 to FR-AM-05 are in Section 4.1 (Login & Session).*

*Performance, load, and penetration testing are out of scope for this STC. These require separate specialised test plans.*

## 2. Test Coverage Summary
|                                    |                      |           |                                             |               |                 |                |
|------------------------------------|----------------------|-----------|---------------------------------------------|---------------|-----------------|----------------|
| **Domain**                         | **TC IDs**           | **Count** | **FR Coverage**                             | **Must Have** | **Should Have** | **Could Have** |
| Patient Registration               | TC-PR-001 to 005     | 5         | FR-PR-01 to 05                              | 5             | 0               | 0              |
| Appointment Management             | TC-APT-001 to 006    | 6         | FR-APT-01 to 06                             | 4             | 2               | 0              |
| Clinical Documentation             | TC-CLN-001 to 006    | 6         | FR-CLN-01 to 10                             | 4             | 2               | 0              |
| Access Management                  | TC-AM-001 to 009     | 9         | FR-AM-01 to 09 (Sections 4.1 and 4.2)       | 6             | 3               | 0              |
| IT Administration                  | TC-IT-001 to 004     | 4         | FR-IT-01 to 04, FR-AUD-01 to 04             | 2             | 2               | 0              |
| Security                           | TC-SEC-001 to 011    | 11        | FR-SEC-01 to 10 + FR-SEC-09 (SQL injection) | 9             | 2               | 0              |
| User Experience                    | TC-UX-001 to 003     | 3         | FR-AM-02, T-NFR-02 (UX covered by NFRs)     | 0             | 3               | 0              |
| Reporting                          | TC-RPT-001 to 007    | 7         | FR-RPT-01 to 06                             | 0             | 6               | 1              |
| Patient Self-Registration (CR-001) | TC-PAT-SR-001 to 004 | 4         | FR-PAT-05 to 08                             | 4             | 0               | 0              |
| TOTAL                              | —                    | 55        | 43 FR IDs covered (65 FRs in FRD v1.2)      | 34            | 20              | 1              |

*Total unique test cases = 55. Priority breakdown: 34 Must Have + 20 Should Have + 1 Could Have (TC-RPT-007) = 55. TC-SEC-011 added for FR-SEC-09 (SQL Injection Prevention) which was displaced when TC-AM-009 was corrected to FR-AM-09 (Force Password Reset).*

## 3. Patient Registration — TC-PR-001 to TC-PR-005
|                                                    |                                                                                                                                                                                        |
|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PR-001 \| Register New Patient — Happy Path** |                                                                                                                                                                                        |
| **Module**                                         | MOD-01                                                                                                                                                                                 |
| **FR Reference (CVH-FRD-001 v1.2)**                | FR-PR-01                                                                                                                                                                               |
| **Priority**                                       | Must Have                                                                                                                                                                              |
| **Preconditions**                                  | User logged in as Receptionist. No existing record for test patient.                                                                                                                   |
| **Test Steps**                                     | 1\. Navigate to MOD-01 Patient Registration. 2. Enter: First='Test', Last='Patient', DOB='01/01/1990', Gender='Male', Mobile='9876543210'. 3. Check consent checkbox. 4. Click Submit. |
| **Expected Result**                                | Patient record created. Patient ID generated (CVH-YYYY-NNNNN). Success message displayed. Record retrievable by search.                                                                |
| **Negative Test**                                  | Submit with consent unchecked → blocked. Submit with mandatory field empty → field highlighted red; no record created.                                                                 |
| **Status**                                         | Planned                                                                                                                                                                                |
|                                                    |                                                                                                                                                                                        |

|                                                                  |                                                                                                                                                                                |
|------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PR-002 \| Duplicate Patient Detection — Combination Logic** |                                                                                                                                                                                |
| **Module**                                                       | MOD-01                                                                                                                                                                         |
| **FR Reference (CVH-FRD-001 v1.2)**                              | FR-PR-02                                                                                                                                                                       |
| **Priority**                                                     | Must Have                                                                                                                                                                      |
| **Preconditions**                                                | Patient 'Test Patient, DOB 01/01/1990, Mobile 9876543210' already registered.                                                                                                  |
| **Test Steps**                                                   | 1\. Attempt registration with same First Name, Last Name, DOB, Mobile. 2. Observe warning. 3. Attempt registration with SAME mobile but DIFFERENT first name ('John Patient'). |
| **Expected Result**                                              | Step 1: Warning shown with existing Patient ID. Override option presented. Step 3: NO duplicate warning. New record created — mobile alone does not trigger duplicate alert.   |
| **Negative Test**                                                | Override without entering reason → blocked. Same mobile different name must NOT trigger warning (combination logic only).                                                      |
| **Status**                                                       | Planned                                                                                                                                                                        |
|                                                                  |                                                                                                                                                                                |

|                                                           |                                                                                                                 |
|-----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **TC-PR-003 \| Consent Not Given — Registration Blocked** |                                                                                                                 |
| **Module**                                                | MOD-01                                                                                                          |
| **FR Reference (CVH-FRD-001 v1.2)**                       | FR-PR-03                                                                                                        |
| **Priority**                                              | Must Have                                                                                                       |
| **Preconditions**                                         | Receptionist logged in. All mandatory fields completed.                                                         |
| **Test Steps**                                            | 1\. Complete all mandatory fields. 2. Leave consent checkbox unchecked. 3. Attempt to submit.                   |
| **Expected Result**                                       | Submit blocked. Message: 'Consent is required to complete registration.' No patient record created in database. |
| **Negative Test**                                         | Verify DB: no partial record inserted. consent\_given=0 must never appear in a saved record.                    |
| **Status**                                                | Planned                                                                                                         |
|                                                           |                                                                                                                 |

|                                           |                                                                                                                                                          |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PR-004 \| Role-Based Record Access** |                                                                                                                                                          |
| **Module**                                | MOD-01                                                                                                                                                   |
| **FR Reference (CVH-FRD-001 v1.2)**       | FR-PR-04                                                                                                                                                 |
| **Priority**                              | Must Have                                                                                                                                                |
| **Preconditions**                         | Patient record exists. Doctor and Receptionist accounts active.                                                                                          |
| **Test Steps**                            | 1\. Login as Receptionist. Search patient. Edit mobile number. Save. 2. Login as Doctor. Search same patient. Attempt to access edit controls.           |
| **Expected Result**                       | Receptionist: edit saves. Audit log: UPDATE event recorded. Doctor: edit controls absent. URL manipulation redirects to home with access denied message. |
| **Negative Test**                         | Doctor must not save demographic changes via any method including direct URL manipulation.                                                               |
| **Status**                                | Planned                                                                                                                                                  |
|                                           |                                                                                                                                                          |

|                                                              |                                                                                                                                     |
|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PR-005 \| Medical History Visible in Doctor Dashboard** |                                                                                                                                     |
| **Module**                                                   | MOD-01                                                                                                                              |
| **FR Reference (CVH-FRD-001 v1.2)**                          | FR-PR-05                                                                                                                            |
| **Priority**                                                 | Must Have                                                                                                                           |
| **Preconditions**                                            | Patient registered with Allergies='Penicillin', Eye Conditions='Glaucoma'. Appointment In-Progress.                                 |
| **Test Steps**                                               | 1\. Login as Doctor. 2. Open In-Progress appointment. 3. View Patient Card.                                                         |
| **Expected Result**                                          | Known Allergies, Current Medications, and Eye Conditions all visible in Patient Card within MOD-03. Values match registration data. |
| **Negative Test**                                            | Receptionist views patient record: medical history visible read-only. Patient portal: medical history NOT exposed to patient.       |
| **Status**                                                   | Planned                                                                                                                             |
|                                                              |                                                                                                                                     |

## 4. Appointment Management — TC-APT-001 to TC-APT-006
|                                                         |                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-APT-001 \| Book Appointment + Conflict Detection** |                                                                                                                                                                                                                                                                  |
| **Module**                                              | MOD-02                                                                                                                                                                                                                                                           |
| **FR Reference (CVH-FRD-001 v1.2)**                     | FR-APT-01, FR-APT-02                                                                                                                                                                                                                                             |
| **Priority**                                            | Must Have                                                                                                                                                                                                                                                        |
| **Preconditions**                                       | Active patient and doctor exist. Date is not a holiday. Booking context stored in session state.                                                                                                                                                                 |
| **Test Steps**                                          | 1\. Login as Receptionist. Navigate to MOD-02. 2. Search patient. Select doctor. Select future date. Select Visit Type. 3. Click Check Availability. Select slot 09:00. Click Confirm Booking. 4. Attempt same doctor, date, slot 09:00 for a different patient. |
| **Expected Result**                                     | Step 3: Appointment created. ID generated (APT-YYYY-NNNNN). Status=Scheduled. Step 4: Slot 09:00 unavailable. Error: 'This slot is already booked.'                                                                                                              |
| **Negative Test**                                       | Select holiday date → no slots shown, date blocked. Submit without patient → error. Submit without visit type → error.                                                                                                                                           |
| **Status**                                              | Planned                                                                                                                                                                                                                                                          |
|                                                         |                                                                                                                                                                                                                                                                  |

|                                                |                                                                                                                                                                                               |
|------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-APT-002 \| Appointment Status Lifecycle** |                                                                                                                                                                                               |
| **Module**                                     | MOD-02                                                                                                                                                                                        |
| **FR Reference (CVH-FRD-001 v1.2)**            | FR-APT-03                                                                                                                                                                                     |
| **Priority**                                   | Must Have                                                                                                                                                                                     |
| **Preconditions**                              | Appointment status=Scheduled. Clinician and Doctor accounts active.                                                                                                                           |
| **Test Steps**                                 | 1\. Receptionist: Check In → verify Checked-In. 2. Doctor: Open appointment → In-Progress. 3. Doctor: Complete consultation → Completed. 4. Verify each status in queue and Doctor dashboard. |
| **Expected Result**                            | Each transition correct and sequential. Audit log: UPDATE at each transition. Patient visible in Clinician Panel after Check-In.                                                              |
| **Negative Test**                              | Check-in &gt;30 min before slot → blocked with timing message. Attempt In-Progress without Checked-In → denied.                                                                               |
| **Status**                                     | Planned                                                                                                                                                                                       |
|                                                |                                                                                                                                                                                               |

|                                                     |                                                                                                                            |
|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **TC-APT-003 \| Emergency and Walk-In Appointment** |                                                                                                                            |
| **Module**                                          | MOD-02                                                                                                                     |
| **FR Reference (CVH-FRD-001 v1.2)**                 | FR-APT-04                                                                                                                  |
| **Priority**                                        | Must Have                                                                                                                  |
| **Preconditions**                                   | Active patient exists. At least one available slot today.                                                                  |
| **Test Steps**                                      | 1\. Create appointment with Visit Type='Emergency'. Verify queue label. 2. Create Walk-In appointment. Verify designation. |
| **Expected Result**                                 | Emergency appears in queue with Emergency label. Walk-In booking succeeds. Both recorded correctly.                        |
| **Negative Test**                                   | Emergency booking on fully-booked date → daily max check applies; rejected.                                                |
| **Status**                                          | Planned                                                                                                                    |
|                                                     |                                                                                                                            |

|                                                         |                                                                                                                                                                                     |
|---------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-APT-004 \| Cancellation + Late Cancellation Flag** |                                                                                                                                                                                     |
| **Module**                                              | MOD-02                                                                                                                                                                              |
| **FR Reference (CVH-FRD-001 v1.2)**                     | FR-APT-05                                                                                                                                                                           |
| **Priority**                                            | Must Have                                                                                                                                                                           |
| **Preconditions**                                       | Scheduled appointment exists. One appointment within 1 hour of current time.                                                                                                        |
| **Test Steps**                                          | 1\. Cancel without reason → verify blocked. 2. Cancel with reason → verify Cancelled status and audit. 3. Cancel appointment within 1 hour of slot → verify Late Cancellation flag. |
| **Expected Result**                                     | Step 1: Blocked; reason field highlighted. Step 2: Status=Cancelled; reason stored; audit UPDATE recorded. Step 3: Late Cancellation flag visible.                                  |
| **Negative Test**                                       | Cancelled appointment must not appear in active schedule. Slot becomes available for rebooking.                                                                                     |
| **Status**                                              | Planned                                                                                                                                                                             |
|                                                         |                                                                                                                                                                                     |

|                                           |                                                                                                                                     |
|-------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **TC-APT-005 \| No-Show Auto-Assignment** |                                                                                                                                     |
| **Module**                                | MOD-02                                                                                                                              |
| **FR Reference (CVH-FRD-001 v1.2)**       | FR-APT-06                                                                                                                           |
| **Priority**                              | Should Have                                                                                                                         |
| **Preconditions**                         | Appointment status=Scheduled. Appointment time is 15+ minutes in the past.                                                          |
| **Test Steps**                            | 1\. Set appointment time to 15+ minutes before current time without checking in. 2. Trigger no-show check. 3. Verify status update. |
| **Expected Result**                       | Appointment status=No-Show. Reflected in admin reports. Audit records status change.                                                |
| **Negative Test**                         | No-Show must NOT fire for Checked-In appointments. Cancelled appointments excluded from check.                                      |
| **Status**                                | Planned                                                                                                                             |
|                                           |                                                                                                                                     |

|                                                    |                                                                                                      |
|----------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **TC-APT-006 \| Doctor Daily Maximum Enforcement** |                                                                                                      |
| **Module**                                         | MOD-02                                                                                               |
| **FR Reference (CVH-FRD-001 v1.2)**                | FR-APT-01                                                                                            |
| **Priority**                                       | Must Have                                                                                            |
| **Preconditions**                                  | Doctor has 24 appointments for test date.                                                            |
| **Test Steps**                                     | 1\. Attempt to book a 25th appointment for same doctor on same date.                                 |
| **Expected Result**                                | All remaining slots unavailable. Error: 'Doctor has reached the maximum appointments for this date.' |
| **Negative Test**                                  | Different doctor on same date unaffected. Emergency appointments also subject to daily maximum.      |
| **Status**                                         | Planned                                                                                              |
|                                                    |                                                                                                      |

## 5. Clinical Documentation — TC-CLN-001 to TC-CLN-006
|                                                        |                                                                                                                                                                   |
|--------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-CLN-001 \| Enter Consultation Note — Happy Path** |                                                                                                                                                                   |
| **Module**                                             | MOD-03                                                                                                                                                            |
| **FR Reference (CVH-FRD-001 v1.2)**                    | FR-CLN-01, FR-CLN-02, FR-CLN-03                                                                                                                                   |
| **Priority**                                           | Must Have                                                                                                                                                         |
| **Preconditions**                                      | Appointment status=In-Progress. Doctor logged in. Vitals recorded.                                                                                                |
| **Test Steps**                                         | 1\. Login as Doctor. Open In-Progress appointment. 2. Verify demographics, history, vitals visible. 3. Enter Chief Complaint, Findings, Diagnosis, Plan. 4. Save. |
| **Expected Result**                                    | Consultation saved. Linked to appointment\_id. doctor\_id and timestamp recorded. is\_editable=1. Audit: CREATE in MOD-03.                                        |
| **Negative Test**                                      | Save with Diagnosis empty → blocked; field highlighted. No partial record inserted.                                                                               |
| **Status**                                             | Planned                                                                                                                                                           |
|                                                        |                                                                                                                                                                   |

|                                                       |                                                                                                                          |
|-------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| **TC-CLN-002 \| Prescription Linked to Consultation** |                                                                                                                          |
| **Module**                                            | MOD-03                                                                                                                   |
| **FR Reference (CVH-FRD-001 v1.2)**                   | FR-CLN-04                                                                                                                |
| **Priority**                                          | Must Have                                                                                                                |
| **Preconditions**                                     | Consultation note saved for In-Progress appointment.                                                                     |
| **Test Steps**                                        | 1\. Add drug: Name='Timolol', Dosage='0.5%', Frequency='Twice daily', Duration='30 days'. 2. Add second drug line. Save. |
| **Expected Result**                                   | Both drug lines saved. Each linked to consultation\_id. Prescription visible in Patient Portal summary.                  |
| **Negative Test**                                     | Attempt prescription before saving consultation → blocked: 'Save consultation note first.'                               |
| **Status**                                            | Planned                                                                                                                  |
|                                                       |                                                                                                                          |

|                                                       |                                                                                                                                                            |
|-------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-CLN-003 \| Clinician Records Vitals + IOP Flag** |                                                                                                                                                            |
| **Module**                                            | MOD-04                                                                                                                                                     |
| **FR Reference (CVH-FRD-001 v1.2)**                   | FR-CLN-07, FR-CLN-08, FR-CLN-09, FR-CLN-10                                                                                                                 |
| **Priority**                                          | Must Have                                                                                                                                                  |
| **Preconditions**                                     | Appointment status=Checked-In. Clinician logged in.                                                                                                        |
| **Test Steps**                                        | 1\. Login as Clinician. Open patient. 2. Enter VA RE=6/6, VA LE=6/9, IOP RE=24 (above normal), BP=120/80. 3. Save. 4. Login as Doctor. Check Patient Card. |
| **Expected Result**                                   | Vitals saved. IOP RE=24 triggers amber advisory (not blocking). Vitals visible in Doctor's Patient Card. Audit: CREATE in MOD-04.                          |
| **Negative Test**                                     | Doctor: vitals input controls absent (read-only). Receptionist: vitals not visible.                                                                        |
| **Status**                                            | Planned                                                                                                                                                    |
|                                                       |                                                                                                                                                            |

|                                                            |                                                                                                   |
|------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| **TC-CLN-004 \| Consultation Record Locks After 24 Hours** |                                                                                                   |
| **Module**                                                 | MOD-03                                                                                            |
| **FR Reference (CVH-FRD-001 v1.2)**                        | FR-CLN-05                                                                                         |
| **Priority**                                               | Must Have                                                                                         |
| **Preconditions**                                          | Consultation record with created\_timestamp &gt;24 hours ago. is\_editable=0.                     |
| **Test Steps**                                             | 1\. Login as Doctor. Open locked consultation. 2. Attempt to edit Diagnosis. 3. Attempt Save.     |
| **Expected Result**                                        | Fields read-only. Save button hidden. Message: 'This record has been locked.' No DB changes.      |
| **Negative Test**                                          | is\_editable=0 enforced in business logic not just UI. Audit records READ only — no UPDATE event. |
| **Status**                                                 | Planned                                                                                           |
|                                                            |                                                                                                   |

|                                                       |                                                                                                           |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| **TC-CLN-005 \| Investigation Order Linked to Visit** |                                                                                                           |
| **Module**                                            | MOD-03                                                                                                    |
| **FR Reference (CVH-FRD-001 v1.2)**                   | FR-CLN-06                                                                                                 |
| **Priority**                                          | Should Have                                                                                               |
| **Preconditions**                                     | Consultation saved for active appointment.                                                                |
| **Test Steps**                                        | 1\. Add investigation: Type='OCT Scan', Instructions='Both eyes'. 2. Save order.                          |
| **Expected Result**                                   | Order saved. Linked to appointment\_id and patient\_id. Visible in patient record history. Audit: CREATE. |
| **Negative Test**                                     | Investigation order without linked appointment → system rejects. Order linked to correct visit only.      |
| **Status**                                            | Planned                                                                                                   |
|                                                       |                                                                                                           |

|                                                            |                                                                                                                    |
|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **TC-CLN-006 \| Complete Consultation Triggers Check-Out** |                                                                                                                    |
| **Module**                                                 | MOD-03                                                                                                             |
| **FR Reference (CVH-FRD-001 v1.2)**                        | FR-CLN-03                                                                                                          |
| **Priority**                                               | Must Have                                                                                                          |
| **Preconditions**                                          | Consultation and prescription saved. Appointment=In-Progress.                                                      |
| **Test Steps**                                             | 1\. Doctor clicks Complete Consultation. 2. Verify appointment status. 3. Login as Receptionist. Check queue.      |
| **Expected Result**                                        | Appointment status=Completed. Check-out available in MOD-05. Receptionist queue reflects Completed. Audit: UPDATE. |
| **Negative Test**                                          | Complete without consultation note → blocked. is\_editable window starts from created\_timestamp.                  |
| **Status**                                                 | Planned                                                                                                            |
|                                                            |                                                                                                                    |

## 6. Access Management — TC-AM-001 to TC-AM-009
*FR-AM-01 to FR-AM-05 defined in FRD v1.2 Section 4.1 (Login & Session). FR-AM-06 to FR-AM-09 defined in FRD v1.2 Section 4.2 (Password Policy).*

|                                                 |                                                                                                                        |
|-------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-001 \| Unauthenticated Access Blocked** |                                                                                                                        |
| **Module**                                      | MOD-09                                                                                                                 |
| **FR Reference (CVH-FRD-001 v1.2)**             | FR-AM-01                                                                                                               |
| **Priority**                                    | Must Have                                                                                                              |
| **Preconditions**                               | Application running. No active session.                                                                                |
| **Test Steps**                                  | 1\. Open browser to application URL without logging in. 2. Attempt direct access to MOD-01 URL. 3. Attempt MOD-03 URL. |
| **Expected Result**                             | All URLs redirect to login page. No module content rendered. No READ events in audit for unauthenticated attempts.     |
| **Negative Test**                               | Session manipulation attempt → session invalid; redirect to login.                                                     |
| **Status**                                      | Planned                                                                                                                |
|                                                 |                                                                                                                        |

|                                                             |                                                                                                                                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-002 \| RBAC — Role Segregation Across All 6 Roles** |                                                                                                                                                                                                                                                                                                                                                         |
| **Module**                                                  | MOD-09                                                                                                                                                                                                                                                                                                                                                  |
| **FR Reference (CVH-FRD-001 v1.2)**                         | FR-AM-02                                                                                                                                                                                                                                                                                                                                                |
| **Priority**                                                | Must Have                                                                                                                                                                                                                                                                                                                                               |
| **Preconditions**                                           | One account per role active.                                                                                                                                                                                                                                                                                                                            |
| **Test Steps**                                              | 1\. Login as Patient → verify only MOD-07 accessible. 2. Login as Receptionist → verify MOD-01/02/05; MOD-03/06 blocked. 3. Login as Doctor → verify MOD-03; MOD-01 blocked. 4. Login as Clinician → verify MOD-04; MOD-03 read-only. 5. Login as System Administrator → verify MOD-06/10; no clinical modules. 6. Login as Dean-Admin → verify MOD-08. |
| **Expected Result**                                         | Each role sees only designated modules. Navigation items for other modules absent. URL manipulation redirects with access denied.                                                                                                                                                                                                                       |
| **Negative Test**                                           | System Administrator must not access patient clinical records. Patient must not see other patients' data.                                                                                                                                                                                                                                               |
| **Status**                                                  | Planned                                                                                                                                                                                                                                                                                                                                                 |
|                                                             |                                                                                                                                                                                                                                                                                                                                                         |

|                                                   |                                                                                                              |
|---------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| **TC-AM-003 \| Session Timeout After 15 Minutes** |                                                                                                              |
| **Module**                                        | MOD-09                                                                                                       |
| **FR Reference (CVH-FRD-001 v1.2)**               | FR-AM-03                                                                                                     |
| **Priority**                                      | Must Have                                                                                                    |
| **Preconditions**                                 | User logged in with valid session.                                                                           |
| **Test Steps**                                    | 1\. Login as Receptionist. 2. Simulate 16 minutes of inactivity. 3. Attempt page interaction.                |
| **Expected Result**                               | Login page displayed. Message: 'Your session has expired due to inactivity.' Audit: LOGOUT, outcome=Timeout. |
| **Negative Test**                                 | Active user (interacting within 15 min) must not get logged out mid-session.                                 |
| **Status**                                        | Planned                                                                                                      |
|                                                   |                                                                                                              |

|                                                        |                                                                                                                                                                                                   |
|--------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-004 \| Account Lockout After 3 Failed Logins** |                                                                                                                                                                                                   |
| **Module**                                             | MOD-09                                                                                                                                                                                            |
| **FR Reference (CVH-FRD-001 v1.2)**                    | FR-AM-04, FR-SEC-04                                                                                                                                                                               |
| **Priority**                                           | Must Have                                                                                                                                                                                         |
| **Preconditions**                                      | Active account. failed\_login\_count=0.                                                                                                                                                           |
| **Test Steps**                                         | 1\. Enter wrong password → attempt 1. Verify error. 2. Enter wrong password → attempt 2. Verify error. 3. Enter wrong password → attempt 3. 4. Attempt login with CORRECT password after lockout. |
| **Expected Result**                                    | Attempts 1-2: error; count incremented. Attempt 3: status=Locked; message: 'Account locked. Contact System Administrator.' Attempt 4: still blocked. Audit: LOCK event.                           |
| **Negative Test**                                      | Successful login resets failed\_login\_count=0. Locked account cannot be bypassed by URL manipulation.                                                                                            |
| **Status**                                             | Planned                                                                                                                                                                                           |
|                                                        |                                                                                                                                                                                                   |

|                                                                    |                                                                                                                                                                                    |
|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-005 \| Simulated MFA for Doctor and System Administrator** |                                                                                                                                                                                    |
| **Module**                                                         | MOD-09                                                                                                                                                                             |
| **FR Reference (CVH-FRD-001 v1.2)**                                | FR-AM-05                                                                                                                                                                           |
| **Priority**                                                       | Should Have                                                                                                                                                                        |
| **Preconditions**                                                  | Doctor and System Administrator accounts active.                                                                                                                                   |
| **Test Steps**                                                     | 1\. Login as Doctor with correct credentials. 2. Observe screen after password verification. 3. Proceed through MFA step. 4. Repeat for System Administrator.                      |
| **Expected Result**                                                | MFA simulation screen shown after password for both roles. Label 'MFA simulation — prototype mode only' visible. Access granted after MFA. Receptionist login shows no MFA screen. |
| **Negative Test**                                                  | Patient and Receptionist must not see MFA screen. MFA screen cannot be skipped via URL manipulation.                                                                               |
| **Status**                                                         | Planned                                                                                                                                                                            |
|                                                                    |                                                                                                                                                                                    |

|                                                        |                                                                                                                                                      |
|--------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-006 \| Password Hashing — No Plaintext in DB** |                                                                                                                                                      |
| **Module**                                             | MOD-09                                                                                                                                               |
| **FR Reference (CVH-FRD-001 v1.2)**                    | FR-AM-06 (FRD Section 4.2)                                                                                                                           |
| **Priority**                                           | Must Have                                                                                                                                            |
| **Preconditions**                                      | At least one user account exists.                                                                                                                    |
| **Test Steps**                                         | 1\. Create user with password 'TestPass1!'. 2. Open cvh\_hospital.db directly. 3. Query: SELECT password\_hash FROM users WHERE username='testuser'. |
| **Expected Result**                                    | password\_hash column contains bcrypt hash (starts with $2b$). Password 'TestPass1!' not visible anywhere in DB.                                     |
| **Negative Test**                                      | Hash changes on password reset (new salt). No password logging in audit\_log or console.                                                             |
| **Status**                                             | Planned                                                                                                                                              |
|                                                        |                                                                                                                                                      |

|                                                  |                                                                                                                                                      |
|--------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-007 \| Password Complexity Enforcement** |                                                                                                                                                      |
| **Module**                                       | MOD-09                                                                                                                                               |
| **FR Reference (CVH-FRD-001 v1.2)**              | FR-AM-07 (FRD Section 4.2), FR-SEC-02                                                                                                                |
| **Priority**                                     | Must Have                                                                                                                                            |
| **Preconditions**                                | System Administrator creating new user account.                                                                                                      |
| **Test Steps**                                   | 1\. Attempt password 'password' (no uppercase, numeral, special). 2. Attempt 'Password1' (no special). 3. Attempt 'Password1!' (meets all criteria). |
| **Expected Result**                              | Attempts 1 & 2: rejected with specific error identifying failed criterion. Attempt 3: accepted. Account created.                                     |
| **Negative Test**                                | 7-character password rejected (minimum is 8). Applies equally to self-registration flow.                                                             |
| **Status**                                       | Planned                                                                                                                                              |
|                                                  |                                                                                                                                                      |

|                                                 |                                                                                                                 |
|-------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|
| **TC-AM-008 \| Password Expiry — Forced Reset** |                                                                                                                 |
| **Module**                                      | MOD-09                                                                                                          |
| **FR Reference (CVH-FRD-001 v1.2)**             | FR-AM-08 (FRD Section 4.2), FR-SEC-03                                                                           |
| **Priority**                                    | Should Have                                                                                                     |
| **Preconditions**                               | Account with password\_expiry\_date set to yesterday.                                                           |
| **Test Steps**                                  | 1\. Login with correct credentials. 2. Observe system behaviour after password check.                           |
| **Expected Result**                             | System detects expiry. Redirects to reset screen before any module access. Access blocked until reset complete. |
| **Negative Test**                               | New password must meet complexity rules. Reset updates expiry to today + 90 days.                               |
| **Status**                                      | Planned                                                                                                         |
|                                                 |                                                                                                                 |

|                                                       |                                                                                                                                                                                             |
|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-AM-009 \| Force Password Reset Flag — FR-AM-09** |                                                                                                                                                                                             |
| **Module**                                            | MOD-09                                                                                                                                                                                      |
| **FR Reference (CVH-FRD-001 v1.2)**                   | FR-AM-09 (FRD Section 4.2)                                                                                                                                                                  |
| **Priority**                                          | Must Have                                                                                                                                                                                   |
| **Preconditions**                                     | System Administrator has set force\_password\_reset=1 for a user account.                                                                                                                   |
| **Test Steps**                                        | 1\. Login as the affected user with correct credentials. 2. Observe system behaviour immediately after password verification.                                                               |
| **Expected Result**                                   | Password reset screen displayed before any module access granted. User cannot navigate to any module until reset is complete. After reset: force\_password\_reset=0; normal access granted. |
| **Negative Test**                                     | Verify force\_password\_reset flag cleared only after successful password change — not on login attempt alone. Verify new password must meet complexity rules (BR-SEC-02).                  |
| **Status**                                            | Planned                                                                                                                                                                                     |
|                                                       |                                                                                                                                                                                             |

## 7. IT Administration — TC-IT-001 to TC-IT-004
|                                         |                                                                                                                                                                                                                                                    |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-IT-001 \| User Account Lifecycle** |                                                                                                                                                                                                                                                    |
| **Module**                              | MOD-06                                                                                                                                                                                                                                             |
| **FR Reference (CVH-FRD-001 v1.2)**     | FR-IT-01                                                                                                                                                                                                                                           |
| **Priority**                            | Must Have                                                                                                                                                                                                                                          |
| **Preconditions**                       | System Administrator logged in.                                                                                                                                                                                                                    |
| **Test Steps**                          | 1\. Create user: username='drtest', role='Doctor'. 2. Login as drtest → verify access. 3. Change drtest role to Receptionist. 4. Login as drtest → Doctor modules inaccessible. 5. Deactivate drtest → login blocked. 6. Reactivate → login works. |
| **Expected Result**                     | Each step succeeds. Role change effective on next login. Deactivated account blocked. Reactivated works. All actions in audit\_log.                                                                                                                |
| **Negative Test**                       | System Administrator cannot deactivate own account. Historical records retained after deactivation.                                                                                                                                                |
| **Status**                              | Planned                                                                                                                                                                                                                                            |
|                                         |                                                                                                                                                                                                                                                    |

|                                                       |                                                                                                                                                       |
|-------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-IT-002 \| Audit Log Completeness and Read-Only** |                                                                                                                                                       |
| **Module**                                            | MOD-10                                                                                                                                                |
| **FR Reference (CVH-FRD-001 v1.2)**                   | FR-AUD-01, FR-AUD-02, FR-IT-02                                                                                                                        |
| **Priority**                                          | Must Have                                                                                                                                             |
| **Preconditions**                                     | System Administrator logged in. Multiple prior actions performed.                                                                                     |
| **Test Steps**                                        | 1\. Navigate to Audit Log Viewer. 2. Filter by Action Type=LOGIN. 3. Filter by today's date. 4. Attempt to edit/delete audit entry. 5. Export to CSV. |
| **Expected Result**                                   | Filters return correct results. No edit/delete controls present. CSV exports correctly. All prior actions visible.                                    |
| **Negative Test**                                     | Audit log captures FAILED login attempts. DUPLICATE\_OVERRIDE appears after registration override.                                                    |
| **Status**                                            | Planned                                                                                                                                               |
|                                                       |                                                                                                                                                       |

|                                          |                                                                                                                                                |
|------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-IT-003 \| System Health Dashboard** |                                                                                                                                                |
| **Module**                               | MOD-06                                                                                                                                         |
| **FR Reference (CVH-FRD-001 v1.2)**      | FR-IT-03                                                                                                                                       |
| **Priority**                             | Should Have                                                                                                                                    |
| **Preconditions**                        | System Administrator logged in. Active sessions and appointments today exist.                                                                  |
| **Test Steps**                           | 1\. Navigate to System Health panel. 2. Verify all 5 indicators: active sessions, user counts, today's appointments, recent errors, DB counts. |
| **Expected Result**                      | All 5 indicators populated. Values match actual DB counts verified by direct query.                                                            |
| **Negative Test**                        | Page refreshes indicators on each load. Counts match exact table row counts.                                                                   |
| **Status**                               | Planned                                                                                                                                        |
|                                          |                                                                                                                                                |

|                                                       |                                                                                                                                 |
|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| **TC-IT-004 \| Holiday Configuration Blocks Booking** |                                                                                                                                 |
| **Module**                                            | MOD-06                                                                                                                          |
| **FR Reference (CVH-FRD-001 v1.2)**                   | FR-IT-04                                                                                                                        |
| **Priority**                                          | Should Have                                                                                                                     |
| **Preconditions**                                     | System Administrator logged in. Receptionist account active.                                                                    |
| **Test Steps**                                        | 1\. System Administrator: Add tomorrow as hospital holiday. 2. Login as Receptionist. Attempt to book appointment for tomorrow. |
| **Expected Result**                                   | Tomorrow unavailable in date picker. Error: 'This date is unavailable.' Existing appointments on that date not auto-cancelled.  |
| **Negative Test**                                     | Removing holiday from config restores bookability. Holiday applies to all doctors.                                              |
| **Status**                                            | Planned                                                                                                                         |
|                                                       |                                                                                                                                 |

## 8. Security — TC-SEC-001 to TC-SEC-011
|                                               |                                                                                                                                   |
|-----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-001 \| Consent Captured and Stored** |                                                                                                                                   |
| **Module**                                    | MOD-01                                                                                                                            |
| **FR Reference (CVH-FRD-001 v1.2)**           | FR-PR-03, FR-PAT-04, FR-SEC-08                                                                                                    |
| **Priority**                                  | Must Have                                                                                                                         |
| **Preconditions**                             | Receptionist logged in.                                                                                                           |
| **Test Steps**                                | 1\. Register patient with consent checked. Verify consent recorded. 2. Register another patient without consent → attempt submit. |
| **Expected Result**                           | Patient 1: consent=Yes with timestamp recorded. Patient 2: submission blocked; no record created.                                 |
| **Negative Test**                             | Consent cannot be backdated or modified to No by non-admin roles.                                                                 |
| **Status**                                    | Planned                                                                                                                           |
|                                               |                                                                                                                                   |

|                                                    |                                                                                                                        |
|----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-002 \| Data Accuracy — Field Validation** |                                                                                                                        |
| **Module**                                         | MOD-01                                                                                                                 |
| **FR Reference (CVH-FRD-001 v1.2)**                | FR-PR-02, FR-PAT-06                                                                                                    |
| **Priority**                                       | Must Have                                                                                                              |
| **Preconditions**                                  | Receptionist logged in.                                                                                                |
| **Test Steps**                                     | 1\. Enter DOB as future date. 2. Enter mobile as 9 digits. 3. Enter mobile with letters. 4. Enter pincode as 5 digits. |
| **Expected Result**                                | All 4 rejected with specific field-level error messages. No invalid data written to DB.                                |
| **Negative Test**                                  | Error messages must not expose DB structure or field names.                                                            |
| **Status**                                         | Planned                                                                                                                |
|                                                    |                                                                                                                        |

|                                                 |                                                                                              |
|-------------------------------------------------|----------------------------------------------------------------------------------------------|
| **TC-SEC-003 \| Password Hashing Verification** |                                                                                              |
| **Module**                                      | MOD-09                                                                                       |
| **FR Reference (CVH-FRD-001 v1.2)**             | FR-SEC-01, FR-AM-06                                                                          |
| **Priority**                                    | Must Have                                                                                    |
| **Preconditions**                               | User account exists.                                                                         |
| **Test Steps**                                  | 1\. Create user with password 'TestPass1!'. 2. Inspect DB: SELECT password\_hash FROM users. |
| **Expected Result**                             | Hash string starts with $2b$. Original password not visible anywhere.                        |
| **Negative Test**                               | Hash changes on password reset. No password in audit\_log or console.                        |
| **Status**                                      | Planned                                                                                      |
|                                                 |                                                                                              |

|                                                  |                                                                                                                                                                                                    |
|--------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-004 \| Audit Log Captures All Actions** |                                                                                                                                                                                                    |
| **Module**                                       | MOD-10                                                                                                                                                                                             |
| **FR Reference (CVH-FRD-001 v1.2)**              | FR-SEC-04 via FR-AUD-01                                                                                                                                                                            |
| **Priority**                                     | Must Have                                                                                                                                                                                          |
| **Preconditions**                                | Perform a series of test actions as different roles.                                                                                                                                               |
| **Test Steps**                                   | 1\. Login as Receptionist (LOGIN event). 2. Register patient (CREATE event). 3. Update mobile (UPDATE event). 4. Enter wrong password (Failed LOGIN event). 5. Check audit\_log for all 4 entries. |
| **Expected Result**                              | All 4 events in audit\_log with correct action\_type, module, user\_id, outcome, timestamp.                                                                                                        |
| **Negative Test**                                | Audit\_log cannot be filtered to hide Failed events.                                                                                                                                               |
| **Status**                                       | Planned                                                                                                                                                                                            |
|                                                  |                                                                                                                                                                                                    |

|                                                          |                                                                                                                                                                                                                               |
|----------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-005 \| RBAC — Minimum Necessary Access to PHI** |                                                                                                                                                                                                                               |
| **Module**                                               | MOD-09                                                                                                                                                                                                                        |
| **FR Reference (CVH-FRD-001 v1.2)**                      | FR-AM-02, FR-SEC-05                                                                                                                                                                                                           |
| **Priority**                                             | Must Have                                                                                                                                                                                                                     |
| **Preconditions**                                        | Patient record with clinical notes and prescription exists.                                                                                                                                                                   |
| **Test Steps**                                           | 1\. Login as Receptionist → verify clinical notes NOT accessible. 2. Login as Patient → only Diagnosis and Treatment Plan summary visible; full notes absent. 3. Login as System Administrator → no clinical data accessible. |
| **Expected Result**                                      | Each role limited to designated data. Clinical notes visible to Doctor only.                                                                                                                                                  |
| **Negative Test**                                        | URL manipulation as Receptionist to consultation endpoint → access denied; audit records Failed READ.                                                                                                                         |
| **Status**                                               | Planned                                                                                                                                                                                                                       |
|                                                          |                                                                                                                                                                                                                               |

|                                                            |                                                                                                                              |
|------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-006 \| Consultation Record Integrity After Lock** |                                                                                                                              |
| **Module**                                                 | MOD-03                                                                                                                       |
| **FR Reference (CVH-FRD-001 v1.2)**                        | FR-CLN-05, FR-SEC-06                                                                                                         |
| **Priority**                                               | Must Have                                                                                                                    |
| **Preconditions**                                          | Consultation with is\_editable=0.                                                                                            |
| **Test Steps**                                             | 1\. Login as Doctor. Open locked consultation. 2. Attempt edit via UI. 3. Attempt direct POST to edit endpoint.              |
| **Expected Result**                                        | UI: fields read-only; save controls absent. Direct POST: rejected by business logic. No data modified. Audit: Failed UPDATE. |
| **Negative Test**                                          | is\_editable=0 enforced in business logic layer — not just UI rendering.                                                     |
| **Status**                                                 | Planned                                                                                                                      |
|                                                            |                                                                                                                              |

|                                                                    |                                                                                                                                                                 |
|--------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-007 \| Data Protection by Design — RBAC in Architecture** |                                                                                                                                                                 |
| **Module**                                                         | MOD-09                                                                                                                                                          |
| **FR Reference (CVH-FRD-001 v1.2)**                                | FR-AM-02, FR-SEC-07                                                                                                                                             |
| **Priority**                                                       | Must Have                                                                                                                                                       |
| **Preconditions**                                                  | All roles active. Application running.                                                                                                                          |
| **Test Steps**                                                     | 1\. Verify RBAC at router level on every page load. 2. System Administrator changes Doctor role to Receptionist mid-session. 3. Doctor session attempts MOD-03. |
| **Expected Result**                                                | Role change effective on next page load. Original session denied after role change.                                                                             |
| **Negative Test**                                                  | No cached role state persists beyond session invalidation.                                                                                                      |
| **Status**                                                         | Planned                                                                                                                                                         |
|                                                                    |                                                                                                                                                                 |

|                                                   |                                                                                                                                  |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-008 \| Consent Withdrawal Notification** |                                                                                                                                  |
| **Module**                                        | MOD-07                                                                                                                           |
| **FR Reference (CVH-FRD-001 v1.2)**               | FR-PAT-04, FR-SEC-08                                                                                                             |
| **Priority**                                      | Should Have                                                                                                                      |
| **Preconditions**                                 | Patient logged in. System Administrator active.                                                                                  |
| **Test Steps**                                    | 1\. Patient submits consent withdrawal request via MOD-07.                                                                       |
| **Expected Result**                               | Withdrawal flag set. System Administrator alerted in MOD-06 dashboard. Audit: UPDATE with detail='Consent withdrawal requested'. |
| **Negative Test**                                 | Patient cannot unilaterally delete own record — only flag for review.                                                            |
| **Status**                                        | Planned                                                                                                                          |
|                                                   |                                                                                                                                  |

|                                                                |                                                                                                                                  |
|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-009 \| Error Messages — No System Internals Exposed** |                                                                                                                                  |
| **Module**                                                     | All Modules                                                                                                                      |
| **FR Reference (CVH-FRD-001 v1.2)**                            | FR-SEC-10, T-NFR-05                                                                                                              |
| **Priority**                                                   | Must Have                                                                                                                        |
| **Preconditions**                                              | Application running.                                                                                                             |
| **Test Steps**                                                 | 1\. Simulate DB error (rename DB file temporarily). 2. Attempt login. 3. Attempt patient registration. 4. Restore DB file.       |
| **Expected Result**                                            | Generic messages shown: 'Service temporarily unavailable. Please try again.' No stack traces, SQL errors, or file paths visible. |
| **Negative Test**                                              | Browser developer tools show no sensitive details in network responses.                                                          |
| **Status**                                                     | Planned                                                                                                                          |
|                                                                |                                                                                                                                  |

|                                         |                                                                                                                     |
|-----------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-010 \| Single Active Session** |                                                                                                                     |
| **Module**                              | MOD-09                                                                                                              |
| **FR Reference (CVH-FRD-001 v1.2)**     | FR-SEC-06                                                                                                           |
| **Priority**                            | Should Have                                                                                                         |
| **Preconditions**                       | User account active. Two browsers available.                                                                        |
| **Test Steps**                          | 1\. Login as Receptionist in Browser A. 2. Login as same Receptionist in Browser B. 3. Attempt action in Browser A. |
| **Expected Result**                     | Browser A session invalidated on next interaction. Re-login required. Audit: two LOGIN events.                      |
| **Negative Test**                       | Both sessions must not be simultaneously active.                                                                    |
| **Status**                              | Planned                                                                                                             |
|                                         |                                                                                                                     |

|                                                        |                                                                                                                                                                                                                                      |
|--------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-SEC-011 \| SQL Injection Prevention — FR-SEC-09** |                                                                                                                                                                                                                                      |
| **Module**                                             | MOD-09 (all input fields)                                                                                                                                                                                                            |
| **FR Reference (CVH-FRD-001 v1.2)**                    | FR-SEC-09 (FRD Section 15)                                                                                                                                                                                                           |
| **Priority**                                           | Must Have                                                                                                                                                                                                                            |
| **Preconditions**                                      | Application running. Login page and patient search fields accessible.                                                                                                                                                                |
| **Test Steps**                                         | 1\. Enter username: admin'-- in login field. 2. Enter: ' OR '1'='1 in login field and submit. 3. Enter SQL injection strings in patient search: name field and mobile field. 4. Verify system response for each attempt.             |
| **Expected Result**                                    | All injection attempts rejected. No DB error message exposed to UI. Login fails with generic credential error. Patient search returns no results or ignores injected syntax. No stack traces or SQL details visible in any response. |
| **Negative Test**                                      | Verify application logs unusual input patterns internally. Verify generic user-facing messages shown in all cases — no SQL syntax, table names, or column names exposed to user.                                                     |
| **Status**                                             | Planned                                                                                                                                                                                                                              |
|                                                        |                                                                                                                                                                                                                                      |

## 9. User Experience — TC-UX-001 to TC-UX-003
*UX requirements are covered by NFR-05, NFR-06, NFR-07, and T-NFR-02 in CVH-BRD-001 v1.3 and CVH-FRD-001 v1.2. No dedicated FR-UX IDs exist — reference NFRs.*

|                                           |                                                                                                                             |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **TC-UX-001 \| Role-Specific Navigation** |                                                                                                                             |
| **Module**                                | All Modules                                                                                                                 |
| **FR Reference (CVH-FRD-001 v1.2)**       | FR-AM-02 (NFR-05)                                                                                                           |
| **Priority**                              | Should Have                                                                                                                 |
| **Preconditions**                         | One account per role active.                                                                                                |
| **Test Steps**                            | 1\. Login as each role in sequence. 2. Verify navigation menu items present and absent per access matrix (FRD Section 2.3). |
| **Expected Result**                       | Each role sees exactly their designated modules. No extra modules visible.                                                  |
| **Negative Test**                         | No hidden navigation items accessible via keyboard shortcuts or developer tools.                                            |
| **Status**                                | Planned                                                                                                                     |
|                                           |                                                                                                                             |

|                                                      |                                                                                                                         |
|------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **TC-UX-002 \| Form Validation — Actionable Errors** |                                                                                                                         |
| **Module**                                           | MOD-01, MOD-02                                                                                                          |
| **FR Reference (CVH-FRD-001 v1.2)**                  | FR-PR-02 to 05 (NFR-06)                                                                                                 |
| **Priority**                                         | Should Have                                                                                                             |
| **Preconditions**                                    | Receptionist logged in.                                                                                                 |
| **Test Steps**                                       | 1\. Submit registration form with 5 invalid fields simultaneously. 2. Submit appointment form with no patient selected. |
| **Expected Result**                                  | All 5 invalid fields highlighted simultaneously with individual error messages identifying field and required format.   |
| **Negative Test**                                    | Generic 'form error' message is not acceptable. Each field must have its own specific error.                            |
| **Status**                                           | Planned                                                                                                                 |
|                                                      |                                                                                                                         |

|                                              |                                                                                                |
|----------------------------------------------|------------------------------------------------------------------------------------------------|
| **TC-UX-003 \| Cross-Browser Compatibility** |                                                                                                |
| **Module**                                   | All Modules                                                                                    |
| **FR Reference (CVH-FRD-001 v1.2)**          | T-NFR-02                                                                                       |
| **Priority**                                 | Should Have                                                                                    |
| **Preconditions**                            | Application running locally. Chrome, Firefox, Edge available.                                  |
| **Test Steps**                               | 1\. Run TC-PR-001 in Chrome. 2. Run TC-PR-001 in Firefox. 3. Run TC-PR-001 in Edge.            |
| **Expected Result**                          | Registration completes in all 3 browsers. UI rendering consistent. No browser-specific errors. |
| **Negative Test**                            | No browser console errors during normal operation.                                             |
| **Status**                                   | Planned                                                                                        |
|                                              |                                                                                                |

## 10. Reporting — TC-RPT-001 to TC-RPT-007
|                                             |                                                                                                                |
|---------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| **TC-RPT-001 \| Daily Appointment Summary** |                                                                                                                |
| **Module**                                  | MOD-08                                                                                                         |
| **FR Reference (CVH-FRD-001 v1.2)**         | FR-RPT-01, FR-RPT-02                                                                                           |
| **Priority**                                | Should Have                                                                                                    |
| **Preconditions**                           | Dean/Admin logged in. 5+ appointments today with mixed statuses.                                               |
| **Test Steps**                              | 1\. Select Daily Appointment Summary. Set date=today. 2. Apply doctor filter. 3. Verify counts. 4. Export CSV. |
| **Expected Result**                         | Correct counts by status. Doctor filter works. Chart renders. CSV exports correctly.                           |
| **Negative Test**                           | Empty date range shows empty report — not an error.                                                            |
| **Status**                                  | Planned                                                                                                        |
|                                             |                                                                                                                |

|                                      |                                                                                                      |
|--------------------------------------|------------------------------------------------------------------------------------------------------|
| **TC-RPT-002 \| Doctor Utilisation** |                                                                                                      |
| **Module**                           | MOD-08                                                                                               |
| **FR Reference (CVH-FRD-001 v1.2)**  | FR-RPT-03                                                                                            |
| **Priority**                         | Should Have                                                                                          |
| **Preconditions**                    | Multiple doctors with varying appointment loads.                                                     |
| **Test Steps**                       | 1\. Run Doctor Utilisation report for this week.                                                     |
| **Expected Result**                  | Appointments per doctor vs available slots shown. Utilisation % calculated correctly. Chart renders. |
| **Negative Test**                    | Doctor with 0 appointments shows 0% — not missing from report.                                       |
| **Status**                           | Planned                                                                                              |
|                                      |                                                                                                      |

|                                                |                                                                                                            |
|------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| **TC-RPT-003 \| Patient Registration Summary** |                                                                                                            |
| **Module**                                     | MOD-08                                                                                                     |
| **FR Reference (CVH-FRD-001 v1.2)**            | FR-RPT-03                                                                                                  |
| **Priority**                                   | Should Have                                                                                                |
| **Preconditions**                              | Patients registered in last 7 days.                                                                        |
| **Test Steps**                                 | 1\. Run Patient Registration Summary for last 7 days.                                                      |
| **Expected Result**                            | New registration count matches DB: SELECT COUNT(\*) WHERE registration\_date &gt;= today-7. Chart renders. |
| **Negative Test**                              | Deactivated patients excluded from active count.                                                           |
| **Status**                                     | Planned                                                                                                    |
|                                                |                                                                                                            |

|                                                   |                                                                           |
|---------------------------------------------------|---------------------------------------------------------------------------|
| **TC-RPT-004 \| No-Show and Cancellation Report** |                                                                           |
| **Module**                                        | MOD-08                                                                    |
| **FR Reference (CVH-FRD-001 v1.2)**               | FR-RPT-04                                                                 |
| **Priority**                                      | Should Have                                                               |
| **Preconditions**                                 | 2+ No-Show and 2+ Cancelled appointments exist.                           |
| **Test Steps**                                    | 1\. Run No-Show and Cancellation report for current month.                |
| **Expected Result**                               | Counts match DB. Late Cancellation flag visible. Chart renders correctly. |
| **Negative Test**                                 | Completed appointments excluded from this report.                         |
| **Status**                                        | Planned                                                                   |
|                                                   |                                                                           |

|                                                          |                                                                                                                                                |
|----------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-RPT-005 \| Audit Activity Report — Access Control** |                                                                                                                                                |
| **Module**                                               | MOD-08                                                                                                                                         |
| **FR Reference (CVH-FRD-001 v1.2)**                      | FR-RPT-05                                                                                                                                      |
| **Priority**                                             | Should Have                                                                                                                                    |
| **Preconditions**                                        | System Administrator and Dean/Admin accounts active.                                                                                           |
| **Test Steps**                                           | 1\. Login as System Administrator → run Audit Activity Report. 2. Login as Dean-Admin → run report. 3. Login as Receptionist → attempt access. |
| **Expected Result**                                      | System Administrator: full access. Dean-Admin: compliance view. Receptionist: not accessible; redirect to home.                                |
| **Negative Test**                                        | Report must not expose password hashes or session tokens even in raw export.                                                                   |
| **Status**                                               | Planned                                                                                                                                        |
|                                                          |                                                                                                                                                |

|                                             |                                                                                                       |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **TC-RPT-006 \| Compliance Status Summary** |                                                                                                       |
| **Module**                                  | MOD-08                                                                                                |
| **FR Reference (CVH-FRD-001 v1.2)**         | FR-RPT-05                                                                                             |
| **Priority**                                | Should Have                                                                                           |
| **Preconditions**                           | Dean/Admin logged in.                                                                                 |
| **Test Steps**                              | 1\. Run Compliance Status Summary report.                                                             |
| **Expected Result**                         | Consent coverage %, access deviations, audit completeness shown. Values traceable to underlying data. |
| **Negative Test**                           | Report runs without error when no compliance flags exist — shows clean status clearly.                |
| **Status**                                  | Planned                                                                                               |
|                                             |                                                                                                       |

|                                                |                                                                                                |
|------------------------------------------------|------------------------------------------------------------------------------------------------|
| **TC-RPT-007 \| Patient Demographics Summary** |                                                                                                |
| **Module**                                     | MOD-08                                                                                         |
| **FR Reference (CVH-FRD-001 v1.2)**            | FR-RPT-06                                                                                      |
| **Priority**                                   | Could Have                                                                                     |
| **Preconditions**                              | 10+ patients registered with varied demographics.                                              |
| **Test Steps**                                 | 1\. Run Patient Demographics Summary.                                                          |
| **Expected Result**                            | Age group and gender distribution shown as charts. Counts match DB aggregation. CSV available. |
| **Negative Test**                              | Deactivated patients excluded. 'Prefer not to say' gender handled correctly in charts.         |
| **Status**                                     | Planned                                                                                        |
|                                                |                                                                                                |

## 11. Patient Self-Registration — TC-PAT-SR-001 to TC-PAT-SR-004 (CVH-CR-001)
|                                                                 |                                                                                                                            |
|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **TC-PAT-SR-001 \| Self-Registration Page Publicly Accessible** |                                                                                                                            |
| **Module**                                                      | MOD-07                                                                                                                     |
| **FR Reference (CVH-FRD-001 v1.2)**                             | FR-PAT-05                                                                                                                  |
| **Priority**                                                    | Must Have                                                                                                                  |
| **Preconditions**                                               | Application running. No active session.                                                                                    |
| **Test Steps**                                                  | 1\. Navigate to application URL without logging in. 2. Verify Register link visible on login page. 3. Click Register link. |
| **Expected Result**                                             | Register link visible without authentication. Self-registration form displayed. No module content exposed on same screen.  |
| **Negative Test**                                               | Direct URL to any module without session → redirect to login. Register link does not bypass RBAC.                          |
| **Status**                                                      | Planned                                                                                                                    |
|                                                                 |                                                                                                                            |

|                                                            |                                                                                                                                            |
|------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PAT-SR-002 \| Self-Registration Duplicate Detection** |                                                                                                                                            |
| **Module**                                                 | MOD-07                                                                                                                                     |
| **FR Reference (CVH-FRD-001 v1.2)**                        | FR-PAT-06                                                                                                                                  |
| **Priority**                                               | Must Have                                                                                                                                  |
| **Preconditions**                                          | Patient 'Raj Shah, DOB 01/01/1990, Mobile 9876543210' already exists in patients table.                                                    |
| **Test Steps**                                             | 1\. Complete self-registration form with same Full Name + DOB + Mobile as existing patient. 2. Submit.                                     |
| **Expected Result**                                        | Warning displayed: 'A record may already exist. Please contact Reception.' No new patient record created. No new user account created.     |
| **Negative Test**                                          | Same mobile but different name must NOT trigger duplicate — combination logic applies. No partial records inserted on duplicate detection. |
| **Status**                                                 | Planned                                                                                                                                    |
|                                                            |                                                                                                                                            |

|                                                                |                                                                                                                                                                                                                                |
|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PAT-SR-003 \| Successful Self-Registration — Auto-Login** |                                                                                                                                                                                                                                |
| **Module**                                                     | MOD-07                                                                                                                                                                                                                         |
| **FR Reference (CVH-FRD-001 v1.2)**                            | FR-PAT-07                                                                                                                                                                                                                      |
| **Priority**                                                   | Must Have                                                                                                                                                                                                                      |
| **Preconditions**                                              | No existing record for the test patient. Application running.                                                                                                                                                                  |
| **Test Steps**                                                 | 1\. Navigate to Register link. 2. Complete form: Name='New Test', DOB='15/06/1995', Gender='Female', Mobile='8765432109', Password='NewTest1!'. 3. Check consent. Submit.                                                      |
| **Expected Result**                                            | Patient ID auto-generated (CVH-YYYY-NNNNN). Portal account created (username=8765432109, role=Patient). Patient auto-logged in. MOD-07 Patient Portal rendered. Audit: CREATE events for both patient record and user account. |
| **Negative Test**                                              | Registration with existing mobile as username → specific error 'Account already exists for this mobile number.' No duplicate user account created.                                                                             |
| **Status**                                                     | Planned                                                                                                                                                                                                                        |
|                                                                |                                                                                                                                                                                                                                |

|                                                               |                                                                                                                                                                                                                                             |
|---------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **TC-PAT-SR-004 \| Password Complexity at Self-Registration** |                                                                                                                                                                                                                                             |
| **Module**                                                    | MOD-07                                                                                                                                                                                                                                      |
| **FR Reference (CVH-FRD-001 v1.2)**                           | FR-PAT-08, FR-SEC-02                                                                                                                                                                                                                        |
| **Priority**                                                  | Must Have                                                                                                                                                                                                                                   |
| **Preconditions**                                             | Self-registration form open. No existing account for test mobile.                                                                                                                                                                           |
| **Test Steps**                                                | 1\. Enter password 'simple' (too short, no uppercase, no numeral, no special). 2. Enter password 'Password1' (no special character). 3. Enter password 'Pass1!' (too short — 6 chars). 4. Enter password 'Password1!' (meets all criteria). |
| **Expected Result**                                           | Attempts 1-3: each rejected with specific error identifying the violated rule. Attempt 4: password accepted; registration proceeds.                                                                                                         |
| **Negative Test**                                             | Complexity error messages identify specific failed criterion — not a generic error. Applies at self-registration, admin creation, and password reset.                                                                                       |
| **Status**                                                    | Planned                                                                                                                                                                                                                                     |
|                                                               |                                                                                                                                                                                                                                             |

## 12. Sign-Off & Test Execution Plan
|           |                                                                 |                           |            |            |
|-----------|-----------------------------------------------------------------|---------------------------|------------|------------|
| **Phase** | **Activity**                                                    | **Owner**                 | **Target** | **Status** |
| Phase 1   | System Test Cases v1.1 authored (this document)                 | Prashant Gore             | July 2026  | Complete   |
| Phase 2   | Test environment setup with synthetic data                      | Developer / BA            | TBD        | Planned    |
| Phase 3   | STC execution against prototype build                           | Prashant Gore / Developer | TBD        | Planned    |
| Phase 4   | Defects logged; retested; RTM updated                           | Prashant Gore             | TBD        | Planned    |
| Phase 5   | UAT Scripts (CVH-UAT-001 v1.1) executed by role representatives | BA + Stakeholders         | TBD        | Planned    |
| Phase 6   | Test Execution Summary (CVH-TER-001) produced                   | Prashant Gore             | TBD        | Planned    |

**END OF DOCUMENT**


</div>