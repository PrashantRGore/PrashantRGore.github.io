---
hide:
  - toc
---

<div class="ba-meta-bar">
<span class="ba-badge ba-badge--id">CVH-UAT-001</span>
<span class="ba-badge ba-badge--version">Version 1.1</span>
<span class="ba-badge ba-badge--status">Baselined</span>
<span class="ba-badge ba-badge--compliance">DPDP / HIPAA / GDPR</span>
</div>

# User Acceptance Testing Scripts (UAT)

|                  |                                                                                   |
|------------------|-----------------------------------------------------------------------------------|
| Document ID      | CVH-UAT-001                                                                       |
| Version          | 1.1 – CVH-CR-001 Amendment                                                        |
| Date             | July 2026                                                                         |
| Prepared By      | Prashant Gore – BA & Digital Transformation Consultant                            |
| Parent Documents | CVH-BRD-001 v1.3 \| CVH-FRD-001 v1.2 \| CVH-RTM-001 v1.1 \| CVH-STC-001 v1.1      |
| UAT Approach     | Business-language scenarios executed by role representatives — no technical steps |
| Total Scenarios  | 43 (39 original + 4 from CVH-CR-001)                                              |
| Status           | DRAFT – Awaiting Execution                                                        |

> *DISCLAIMER: Prototype demonstration project only. No real patient data. Not for production clinical deployment.*

## 1. Document Control & UAT Approach
|             |           |               |                                                                                                                                                                                           |            |
|-------------|-----------|---------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| **Version** | **Date**  | **Author**    | **Description**                                                                                                                                                                           | **Status** |
| 1.0         | June 2026 | Prashant Gore | Initial UAT Scripts — 39 business acceptance scenarios                                                                                                                                    | Superseded |
| 1.1         | July 2026 | Prashant Gore | CVH-CR-001: UAT-PAT-SR-001 to 004 added; FR references corrected (UAT-RPT-004, UAT-SEC-001, UAT-UX); Section 5 header corrected; coverage table corrected; Business Comments column added | Draft      |

**1.1 UAT vs STC Boundary**

|               |                                           |                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------|
| **Aspect**    | **System Test Cases (CVH-STC-001 v1.1)**  | **UAT Scripts (CVH-UAT-001 v1.1)**                    |
| Purpose       | Verify system works correctly (technical) | Verify business needs are met (acceptance)            |
| Executed By   | BA / Developer / QA                       | Role representatives (Receptionist, Doctor, etc.)     |
| Language      | Technical steps, DB checks, FR references | Plain business language — no technical detail         |
| Format        | Steps + Expected Result + Negative Test   | Given / When / Then + Acceptance Criterion            |
| Pass Criteria | Functional correctness                    | Business acceptance by role representative            |
| Out of Scope  | —                                         | Performance, load, penetration testing, DB validation |

**1.2 UAT Execution Instructions**

Each scenario is executed by a representative of the stated role. The executor reads the Business Scenario, follows the When (User Action), and confirms whether the Then (Acceptance Criterion) is met. Results recorded as Pass or Fail. Business Comments capture observations not constituting defects. Any Fail triggers a Defect ID entry for resolution before sign-off.

**1.3 Sign-Off Criteria**

UAT is passed when: (1) 100% of Must Have scenarios Pass. (2) ≥80% of Should Have scenarios Pass. (3) Zero open Critical defects (data loss, security breach, RBAC failure). (4) Sign-off from at least one representative per role group.

## 2. UAT Coverage Summary
|                                    |               |                                       |               |                 |
|------------------------------------|---------------|---------------------------------------|---------------|-----------------|
| **Role Group**                     | **Scenarios** | **UAT IDs**                           | **Must Have** | **Should Have** |
| Receptionist                       | 8             | UAT-PR-001 to 005, UAT-APT-001 to 003 | 7             | 1               |
| Doctor                             | 6             | UAT-CLN-001 to 006                    | 5             | 1               |
| Clinician                          | 2             | UAT-CLN-007 to 008                    | 2             | 0               |
| Patient                            | 3             | UAT-PAT-001 to 003                    | 1             | 2               |
| System Administrator               | 8             | UAT-AM-001 to 004, UAT-IT-001 to 004  | 6             | 2               |
| Dean / Admin                       | 5             | UAT-RPT-001 to 005                    | 0             | 5               |
| Cross-Role / Compliance            | 7             | UAT-SEC-001 to 004, UAT-UX-001 to 003 | 4             | 3               |
| Patient Self-Registration (CR-001) | 4             | UAT-PAT-SR-001 to 004                 | 4             | 0               |
| TOTAL                              | 43            | —                                     | 29            | 14              |

*UAT-CLN-001 to 006: Doctor scenarios. UAT-CLN-007 to 008: Clinician scenarios. IDs are sequential and non-overlapping.*

## 3. Receptionist Scenarios — UAT-PR-001 to UAT-APT-003
|                                          |                                                                                                                                                                                 |
|------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PR-001 \| Register a New Patient** |                                                                                                                                                                                 |
| **Role / Actor**                         | Receptionist                                                                                                                                                                    |
| **RTM Reference**                        | O-01 → BR-REQ-PR-01 → FR-PR-01                                                                                                                                                  |
| **STC Reference**                        | TC-PR-001                                                                                                                                                                       |
| **Priority**                             | Must Have                                                                                                                                                                       |
| **Business Scenario**                    | As a Receptionist, I need to register a new patient so they can be booked for an appointment.                                                                                   |
| **Given (Precondition)**                 | I am logged in as Receptionist. A new patient has arrived who is not yet registered.                                                                                            |
| **When (User Action)**                   | I fill in the patient's name, date of birth, mobile number, and other required details. I confirm consent and submit.                                                           |
| **Then (Acceptance Criterion)**          | A unique Patient ID is generated and displayed. I can immediately find the patient by name or ID.                                                                               |
| **Fail Condition**                       | If I leave any required field blank, the system highlights the missing field and does not register the patient. If I do not tick the consent box, the form cannot be submitted. |
| **Actual Result**                        | (To be completed during execution)                                                                                                                                              |
| **Pass / Fail**                          | ☐ Pass ☐ Fail                                                                                                                                                                   |
| **Defect ID**                            | (If failed — log in defect register)                                                                                                                                            |
| **Business Comments**                    | (User observations, suggestions, or feedback during UAT)                                                                                                                        |
| **Executed By / Date**                   | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                                       |
|                                          |                                                                                                                                                                                 |

|                                                  |                                                                                                                                                                                   |
|--------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PR-002 \| Prevent Duplicate Registration** |                                                                                                                                                                                   |
| **Role / Actor**                                 | Receptionist                                                                                                                                                                      |
| **RTM Reference**                                | O-01 → BR-REQ-PR-02 → FR-PR-02                                                                                                                                                    |
| **STC Reference**                                | TC-PR-002                                                                                                                                                                         |
| **Priority**                                     | Must Have                                                                                                                                                                         |
| **Business Scenario**                            | As a Receptionist, I need the system to warn me if a patient may already exist.                                                                                                   |
| **Given (Precondition)**                         | A patient 'Raj Shah', DOB '01-Jan-1990', mobile '9876543210' already exists.                                                                                                      |
| **When (User Action)**                           | I attempt to register a new patient with the same name, date of birth, and mobile number.                                                                                         |
| **Then (Acceptance Criterion)**                  | The system warns me that a matching patient already exists and shows me their Patient ID. I can override or cancel.                                                               |
| **Fail Condition**                               | If I register the same mobile number but a different name, the system does NOT warn me — it creates a new record normally. Mobile alone is not sufficient to trigger a duplicate. |
| **Actual Result**                                | (To be completed during execution)                                                                                                                                                |
| **Pass / Fail**                                  | ☐ Pass ☐ Fail                                                                                                                                                                     |
| **Defect ID**                                    | (If failed — log in defect register)                                                                                                                                              |
| **Business Comments**                            | (User observations, suggestions, or feedback during UAT)                                                                                                                          |
| **Executed By / Date**                           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                                         |
|                                                  |                                                                                                                                                                                   |

|                                                     |                                                                                                                                                  |
|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PR-003 \| Patient Consent Must Be Confirmed** |                                                                                                                                                  |
| **Role / Actor**                                    | Receptionist                                                                                                                                     |
| **RTM Reference**                                   | O-01 → BR-REQ-PR-03 → FR-PR-03                                                                                                                   |
| **STC Reference**                                   | TC-PR-003                                                                                                                                        |
| **Priority**                                        | Must Have                                                                                                                                        |
| **Business Scenario**                               | As a Receptionist, I must ensure every patient gives consent before their record is created.                                                     |
| **Given (Precondition)**                            | I am on the patient registration form with all mandatory fields filled.                                                                          |
| **When (User Action)**                              | I attempt to submit the form without ticking the consent checkbox.                                                                               |
| **Then (Acceptance Criterion)**                     | The system does not allow submission. A clear message tells me consent is required. When I tick consent and resubmit, the patient is registered. |
| **Fail Condition**                                  | A patient record is never created without consent being recorded.                                                                                |
| **Actual Result**                                   | (To be completed during execution)                                                                                                               |
| **Pass / Fail**                                     | ☐ Pass ☐ Fail                                                                                                                                    |
| **Defect ID**                                       | (If failed — log in defect register)                                                                                                             |
| **Business Comments**                               | (User observations, suggestions, or feedback during UAT)                                                                                         |
| **Executed By / Date**                              | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                        |
|                                                     |                                                                                                                                                  |

|                                                    |                                                                                                                         |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **UAT-PR-004 \| Search and Update Patient Record** |                                                                                                                         |
| **Role / Actor**                                   | Receptionist                                                                                                            |
| **RTM Reference**                                  | O-01 → BR-REQ-PR-04 → FR-PR-04                                                                                          |
| **STC Reference**                                  | TC-PR-004                                                                                                               |
| **Priority**                                       | Must Have                                                                                                               |
| **Business Scenario**                              | As a Receptionist, I need to find and update an existing patient's contact details.                                     |
| **Given (Precondition)**                           | Patient 'Raj Shah' (CVH-2026-00001) is registered.                                                                      |
| **When (User Action)**                             | I search for the patient by name, update the mobile number and save.                                                    |
| **Then (Acceptance Criterion)**                    | The patient record is found immediately. The updated mobile number is saved and reflected when I view the record again. |
| **Fail Condition**                                 | If I search for a name that does not exist, the system shows 'No patient found' — not a blank screen.                   |
| **Actual Result**                                  | (To be completed during execution)                                                                                      |
| **Pass / Fail**                                    | ☐ Pass ☐ Fail                                                                                                           |
| **Defect ID**                                      | (If failed — log in defect register)                                                                                    |
| **Business Comments**                              | (User observations, suggestions, or feedback during UAT)                                                                |
| **Executed By / Date**                             | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                               |
|                                                    |                                                                                                                         |

|                                                       |                                                                                                                        |
|-------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| **UAT-PR-005 \| Medical History Available to Doctor** |                                                                                                                        |
| **Role / Actor**                                      | Receptionist                                                                                                           |
| **RTM Reference**                                     | O-01 → BR-REQ-PR-05 → FR-PR-05                                                                                         |
| **STC Reference**                                     | TC-PR-005                                                                                                              |
| **Priority**                                          | Must Have                                                                                                              |
| **Business Scenario**                                 | As a Receptionist, I want to confirm that medical history entered at registration is available to the treating Doctor. |
| **Given (Precondition)**                              | Patient registered with Known Allergies = 'Penicillin'. Appointment In-Progress.                                       |
| **When (User Action)**                                | I confirm with the Doctor that they can see the allergy information before starting the consultation.                  |
| **Then (Acceptance Criterion)**                       | The Doctor confirms they can see 'Penicillin' under Known Allergies in the patient's record during consultation.       |
| **Fail Condition**                                    | If medical history is blank, the Doctor sees a clear 'No history recorded' indicator — not missing fields.             |
| **Actual Result**                                     | (To be completed during execution)                                                                                     |
| **Pass / Fail**                                       | ☐ Pass ☐ Fail                                                                                                          |
| **Defect ID**                                         | (If failed — log in defect register)                                                                                   |
| **Business Comments**                                 | (User observations, suggestions, or feedback during UAT)                                                               |
| **Executed By / Date**                                | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                              |
|                                                       |                                                                                                                        |

|                                        |                                                                                                                                                    |
|----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-APT-001 \| Book an Appointment** |                                                                                                                                                    |
| **Role / Actor**                       | Receptionist                                                                                                                                       |
| **RTM Reference**                      | O-02 → BR-REQ-APT-01 → FR-APT-01                                                                                                                   |
| **STC Reference**                      | TC-APT-001                                                                                                                                         |
| **Priority**                           | Must Have                                                                                                                                          |
| **Business Scenario**                  | As a Receptionist, I need to book an appointment for a registered patient.                                                                         |
| **Given (Precondition)**               | Patient 'Raj Shah' is registered. Dr. Mehta has availability tomorrow.                                                                             |
| **When (User Action)**                 | I search for the patient, select Dr. Mehta, choose tomorrow's date, select 10:00 AM, set Visit Type as New, and confirm.                           |
| **Then (Acceptance Criterion)**        | The appointment is confirmed with a unique Appointment ID. It appears in tomorrow's queue. The 10:00 AM slot is no longer available for Dr. Mehta. |
| **Fail Condition**                     | If I try to book the same slot for Dr. Mehta again, the system tells me the slot is already taken.                                                 |
| **Actual Result**                      | (To be completed during execution)                                                                                                                 |
| **Pass / Fail**                        | ☐ Pass ☐ Fail                                                                                                                                      |
| **Defect ID**                          | (If failed — log in defect register)                                                                                                               |
| **Business Comments**                  | (User observations, suggestions, or feedback during UAT)                                                                                           |
| **Executed By / Date**                 | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                          |
|                                        |                                                                                                                                                    |

|                                       |                                                                                                                     |
|---------------------------------------|---------------------------------------------------------------------------------------------------------------------|
| **UAT-APT-002 \| Check In a Patient** |                                                                                                                     |
| **Role / Actor**                      | Receptionist                                                                                                        |
| **RTM Reference**                     | O-02 → BR-REQ-APT-02 → FR-APT-03                                                                                    |
| **STC Reference**                     | TC-APT-002                                                                                                          |
| **Priority**                          | Must Have                                                                                                           |
| **Business Scenario**                 | As a Receptionist, I need to check in a patient when they arrive.                                                   |
| **Given (Precondition)**              | An appointment for 'Raj Shah' at 10:00 AM today is Scheduled.                                                       |
| **When (User Action)**                | I find the appointment in today's queue and click Check In.                                                         |
| **Then (Acceptance Criterion)**       | The appointment status changes to Checked-In. The patient now appears in the Clinician's list for vitals.           |
| **Fail Condition**                    | If I try to check in more than 30 minutes before the appointment time, the system prevents me with a clear message. |
| **Actual Result**                     | (To be completed during execution)                                                                                  |
| **Pass / Fail**                       | ☐ Pass ☐ Fail                                                                                                       |
| **Defect ID**                         | (If failed — log in defect register)                                                                                |
| **Business Comments**                 | (User observations, suggestions, or feedback during UAT)                                                            |
| **Executed By / Date**                | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                           |
|                                       |                                                                                                                     |

|                                          |                                                                                                             |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **UAT-APT-003 \| Cancel an Appointment** |                                                                                                             |
| **Role / Actor**                         | Receptionist                                                                                                |
| **RTM Reference**                        | O-02 → BR-REQ-APT-04 → FR-APT-05                                                                            |
| **STC Reference**                        | TC-APT-004                                                                                                  |
| **Priority**                             | Must Have                                                                                                   |
| **Business Scenario**                    | As a Receptionist, I need to cancel a patient's appointment and record the reason.                          |
| **Given (Precondition)**                 | An appointment for 'Raj Shah' is Scheduled for today.                                                       |
| **When (User Action)**                   | I select the appointment, choose Cancel, enter the reason 'Patient request', and confirm.                   |
| **Then (Acceptance Criterion)**          | The appointment status changes to Cancelled. The reason is saved. The slot becomes available for rebooking. |
| **Fail Condition**                       | If I try to cancel without entering a reason, the system does not allow it.                                 |
| **Actual Result**                        | (To be completed during execution)                                                                          |
| **Pass / Fail**                          | ☐ Pass ☐ Fail                                                                                               |
| **Defect ID**                            | (If failed — log in defect register)                                                                        |
| **Business Comments**                    | (User observations, suggestions, or feedback during UAT)                                                    |
| **Executed By / Date**                   | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                   |
|                                          |                                                                                                             |

## 4. Doctor Scenarios — UAT-CLN-001 to UAT-CLN-006
|                                          |                                                                                                |
|------------------------------------------|------------------------------------------------------------------------------------------------|
| **UAT-CLN-001 \| View Today's Schedule** |                                                                                                |
| **Role / Actor**                         | Doctor                                                                                         |
| **RTM Reference**                        | O-03 → BR-REQ-CLN-01 → FR-CLN-01                                                               |
| **STC Reference**                        | TC-CLN-001                                                                                     |
| **Priority**                             | Must Have                                                                                      |
| **Business Scenario**                    | As a Doctor, I want to see all my appointments for today when I log in.                        |
| **Given (Precondition)**                 | I have 3 appointments scheduled today.                                                         |
| **When (User Action)**                   | I log in as Doctor and view my home screen.                                                    |
| **Then (Acceptance Criterion)**          | I can see all 3 appointments listed in time order with patient names, visit types, and status. |
| **Fail Condition**                       | Appointments from other doctors are not visible in my schedule.                                |
| **Actual Result**                        | (To be completed during execution)                                                             |
| **Pass / Fail**                          | ☐ Pass ☐ Fail                                                                                  |
| **Defect ID**                            | (If failed — log in defect register)                                                           |
| **Business Comments**                    | (User observations, suggestions, or feedback during UAT)                                       |
| **Executed By / Date**                   | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                      |
|                                          |                                                                                                |

|                                                             |                                                                                                                             |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **UAT-CLN-002 \| View Patient History Before Consultation** |                                                                                                                             |
| **Role / Actor**                                            | Doctor                                                                                                                      |
| **RTM Reference**                                           | O-03 → BR-REQ-CLN-01 → FR-CLN-02                                                                                            |
| **STC Reference**                                           | TC-CLN-001                                                                                                                  |
| **Priority**                                                | Must Have                                                                                                                   |
| **Business Scenario**                                       | As a Doctor, I need to review a patient's history, allergies, and vitals before the consultation.                           |
| **Given (Precondition)**                                    | Patient has a prior consultation and vitals recorded for today's visit.                                                     |
| **When (User Action)**                                      | I open the patient card from my appointment list.                                                                           |
| **Then (Acceptance Criterion)**                             | I can see demographics, known allergies, current medications, eye conditions, past history, and today's vitals in one view. |
| **Fail Condition**                                          | I cannot see other doctors' patient records from my dashboard.                                                              |
| **Actual Result**                                           | (To be completed during execution)                                                                                          |
| **Pass / Fail**                                             | ☐ Pass ☐ Fail                                                                                                               |
| **Defect ID**                                               | (If failed — log in defect register)                                                                                        |
| **Business Comments**                                       | (User observations, suggestions, or feedback during UAT)                                                                    |
| **Executed By / Date**                                      | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                   |
|                                                             |                                                                                                                             |

|                                             |                                                                                                                   |
|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **UAT-CLN-003 \| Record Consultation Note** |                                                                                                                   |
| **Role / Actor**                            | Doctor                                                                                                            |
| **RTM Reference**                           | O-03 → BR-REQ-CLN-01 → FR-CLN-03                                                                                  |
| **STC Reference**                           | TC-CLN-001                                                                                                        |
| **Priority**                                | Must Have                                                                                                         |
| **Business Scenario**                       | As a Doctor, I need to record my findings and treatment plan after examining the patient.                         |
| **Given (Precondition)**                    | Appointment is In-Progress. I have examined the patient.                                                          |
| **When (User Action)**                      | I enter Chief Complaint, Findings, Diagnosis, and Treatment Plan. I save the note.                                |
| **Then (Acceptance Criterion)**             | The consultation note is saved showing my name and the date/time recorded. I can see it when I reopen the record. |
| **Fail Condition**                          | If I leave the Diagnosis field blank, the system does not save and highlights the missing field.                  |
| **Actual Result**                           | (To be completed during execution)                                                                                |
| **Pass / Fail**                             | ☐ Pass ☐ Fail                                                                                                     |
| **Defect ID**                               | (If failed — log in defect register)                                                                              |
| **Business Comments**                       | (User observations, suggestions, or feedback during UAT)                                                          |
| **Executed By / Date**                      | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                         |
|                                             |                                                                                                                   |

|                                            |                                                                                              |
|--------------------------------------------|----------------------------------------------------------------------------------------------|
| **UAT-CLN-004 \| Generate a Prescription** |                                                                                              |
| **Role / Actor**                           | Doctor                                                                                       |
| **RTM Reference**                          | O-03 → BR-REQ-CLN-02 → FR-CLN-04                                                             |
| **STC Reference**                          | TC-CLN-002                                                                                   |
| **Priority**                               | Must Have                                                                                    |
| **Business Scenario**                      | As a Doctor, I need to issue a digital prescription for the patient.                         |
| **Given (Precondition)**                   | Consultation note has been saved.                                                            |
| **When (User Action)**                     | I navigate to Prescription, add the drug name, dosage, frequency, and duration, and save.    |
| **Then (Acceptance Criterion)**            | The prescription is saved and linked to this visit. The patient can view it in their portal. |
| **Fail Condition**                         | If I try to save a prescription before saving the consultation note, the system blocks me.   |
| **Actual Result**                          | (To be completed during execution)                                                           |
| **Pass / Fail**                            | ☐ Pass ☐ Fail                                                                                |
| **Defect ID**                              | (If failed — log in defect register)                                                         |
| **Business Comments**                      | (User observations, suggestions, or feedback during UAT)                                     |
| **Executed By / Date**                     | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                    |
|                                            |                                                                                              |

|                                              |                                                                                                                            |
|----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| **UAT-CLN-005 \| Complete the Consultation** |                                                                                                                            |
| **Role / Actor**                             | Doctor                                                                                                                     |
| **RTM Reference**                            | O-03 → BR-REQ-CLN-01 → FR-CLN-03                                                                                           |
| **STC Reference**                            | TC-CLN-006                                                                                                                 |
| **Priority**                                 | Must Have                                                                                                                  |
| **Business Scenario**                        | As a Doctor, I want to mark the consultation as complete when finished.                                                    |
| **Given (Precondition)**                     | Consultation note and prescription saved.                                                                                  |
| **When (User Action)**                       | I click Complete Consultation.                                                                                             |
| **Then (Acceptance Criterion)**              | Appointment status changes to Completed. Patient disappears from active queue. Receptionist can now check out the patient. |
| **Fail Condition**                           | If I try to complete without saving a consultation note, the system does not allow it.                                     |
| **Actual Result**                            | (To be completed during execution)                                                                                         |
| **Pass / Fail**                              | ☐ Pass ☐ Fail                                                                                                              |
| **Defect ID**                                | (If failed — log in defect register)                                                                                       |
| **Business Comments**                        | (User observations, suggestions, or feedback during UAT)                                                                   |
| **Executed By / Date**                       | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                  |
|                                              |                                                                                                                            |

|                                                              |                                                                                                  |
|--------------------------------------------------------------|--------------------------------------------------------------------------------------------------|
| **UAT-CLN-006 \| Consultation Record Locked After 24 Hours** |                                                                                                  |
| **Role / Actor**                                             | Doctor                                                                                           |
| **RTM Reference**                                            | O-03 → BR-REQ-CLN-04 → FR-CLN-05                                                                 |
| **STC Reference**                                            | TC-CLN-004                                                                                       |
| **Priority**                                                 | Should Have                                                                                      |
| **Business Scenario**                                        | As a Doctor, I understand consultation records are locked after 24 hours for clinical integrity. |
| **Given (Precondition)**                                     | A consultation record was saved more than 24 hours ago.                                          |
| **When (User Action)**                                       | I open the old consultation and attempt to change the Diagnosis.                                 |
| **Then (Acceptance Criterion)**                              | All fields are read-only. I see a message that the record is locked. I cannot save changes.      |
| **Fail Condition**                                           | The 24-hour lock applies even if I am the original author of the record.                         |
| **Actual Result**                                            | (To be completed during execution)                                                               |
| **Pass / Fail**                                              | ☐ Pass ☐ Fail                                                                                    |
| **Defect ID**                                                | (If failed — log in defect register)                                                             |
| **Business Comments**                                        | (User observations, suggestions, or feedback during UAT)                                         |
| **Executed By / Date**                                       | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                        |
|                                                              |                                                                                                  |

## 5. Clinician Scenarios — UAT-CLN-007 to UAT-CLN-008
|                                          |                                                                                                         |
|------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **UAT-CLN-007 \| Record Patient Vitals** |                                                                                                         |
| **Role / Actor**                         | Clinician                                                                                               |
| **RTM Reference**                        | O-03 → BR-REQ-CLN-03 → FR-CLN-08                                                                        |
| **STC Reference**                        | TC-CLN-003                                                                                              |
| **Priority**                             | Must Have                                                                                               |
| **Business Scenario**                    | As a Clinician, I need to record patient vital signs before the Doctor starts the consultation.         |
| **Given (Precondition)**                 | Patient 'Raj Shah' is Checked-In for a 10:00 AM appointment. I am logged in as Clinician.               |
| **When (User Action)**                   | I find the patient in my list, enter Visual Acuity, IOP, Blood Pressure, and Weight, and save.          |
| **Then (Acceptance Criterion)**          | Vitals are saved. The treating Doctor can immediately see them in the patient card during consultation. |
| **Fail Condition**                       | If I enter IOP above 21, I see a caution advisory but can still save the record normally.               |
| **Actual Result**                        | (To be completed during execution)                                                                      |
| **Pass / Fail**                          | ☐ Pass ☐ Fail                                                                                           |
| **Defect ID**                            | (If failed — log in defect register)                                                                    |
| **Business Comments**                    | (User observations, suggestions, or feedback during UAT)                                                |
| **Executed By / Date**                   | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                               |
|                                          |                                                                                                         |

|                                                       |                                                                                                         |
|-------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **UAT-CLN-008 \| Vitals Cannot Be Entered by Doctor** |                                                                                                         |
| **Role / Actor**                                      | Clinician / Doctor                                                                                      |
| **RTM Reference**                                     | O-03 → BR-REQ-CLN-03 → FR-CLN-10                                                                        |
| **STC Reference**                                     | TC-CLN-003                                                                                              |
| **Priority**                                          | Must Have                                                                                               |
| **Business Scenario**                                 | As the system, I need to ensure only Clinicians can record vitals — Doctors have read-only access.      |
| **Given (Precondition)**                              | A Doctor is logged in and viewing a patient card.                                                       |
| **When (User Action)**                                | The Doctor attempts to enter or change vitals.                                                          |
| **Then (Acceptance Criterion)**                       | No vitals input fields are available to the Doctor. Vitals are displayed as read-only information only. |
| **Fail Condition**                                    | This restriction applies even to the treating physician for that patient.                               |
| **Actual Result**                                     | (To be completed during execution)                                                                      |
| **Pass / Fail**                                       | ☐ Pass ☐ Fail                                                                                           |
| **Defect ID**                                         | (If failed — log in defect register)                                                                    |
| **Business Comments**                                 | (User observations, suggestions, or feedback during UAT)                                                |
| **Executed By / Date**                                | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                               |
|                                                       |                                                                                                         |

## 6. Patient Scenarios — UAT-PAT-001 to UAT-PAT-003
|                                         |                                                                                                                       |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------|
| **UAT-PAT-001 \| View My Appointments** |                                                                                                                       |
| **Role / Actor**                        | Patient                                                                                                               |
| **RTM Reference**                       | O-01 → BR-REQ-PR-04 → FR-PAT-01                                                                                       |
| **STC Reference**                       | TC-PR-004                                                                                                             |
| **Priority**                            | Should Have                                                                                                           |
| **Business Scenario**                   | As a Patient, I want to see my appointment history and upcoming appointments.                                         |
| **Given (Precondition)**                | I am registered and have 2 past and 1 upcoming appointment.                                                           |
| **When (User Action)**                  | I log in to the Patient Portal and navigate to My Appointments.                                                       |
| **Then (Acceptance Criterion)**         | I can see all 3 appointments with date, time, Doctor name, and status. I cannot see any other patient's appointments. |
| **Fail Condition**                      | If I have no appointments, the page shows a clear 'No appointments found' message — not a blank screen.               |
| **Actual Result**                       | (To be completed during execution)                                                                                    |
| **Pass / Fail**                         | ☐ Pass ☐ Fail                                                                                                         |
| **Defect ID**                           | (If failed — log in defect register)                                                                                  |
| **Business Comments**                   | (User observations, suggestions, or feedback during UAT)                                                              |
| **Executed By / Date**                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                             |
|                                         |                                                                                                                       |

|                                              |                                                                                                                   |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| **UAT-PAT-002 \| View Consultation Summary** |                                                                                                                   |
| **Role / Actor**                             | Patient                                                                                                           |
| **RTM Reference**                            | O-03 → BR-REQ-CLN-01 → FR-PAT-02                                                                                  |
| **STC Reference**                            | TC-CLN-001                                                                                                        |
| **Priority**                                 | Should Have                                                                                                       |
| **Business Scenario**                        | As a Patient, I want to see the outcome of my completed consultation.                                             |
| **Given (Precondition)**                     | I have a Completed appointment with a consultation note and prescription.                                         |
| **When (User Action)**                       | I open the completed appointment in my portal.                                                                    |
| **Then (Acceptance Criterion)**              | I can see the Diagnosis and Treatment Plan summary, and my prescription details.                                  |
| **Fail Condition**                           | I cannot see the Doctor's detailed examination findings or full clinical notes — only the patient-facing summary. |
| **Actual Result**                            | (To be completed during execution)                                                                                |
| **Pass / Fail**                              | ☐ Pass ☐ Fail                                                                                                     |
| **Defect ID**                                | (If failed — log in defect register)                                                                              |
| **Business Comments**                        | (User observations, suggestions, or feedback during UAT)                                                          |
| **Executed By / Date**                       | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                         |
|                                              |                                                                                                                   |

|                                              |                                                                                  |
|----------------------------------------------|----------------------------------------------------------------------------------|
| **UAT-PAT-003 \| Update My Contact Details** |                                                                                  |
| **Role / Actor**                             | Patient                                                                          |
| **RTM Reference**                            | O-01 → BR-REQ-PR-04 → FR-PAT-03                                                  |
| **STC Reference**                            | TC-PR-004                                                                        |
| **Priority**                                 | Should Have                                                                      |
| **Business Scenario**                        | As a Patient, I want to update my mobile number.                                 |
| **Given (Precondition)**                     | I am logged in to the Patient Portal.                                            |
| **When (User Action)**                       | I navigate to my profile, update my mobile number, and save.                     |
| **Then (Acceptance Criterion)**              | The updated mobile number is saved and displayed correctly on my profile.        |
| **Fail Condition**                           | I cannot update clinical information such as diagnosis, prescription, or vitals. |
| **Actual Result**                            | (To be completed during execution)                                               |
| **Pass / Fail**                              | ☐ Pass ☐ Fail                                                                    |
| **Defect ID**                                | (If failed — log in defect register)                                             |
| **Business Comments**                        | (User observations, suggestions, or feedback during UAT)                         |
| **Executed By / Date**                       | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_        |
|                                              |                                                                                  |

## 7. System Administrator Scenarios — UAT-AM-001 to UAT-IT-004
|                                                       |                                                                                                                              |
|-------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| **UAT-AM-001 \| All Roles Access Only Their Modules** |                                                                                                                              |
| **Role / Actor**                                      | System Administrator                                                                                                         |
| **RTM Reference**                                     | O-04 → BR-REQ-AM-02 → FR-AM-02                                                                                               |
| **STC Reference**                                     | TC-AM-002                                                                                                                    |
| **Priority**                                          | Must Have                                                                                                                    |
| **Business Scenario**                                 | As System Administrator, I need to confirm role-based access is correctly enforced.                                          |
| **Given (Precondition)**                              | One active account per role exists.                                                                                          |
| **When (User Action)**                                | I observe each role representative log in and confirm they can only see their designated sections.                           |
| **Then (Acceptance Criterion)**                       | Each role sees only their entitled modules. Attempts to navigate to restricted areas redirect the user to their home screen. |
| **Fail Condition**                                    | No role should have access to the audit log modification controls.                                                           |
| **Actual Result**                                     | (To be completed during execution)                                                                                           |
| **Pass / Fail**                                       | ☐ Pass ☐ Fail                                                                                                                |
| **Defect ID**                                         | (If failed — log in defect register)                                                                                         |
| **Business Comments**                                 | (User observations, suggestions, or feedback during UAT)                                                                     |
| **Executed By / Date**                                | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                    |
|                                                       |                                                                                                                              |

|                                           |                                                                                                          |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **UAT-AM-002 \| No Access Without Login** |                                                                                                          |
| **Role / Actor**                          | System Administrator                                                                                     |
| **RTM Reference**                         | O-04 → BR-REQ-AM-01 → FR-AM-01                                                                           |
| **STC Reference**                         | TC-AM-001                                                                                                |
| **Priority**                              | Must Have                                                                                                |
| **Business Scenario**                     | As System Administrator, I want to confirm no portal content is accessible without authentication.       |
| **Given (Precondition)**                  | Application running. No active sessions.                                                                 |
| **When (User Action)**                    | I attempt to open a portal module URL directly without logging in.                                       |
| **Then (Acceptance Criterion)**           | The browser redirects to the login page. No patient data, appointments, or clinical records are visible. |
| **Fail Condition**                        | This must apply to all module URLs — not just the home page.                                             |
| **Actual Result**                         | (To be completed during execution)                                                                       |
| **Pass / Fail**                           | ☐ Pass ☐ Fail                                                                                            |
| **Defect ID**                             | (If failed — log in defect register)                                                                     |
| **Business Comments**                     | (User observations, suggestions, or feedback during UAT)                                                 |
| **Executed By / Date**                    | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                |
|                                           |                                                                                                          |

|                                                                |                                                                                                                                                          |
|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-AM-003 \| Account Locks After Repeated Wrong Passwords** |                                                                                                                                                          |
| **Role / Actor**                                               | System Administrator                                                                                                                                     |
| **RTM Reference**                                              | O-04 → BR-REQ-AM-04 → FR-AM-04                                                                                                                           |
| **STC Reference**                                              | TC-AM-004                                                                                                                                                |
| **Priority**                                                   | Must Have                                                                                                                                                |
| **Business Scenario**                                          | As System Administrator, I need to confirm the account lockout policy works.                                                                             |
| **Given (Precondition)**                                       | Active user account with no prior failed attempts.                                                                                                       |
| **When (User Action)**                                         | I ask the user to enter the wrong password three times in a row.                                                                                         |
| **Then (Acceptance Criterion)**                                | After the third failed attempt, the account is locked. The user sees a clear message. The account shows status=Locked in the System Administrator panel. |
| **Fail Condition**                                             | The correct password does not work while locked. Only I can unlock it.                                                                                   |
| **Actual Result**                                              | (To be completed during execution)                                                                                                                       |
| **Pass / Fail**                                                | ☐ Pass ☐ Fail                                                                                                                                            |
| **Defect ID**                                                  | (If failed — log in defect register)                                                                                                                     |
| **Business Comments**                                          | (User observations, suggestions, or feedback during UAT)                                                                                                 |
| **Executed By / Date**                                         | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                |
|                                                                |                                                                                                                                                          |

|                                                    |                                                                                                        |
|----------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| **UAT-AM-004 \| Session Expires After Inactivity** |                                                                                                        |
| **Role / Actor**                                   | System Administrator                                                                                   |
| **RTM Reference**                                  | O-04 → BR-REQ-AM-03 → FR-AM-03                                                                         |
| **STC Reference**                                  | TC-AM-003                                                                                              |
| **Priority**                                       | Must Have                                                                                              |
| **Business Scenario**                              | As System Administrator, I want to verify idle sessions are automatically ended.                       |
| **Given (Precondition)**                           | A user is logged in but has been inactive for more than 15 minutes.                                    |
| **When (User Action)**                             | After the inactivity period, I attempt to interact with the portal.                                    |
| **Then (Acceptance Criterion)**                    | The portal redirects to the login screen with a message: 'Your session has expired due to inactivity.' |
| **Fail Condition**                                 | A user actively using the system does not get logged out mid-session.                                  |
| **Actual Result**                                  | (To be completed during execution)                                                                     |
| **Pass / Fail**                                    | ☐ Pass ☐ Fail                                                                                          |
| **Defect ID**                                      | (If failed — log in defect register)                                                                   |
| **Business Comments**                              | (User observations, suggestions, or feedback during UAT)                                               |
| **Executed By / Date**                             | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                              |
|                                                    |                                                                                                        |

|                                                   |                                                                                                                                               |
|---------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-IT-001 \| Create and Manage User Accounts** |                                                                                                                                               |
| **Role / Actor**                                  | System Administrator                                                                                                                          |
| **RTM Reference**                                 | O-05 → BR-REQ-IT-01 → FR-IT-01                                                                                                                |
| **STC Reference**                                 | TC-IT-001                                                                                                                                     |
| **Priority**                                      | Must Have                                                                                                                                     |
| **Business Scenario**                             | As System Administrator, I need to add, update, and deactivate portal user accounts.                                                          |
| **Given (Precondition)**                          | I am logged in as System Administrator.                                                                                                       |
| **When (User Action)**                            | I create a new Doctor account, change their role to Receptionist, then deactivate the account.                                                |
| **Then (Acceptance Criterion)**                   | New account created and usable. Role change takes effect on next login. Deactivated account cannot log in. All changes recorded in audit log. |
| **Fail Condition**                                | I cannot delete a user account — only deactivate it. Historical records linked to the user are retained.                                      |
| **Actual Result**                                 | (To be completed during execution)                                                                                                            |
| **Pass / Fail**                                   | ☐ Pass ☐ Fail                                                                                                                                 |
| **Defect ID**                                     | (If failed — log in defect register)                                                                                                          |
| **Business Comments**                             | (User observations, suggestions, or feedback during UAT)                                                                                      |
| **Executed By / Date**                            | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                     |
|                                                   |                                                                                                                                               |

|                                  |                                                                                                                                             |
|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-IT-002 \| View Audit Log** |                                                                                                                                             |
| **Role / Actor**                 | System Administrator                                                                                                                        |
| **RTM Reference**                | O-05 → BR-REQ-IT-02 → FR-IT-02                                                                                                              |
| **STC Reference**                | TC-IT-002                                                                                                                                   |
| **Priority**                     | Must Have                                                                                                                                   |
| **Business Scenario**            | As System Administrator, I need to review a complete log of all portal activity.                                                            |
| **Given (Precondition)**         | Multiple users have performed registrations, logins, and updates.                                                                           |
| **When (User Action)**           | I navigate to the Audit Log Viewer and apply filters by date and action type.                                                               |
| **Then (Acceptance Criterion)**  | I can see a complete list of events with user, action, module, and timestamp. I can filter to find specific events. I can export to a file. |
| **Fail Condition**               | I cannot edit or delete any entry in the audit log.                                                                                         |
| **Actual Result**                | (To be completed during execution)                                                                                                          |
| **Pass / Fail**                  | ☐ Pass ☐ Fail                                                                                                                               |
| **Defect ID**                    | (If failed — log in defect register)                                                                                                        |
| **Business Comments**            | (User observations, suggestions, or feedback during UAT)                                                                                    |
| **Executed By / Date**           | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                   |
|                                  |                                                                                                                                             |

|                                                   |                                                                                                                                          |
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-IT-003 \| Configure Hospital Closed Dates** |                                                                                                                                          |
| **Role / Actor**                                  | System Administrator                                                                                                                     |
| **RTM Reference**                                 | O-05 → BR-APT-08 → FR-IT-04                                                                                                              |
| **STC Reference**                                 | TC-IT-004                                                                                                                                |
| **Priority**                                      | Should Have                                                                                                                              |
| **Business Scenario**                             | As System Administrator, I want to block appointment bookings on hospital holidays.                                                      |
| **Given (Precondition)**                          | I am logged in as System Administrator.                                                                                                  |
| **When (User Action)**                            | I add next Sunday as a hospital closed day. I then ask a Receptionist to book on that date.                                              |
| **Then (Acceptance Criterion)**                   | The Receptionist cannot select that date for booking. A message indicates the date is unavailable. Existing appointments are unaffected. |
| **Fail Condition**                                | Removing the date from configuration restores the ability to book on that date.                                                          |
| **Actual Result**                                 | (To be completed during execution)                                                                                                       |
| **Pass / Fail**                                   | ☐ Pass ☐ Fail                                                                                                                            |
| **Defect ID**                                     | (If failed — log in defect register)                                                                                                     |
| **Business Comments**                             | (User observations, suggestions, or feedback during UAT)                                                                                 |
| **Executed By / Date**                            | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                |
|                                                   |                                                                                                                                          |

|                                           |                                                                                                     |
|-------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **UAT-IT-004 \| Unlock a Locked Account** |                                                                                                     |
| **Role / Actor**                          | System Administrator                                                                                |
| **RTM Reference**                         | O-05 → BR-REQ-IT-01 → FR-IT-01                                                                      |
| **STC Reference**                         | TC-IT-001                                                                                           |
| **Priority**                              | Must Have                                                                                           |
| **Business Scenario**                     | As System Administrator, I need to restore access to a locked account.                              |
| **Given (Precondition)**                  | A Doctor account is locked after 3 failed login attempts.                                           |
| **When (User Action)**                    | I find the locked account in user management and unlock it.                                         |
| **Then (Acceptance Criterion)**           | The Doctor can now log in. Failed login counter reset to zero. Unlock action recorded in audit log. |
| **Fail Condition**                        | Unlocking does not alter the user's role or permissions.                                            |
| **Actual Result**                         | (To be completed during execution)                                                                  |
| **Pass / Fail**                           | ☐ Pass ☐ Fail                                                                                       |
| **Defect ID**                             | (If failed — log in defect register)                                                                |
| **Business Comments**                     | (User observations, suggestions, or feedback during UAT)                                            |
| **Executed By / Date**                    | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                           |
|                                           |                                                                                                     |

## 8. Dean & Admin Scenarios — UAT-RPT-001 to UAT-RPT-005
|                                                   |                                                                                                    |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------|
| **UAT-RPT-001 \| View Daily Appointment Summary** |                                                                                                    |
| **Role / Actor**                                  | Dean / Admin                                                                                       |
| **RTM Reference**                                 | O-08 → RPT-01 → FR-RPT-01, FR-RPT-02                                                               |
| **STC Reference**                                 | TC-RPT-001                                                                                         |
| **Priority**                                      | Should Have                                                                                        |
| **Business Scenario**                             | As the Dean, I want to see a daily summary of appointment activity.                                |
| **Given (Precondition)**                          | Today has a mix of Completed, Cancelled, and No-Show appointments.                                 |
| **When (User Action)**                            | I open the Daily Appointment Summary report for today.                                             |
| **Then (Acceptance Criterion)**                   | I can see total appointments broken down by status. I can filter by doctor. I can export the data. |
| **Fail Condition**                                | The report shows accurate numbers that match what the Receptionist has processed today.            |
| **Actual Result**                                 | (To be completed during execution)                                                                 |
| **Pass / Fail**                                   | ☐ Pass ☐ Fail                                                                                      |
| **Defect ID**                                     | (If failed — log in defect register)                                                               |
| **Business Comments**                             | (User observations, suggestions, or feedback during UAT)                                           |
| **Executed By / Date**                            | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                          |
|                                                   |                                                                                                    |

|                                            |                                                                                                 |
|--------------------------------------------|-------------------------------------------------------------------------------------------------|
| **UAT-RPT-002 \| View Doctor Utilisation** |                                                                                                 |
| **Role / Actor**                           | Dean / Admin                                                                                    |
| **RTM Reference**                          | O-08 → RPT-02 → FR-RPT-03                                                                       |
| **STC Reference**                          | TC-RPT-002                                                                                      |
| **Priority**                               | Should Have                                                                                     |
| **Business Scenario**                      | As the Dean, I want to understand how efficiently appointment slots are being used.             |
| **Given (Precondition)**                   | Multiple doctors with varying appointment loads.                                                |
| **When (User Action)**                     | I open the Doctor Utilisation report for this week.                                             |
| **Then (Acceptance Criterion)**            | I can see each doctor's appointment count versus available slots with a utilisation percentage. |
| **Fail Condition**                         | A doctor with 0 appointments shows 0% utilisation and is still included in the report.          |
| **Actual Result**                          | (To be completed during execution)                                                              |
| **Pass / Fail**                            | ☐ Pass ☐ Fail                                                                                   |
| **Defect ID**                              | (If failed — log in defect register)                                                            |
| **Business Comments**                      | (User observations, suggestions, or feedback during UAT)                                        |
| **Executed By / Date**                     | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                       |
|                                            |                                                                                                 |

|                                                         |                                                                                                                                 |
|---------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| **UAT-RPT-003 \| View No-Show and Cancellation Trends** |                                                                                                                                 |
| **Role / Actor**                                        | Dean / Admin                                                                                                                    |
| **RTM Reference**                                       | O-08 → RPT-04 → FR-RPT-04                                                                                                       |
| **STC Reference**                                       | TC-RPT-004                                                                                                                      |
| **Priority**                                            | Should Have                                                                                                                     |
| **Business Scenario**                                   | As the Dean, I want to monitor no-show and cancellation patterns.                                                               |
| **Given (Precondition)**                                | No-Show and Cancelled appointments exist.                                                                                       |
| **When (User Action)**                                  | I open the No-Show and Cancellation report for the current month.                                                               |
| **Then (Acceptance Criterion)**                         | I can see counts for No-Shows and Cancellations. Late Cancellations are identified separately. A chart makes the trend visible. |
| **Fail Condition**                                      | Completed appointments must not appear in this report.                                                                          |
| **Actual Result**                                       | (To be completed during execution)                                                                                              |
| **Pass / Fail**                                         | ☐ Pass ☐ Fail                                                                                                                   |
| **Defect ID**                                           | (If failed — log in defect register)                                                                                            |
| **Business Comments**                                   | (User observations, suggestions, or feedback during UAT)                                                                        |
| **Executed By / Date**                                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                       |
|                                                         |                                                                                                                                 |

|                                                      |                                                                                           |
|------------------------------------------------------|-------------------------------------------------------------------------------------------|
| **UAT-RPT-004 \| View Patient Registration Summary** |                                                                                           |
| **Role / Actor**                                     | Dean / Admin                                                                              |
| **RTM Reference**                                    | O-08 → RPT-03 → FR-RPT-03                                                                 |
| **STC Reference**                                    | TC-RPT-003                                                                                |
| **Priority**                                         | Should Have                                                                               |
| **Business Scenario**                                | As the Dean, I want to track patient registration volume.                                 |
| **Given (Precondition)**                             | New patients registered in the past 7 days.                                               |
| **When (User Action)**                               | I open the Patient Registration Summary report.                                           |
| **Then (Acceptance Criterion)**                      | I can see the number of new registrations this week and a trend over the selected period. |
| **Fail Condition**                                   | Deactivated patient records are excluded from the active patient count.                   |
| **Actual Result**                                    | (To be completed during execution)                                                        |
| **Pass / Fail**                                      | ☐ Pass ☐ Fail                                                                             |
| **Defect ID**                                        | (If failed — log in defect register)                                                      |
| **Business Comments**                                | (User observations, suggestions, or feedback during UAT)                                  |
| **Executed By / Date**                               | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                 |
|                                                      |                                                                                           |

|                                                   |                                                                                                          |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **UAT-RPT-005 \| View Compliance Status Summary** |                                                                                                          |
| **Role / Actor**                                  | Dean / Admin                                                                                             |
| **RTM Reference**                                 | O-06 + O-08 → RPT-06 → FR-RPT-05                                                                         |
| **STC Reference**                                 | TC-RPT-006                                                                                               |
| **Priority**                                      | Should Have                                                                                              |
| **Business Scenario**                             | As the Dean, I want to confirm the portal is operating within compliance expectations.                   |
| **Given (Precondition)**                          | I am logged in as Dean/Admin.                                                                            |
| **When (User Action)**                            | I open the Compliance Status Summary report.                                                             |
| **Then (Acceptance Criterion)**                   | I can see consent coverage percentage, any access control deviations, and audit log completeness status. |
| **Fail Condition**                                | The report displays a clean confirmation when no compliance flags exist — not a blank or error screen.   |
| **Actual Result**                                 | (To be completed during execution)                                                                       |
| **Pass / Fail**                                   | ☐ Pass ☐ Fail                                                                                            |
| **Defect ID**                                     | (If failed — log in defect register)                                                                     |
| **Business Comments**                             | (User observations, suggestions, or feedback during UAT)                                                 |
| **Executed By / Date**                            | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                |
|                                                   |                                                                                                          |

## 9. Cross-Role Acceptance Scenarios — UAT-SEC-001 to UAT-UX-003
*UAT-UX scenarios reference NFR-05, NFR-06 (CVH-BRD-001 v1.3 Section 11) and T-NFR-02 (CVH-FRD-001 v1.2 Section 17). No dedicated FR-UX IDs exist — UX is governed by NFRs.*

|                                                              |                                                                                                                                                                 |
|--------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-SEC-001 \| Patient Consent Confirmed at Registration** |                                                                                                                                                                 |
| **Role / Actor**                                             | Receptionist / Compliance                                                                                                                                       |
| **RTM Reference**                                            | O-06 → DPDP-01 → FR-PR-03, FR-PAT-04                                                                                                                            |
| **STC Reference**                                            | TC-SEC-001                                                                                                                                                      |
| **Priority**                                                 | Must Have                                                                                                                                                       |
| **Business Scenario**                                        | As a Compliance Officer, I want to verify no patient record exists without confirmed consent.                                                                   |
| **Given (Precondition)**                                     | Several patients have been registered through the system.                                                                                                       |
| **When (User Action)**                                       | I review a sample of patient records and confirm consent is displayed before each registration was completed.                                                   |
| **Then (Acceptance Criterion)**                              | Every active patient record shows consent was given. The portal does not allow registration without consent being confirmed by the patient or the Receptionist. |
| **Fail Condition**                                           | The system must not allow a patient record to be created if consent was refused.                                                                                |
| **Actual Result**                                            | (To be completed during execution)                                                                                                                              |
| **Pass / Fail**                                              | ☐ Pass ☐ Fail                                                                                                                                                   |
| **Defect ID**                                                | (If failed — log in defect register)                                                                                                                            |
| **Business Comments**                                        | (User observations, suggestions, or feedback during UAT)                                                                                                        |
| **Executed By / Date**                                       | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                       |
|                                                              |                                                                                                                                                                 |

|                                                       |                                                                                                                                                                 |
|-------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-SEC-002 \| Each User Sees Only What They Need** |                                                                                                                                                                 |
| **Role / Actor**                                      | All Roles                                                                                                                                                       |
| **RTM Reference**                                     | O-04 → BR-REQ-AM-02 → FR-AM-02                                                                                                                                  |
| **STC Reference**                                     | TC-AM-002                                                                                                                                                       |
| **Priority**                                          | Must Have                                                                                                                                                       |
| **Business Scenario**                                 | As a Compliance Officer, I want to confirm minimum necessary access is enforced.                                                                                |
| **Given (Precondition)**                              | All 6 role accounts active.                                                                                                                                     |
| **When (User Action)**                                | Each role representative confirms they cannot see modules outside their entitlement.                                                                            |
| **Then (Acceptance Criterion)**                       | No role can access another role's data or functions. Clinical records visible only to clinical roles. Audit logs only visible to System Administrator and Dean. |
| **Fail Condition**                                    | No workaround (normal navigation or direct URL entry) allows access to restricted modules.                                                                      |
| **Actual Result**                                     | (To be completed during execution)                                                                                                                              |
| **Pass / Fail**                                       | ☐ Pass ☐ Fail                                                                                                                                                   |
| **Defect ID**                                         | (If failed — log in defect register)                                                                                                                            |
| **Business Comments**                                 | (User observations, suggestions, or feedback during UAT)                                                                                                        |
| **Executed By / Date**                                | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                       |
|                                                       |                                                                                                                                                                 |

|                                                         |                                                                                                                                               |
|---------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-SEC-003 \| Audit Trail Confirms All Key Actions** |                                                                                                                                               |
| **Role / Actor**                                        | System Administrator                                                                                                                          |
| **RTM Reference**                                       | O-05 → BR-REQ-IT-02 → FR-AUD-01                                                                                                               |
| **STC Reference**                                       | TC-SEC-004                                                                                                                                    |
| **Priority**                                            | Must Have                                                                                                                                     |
| **Business Scenario**                                   | As a Compliance Officer, I want to confirm all significant actions are recorded.                                                              |
| **Given (Precondition)**                                | A full day of portal activity: registrations, logins, appointments, consultations.                                                            |
| **When (User Action)**                                  | I review the audit log for today's activity.                                                                                                  |
| **Then (Acceptance Criterion)**                         | I can find audit entries for every registration, login, appointment change, and consultation. Each shows who did it, what they did, and when. |
| **Fail Condition**                                      | No gaps in the audit log for any key business transaction.                                                                                    |
| **Actual Result**                                       | (To be completed during execution)                                                                                                            |
| **Pass / Fail**                                         | ☐ Pass ☐ Fail                                                                                                                                 |
| **Defect ID**                                           | (If failed — log in defect register)                                                                                                          |
| **Business Comments**                                   | (User observations, suggestions, or feedback during UAT)                                                                                      |
| **Executed By / Date**                                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                     |
|                                                         |                                                                                                                                               |

|                                                         |                                                                                                                                      |
|---------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-SEC-004 \| Sensitive Data Not Exposed in Errors** |                                                                                                                                      |
| **Role / Actor**                                        | All Roles                                                                                                                            |
| **RTM Reference**                                       | O-06 → FR-SEC-10                                                                                                                     |
| **STC Reference**                                       | TC-SEC-009                                                                                                                           |
| **Priority**                                            | Must Have                                                                                                                            |
| **Business Scenario**                                   | As a Compliance Officer, I want to confirm errors do not reveal sensitive system information.                                        |
| **Given (Precondition)**                                | Application running normally.                                                                                                        |
| **When (User Action)**                                  | I trigger an error by entering unexpected data in various fields.                                                                    |
| **Then (Acceptance Criterion)**                         | All error messages are in plain language. No technical details, database references, or file paths are visible in any error message. |
| **Fail Condition**                                      | This applies to all roles and all modules.                                                                                           |
| **Actual Result**                                       | (To be completed during execution)                                                                                                   |
| **Pass / Fail**                                         | ☐ Pass ☐ Fail                                                                                                                        |
| **Defect ID**                                           | (If failed — log in defect register)                                                                                                 |
| **Business Comments**                                   | (User observations, suggestions, or feedback during UAT)                                                                             |
| **Executed By / Date**                                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                            |
|                                                         |                                                                                                                                      |

|                                                         |                                                                                                                                                       |
|---------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-UX-001 \| Each Role Sees a Relevant Home Screen** |                                                                                                                                                       |
| **Role / Actor**                                        | All Roles                                                                                                                                             |
| **RTM Reference**                                       | O-07 → NFR-05 (BRD Section 11)                                                                                                                        |
| **STC Reference**                                       | TC-UX-001                                                                                                                                             |
| **Priority**                                            | Should Have                                                                                                                                           |
| **Business Scenario**                                   | As each role representative, I expect to see only the tools relevant to my job when I log in.                                                         |
| **Given (Precondition)**                                | All 6 role accounts active.                                                                                                                           |
| **When (User Action)**                                  | Each role representative logs in and reviews their home screen and navigation.                                                                        |
| **Then (Acceptance Criterion)**                         | Every role sees a clean, role-specific interface. Navigation shows only entitled modules. The experience feels appropriate to daily responsibilities. |
| **Fail Condition**                                      | No role sees a blank screen or error on login.                                                                                                        |
| **Actual Result**                                       | (To be completed during execution)                                                                                                                    |
| **Pass / Fail**                                         | ☐ Pass ☐ Fail                                                                                                                                         |
| **Defect ID**                                           | (If failed — log in defect register)                                                                                                                  |
| **Business Comments**                                   | (User observations, suggestions, or feedback during UAT)                                                                                              |
| **Executed By / Date**                                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                             |
|                                                         |                                                                                                                                                       |

|                                                                 |                                                                                                                                                             |
|-----------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-UX-002 \| Forms Give Clear Guidance When Input Is Wrong** |                                                                                                                                                             |
| **Role / Actor**                                                | Receptionist / All                                                                                                                                          |
| **RTM Reference**                                               | O-07 → NFR-06 (BRD Section 11)                                                                                                                              |
| **STC Reference**                                               | TC-UX-002                                                                                                                                                   |
| **Priority**                                                    | Should Have                                                                                                                                                 |
| **Business Scenario**                                           | As a Receptionist, I want the system to clearly tell me what went wrong if I make a mistake.                                                                |
| **Given (Precondition)**                                        | I am on the patient registration form.                                                                                                                      |
| **When (User Action)**                                          | I intentionally enter an invalid date of birth and a mobile number with only 8 digits. I submit.                                                            |
| **Then (Acceptance Criterion)**                                 | The system highlights both fields in red and shows a separate specific message for each — telling me exactly what is wrong and the correct format required. |
| **Fail Condition**                                              | A single generic 'form error' is not acceptable. Each field must have its own error message.                                                                |
| **Actual Result**                                               | (To be completed during execution)                                                                                                                          |
| **Pass / Fail**                                                 | ☐ Pass ☐ Fail                                                                                                                                               |
| **Defect ID**                                                   | (If failed — log in defect register)                                                                                                                        |
| **Business Comments**                                           | (User observations, suggestions, or feedback during UAT)                                                                                                    |
| **Executed By / Date**                                          | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                   |
|                                                                 |                                                                                                                                                             |

|                                                     |                                                                                                                                       |
|-----------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-UX-003 \| Application Works Across Browsers** |                                                                                                                                       |
| **Role / Actor**                                    | All Roles                                                                                                                             |
| **RTM Reference**                                   | O-07 → T-NFR-02 (FRD Section 17)                                                                                                      |
| **STC Reference**                                   | TC-UX-003                                                                                                                             |
| **Priority**                                        | Should Have                                                                                                                           |
| **Business Scenario**                               | As any portal user, I expect the application to work regardless of which modern browser I use.                                        |
| **Given (Precondition)**                            | Application running locally.                                                                                                          |
| **When (User Action)**                              | Each role representative accesses the portal using Chrome, Firefox, and Edge.                                                         |
| **Then (Acceptance Criterion)**                     | The portal loads correctly in all three browsers. Forms, reports, and dashboards display consistently. No features broken or missing. |
| **Fail Condition**                                  | The application must not require browser plugins or extensions to function.                                                           |
| **Actual Result**                                   | (To be completed during execution)                                                                                                    |
| **Pass / Fail**                                     | ☐ Pass ☐ Fail                                                                                                                         |
| **Defect ID**                                       | (If failed — log in defect register)                                                                                                  |
| **Business Comments**                               | (User observations, suggestions, or feedback during UAT)                                                                              |
| **Executed By / Date**                              | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                             |
|                                                     |                                                                                                                                       |

## 10. Patient Self-Registration Scenarios — UAT-PAT-SR-001 to UAT-PAT-SR-004 (CVH-CR-001)
|                                                         |                                                                                                                                                      |
|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PAT-SR-001 \| Register Without Staff Assistance** |                                                                                                                                                      |
| **Role / Actor**                                        | Patient (Unregistered)                                                                                                                               |
| **RTM Reference**                                       | O-01 → BR-PAT-07 → FR-PAT-05                                                                                                                         |
| **STC Reference**                                       | TC-PAT-SR-001                                                                                                                                        |
| **Priority**                                            | Must Have                                                                                                                                            |
| **Business Scenario**                                   | As a new patient, I want to register myself online without needing to visit Reception first.                                                         |
| **Given (Precondition)**                                | I am a new patient. I have not previously registered. I am on the hospital portal login page.                                                        |
| **When (User Action)**                                  | I click 'New Patient? Register Here', complete the registration form with my personal details and a password, tick the consent checkbox, and submit. |
| **Then (Acceptance Criterion)**                         | My registration is accepted. I receive a unique Patient ID. I am automatically logged in and taken to my Patient Portal where I can see my account.  |
| **Fail Condition**                                      | If I leave any required field blank, the system highlights the field and does not register me. If I do not tick the consent box, I cannot proceed.   |
| **Actual Result**                                       | (To be completed during execution)                                                                                                                   |
| **Pass / Fail**                                         | ☐ Pass ☐ Fail                                                                                                                                        |
| **Defect ID**                                           | (If failed — log in defect register)                                                                                                                 |
| **Business Comments**                                   | (User observations, suggestions, or feedback during UAT)                                                                                             |
| **Executed By / Date**                                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                            |
|                                                         |                                                                                                                                                      |

|                                                                         |                                                                                                                                                                                                 |
|-------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PAT-SR-002 \| System Identifies Possible Duplicate Registration** |                                                                                                                                                                                                 |
| **Role / Actor**                                                        | Patient (Unregistered)                                                                                                                                                                          |
| **RTM Reference**                                                       | O-01 → BR-PAT-08 → FR-PAT-06                                                                                                                                                                    |
| **STC Reference**                                                       | TC-PAT-SR-002                                                                                                                                                                                   |
| **Priority**                                                            | Must Have                                                                                                                                                                                       |
| **Business Scenario**                                                   | As a new patient, if I accidentally try to register twice, I expect the system to alert me rather than creating a duplicate.                                                                    |
| **Given (Precondition)**                                                | My details (name, date of birth, mobile) already exist in the system from a previous registration.                                                                                              |
| **When (User Action)**                                                  | I attempt to self-register with the same name, date of birth, and mobile number.                                                                                                                |
| **Then (Acceptance Criterion)**                                         | The system warns me that a record may already exist and advises me to contact Reception to access my account.                                                                                   |
| **Fail Condition**                                                      | If I register with the same mobile number but a different name, the system does NOT warn me and creates a new record. Only the combination of name + date of birth + mobile triggers the alert. |
| **Actual Result**                                                       | (To be completed during execution)                                                                                                                                                              |
| **Pass / Fail**                                                         | ☐ Pass ☐ Fail                                                                                                                                                                                   |
| **Defect ID**                                                           | (If failed — log in defect register)                                                                                                                                                            |
| **Business Comments**                                                   | (User observations, suggestions, or feedback during UAT)                                                                                                                                        |
| **Executed By / Date**                                                  | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                                                       |
|                                                                         |                                                                                                                                                                                                 |

|                                                               |                                                                                                                                                                                                           |
|---------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PAT-SR-003 \| Set My Own Password During Registration** |                                                                                                                                                                                                           |
| **Role / Actor**                                              | Patient (Unregistered)                                                                                                                                                                                    |
| **RTM Reference**                                             | O-04 → BR-PAT-09, BR-SEC-02 → FR-PAT-07, FR-PAT-08                                                                                                                                                        |
| **STC Reference**                                             | TC-PAT-SR-003                                                                                                                                                                                             |
| **Priority**                                                  | Must Have                                                                                                                                                                                                 |
| **Business Scenario**                                         | As a new patient, I want to set my own secure password when I register.                                                                                                                                   |
| **Given (Precondition)**                                      | I am on the self-registration form. No existing account for my mobile number.                                                                                                                             |
| **When (User Action)**                                        | I enter a password that does not meet the rules (e.g., too short or no uppercase letter), then attempt to register. I then enter a strong password and complete registration.                             |
| **Then (Acceptance Criterion)**                               | The weak password is rejected with a specific message telling me which rule I violated. When I enter a strong password and complete registration, my account is created and I am logged in automatically. |
| **Fail Condition**                                            | The error message must tell me specifically which rule was violated — not a generic 'password invalid' message.                                                                                           |
| **Actual Result**                                             | (To be completed during execution)                                                                                                                                                                        |
| **Pass / Fail**                                               | ☐ Pass ☐ Fail                                                                                                                                                                                             |
| **Defect ID**                                                 | (If failed — log in defect register)                                                                                                                                                                      |
| **Business Comments**                                         | (User observations, suggestions, or feedback during UAT)                                                                                                                                                  |
| **Executed By / Date**                                        | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                                                                 |
|                                                               |                                                                                                                                                                                                           |

|                                                                |                                                                                                                                                                                                                |
|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **UAT-PAT-SR-004 \| Access My Portal After Self-Registration** |                                                                                                                                                                                                                |
| **Role / Actor**                                               | Patient (Self-Registered)                                                                                                                                                                                      |
| **RTM Reference**                                              | O-01 → BR-PAT-09 → FR-PAT-07                                                                                                                                                                                   |
| **STC Reference**                                              | TC-PAT-SR-004                                                                                                                                                                                                  |
| **Priority**                                                   | Must Have                                                                                                                                                                                                      |
| **Business Scenario**                                          | As a newly self-registered patient, I want to see my Patient Portal and understand what I can access.                                                                                                          |
| **Given (Precondition)**                                       | I have just completed self-registration and been automatically logged in.                                                                                                                                      |
| **When (User Action)**                                         | I explore my Patient Portal home screen.                                                                                                                                                                       |
| **Then (Acceptance Criterion)**                                | I can see my Patient ID, My Appointments section (empty until Receptionist books one), and options to update my contact details and manage my consent. The portal feels clear and relevant to me as a patient. |
| **Fail Condition**                                             | I cannot see any other patient's information. I cannot access any clinical staff modules such as the Doctor Dashboard or Receptionist Desk.                                                                    |
| **Actual Result**                                              | (To be completed during execution)                                                                                                                                                                             |
| **Pass / Fail**                                                | ☐ Pass ☐ Fail                                                                                                                                                                                                  |
| **Defect ID**                                                  | (If failed — log in defect register)                                                                                                                                                                           |
| **Business Comments**                                          | (User observations, suggestions, or feedback during UAT)                                                                                                                                                       |
| **Executed By / Date**                                         | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ \_\_\_\_\_\_\_\_\_\_\_                                                                                                                                      |
|                                                                |                                                                                                                                                                                                                |

## 11. UAT Sign-Off
**11.1 UAT Execution Summary Dashboard**

*To be completed during execution phase.*

|                       |                   |
|-----------------------|-------------------|
| **Metric**            | **Value**         |
| Total UAT Scenarios   | 43                |
| Must Have Scenarios   | 29                |
| Should Have Scenarios | 14                |
| Passed                | (To be completed) |
| Failed                | (To be completed) |
| Blocked               | (To be completed) |
| Defects Logged        | (To be completed) |
| Critical Defects Open | (To be completed) |
| UAT Status            | Planned           |

**11.2 Sign-Off Criteria**

|                                                             |                     |            |
|-------------------------------------------------------------|---------------------|------------|
| **Criterion**                                               | **Threshold**       | **Status** |
| All Must Have UAT scenarios                                 | 100% Pass           | Pending    |
| Should Have UAT scenarios                                   | Minimum 80% Pass    | Pending    |
| Critical defects (RBAC failure, data loss, security breach) | Zero open           | Pending    |
| Sign-off from at least one rep per role group               | All 7 groups signed | Pending    |
| RTM updated: all UAT IDs status = Passed                    | RTM v1.1 updated    | Pending    |

**11.3 Role Representative Sign-Off**

|                           |                                        |                        |                                        |               |
|---------------------------|----------------------------------------|------------------------|----------------------------------------|---------------|
| **Role**                  | **Representative Name**                | **Sign-off Date**      | **Signature**                          | **Outcome**   |
| Receptionist              | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| Doctor                    | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| Clinician                 | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| Patient (Existing)        | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| Patient (Self-Registered) | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| System Administrator      | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| Dean / Admin              | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_ | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |
| BA (Prashant Gore)        | Prashant Gore                          | July 2026              | \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ | ☐ Pass ☐ Fail |

**END OF DOCUMENT**
