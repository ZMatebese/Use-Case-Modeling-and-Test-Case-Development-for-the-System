# Use Case Specifications
## RPL (Recognition of Prior Learning) Application System

**Author:** Boniface Kabaso
**Date:** March 2026
**Assignment:** Assignment 5

---

## Table of Contents

1. [UC1 – Register / Login](#uc1--register--login)
2. [UC2 – Submit RPL Application](#uc2--submit-rpl-application)
3. [UC3 – Upload Supporting Documents](#uc3--upload-supporting-documents)
4. [UC4 – Track Application Status](#uc4--track-application-status)
5. [UC6 – Review Application](#uc6--review-application)
6. [UC7 – Request Additional Information](#uc7--request-additional-information)
7. [UC8 – Approve / Reject Application](#uc8--approve--reject-application)
8. [UC14 – Prevent Duplicate Applications](#uc14--prevent-duplicate-applications)

---

## UC1 – Register / Login

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC1 |
| **Use Case Name** | Register / Login |
| **Actor(s)** | Student, Assessor, Registrar, Institution Administrator, IT Administrator, Helpdesk Staff |
| **Related Requirement** | FR-01 |
| **Description** | Allows all system users to create an account using their institutional email and securely log in to access role-appropriate features. |
| **Preconditions** | The user has a valid institutional email address. The system is online and accessible. |
| **Postconditions** | The user is authenticated and redirected to their role-specific dashboard. An audit log entry is created for the login event. |

**Basic Flow:**
1. User navigates to the RPL system login page.
2. New user selects "Register" and provides their institutional email, full name, and password.
3. System validates email format and password complexity (min 8 chars, uppercase, number, special character).
4. System sends a verification email to the provided address.
5. User clicks the verification link in the email.
6. Account is activated and the user is directed to log in.
7. User enters email and password on the login page.
8. System authenticates credentials and identifies the user's role.
9. System redirects the user to their role-specific dashboard.

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – Invalid email format** | At step 3, system displays an error: "Please enter a valid institutional email address." User must correct the email before proceeding. |
| **AF2 – Weak password** | At step 3, system highlights password field and displays requirements. User must update password before continuing. |
| **AF3 – Email already registered** | At step 3, system notifies user: "An account with this email already exists. Please log in or reset your password." |
| **AF4 – Incorrect login credentials** | At step 8, system displays: "Incorrect email or password." After 5 failed attempts, the account is temporarily locked and the user is emailed an unlock link. |
| **AF5 – Unverified email** | At step 8, system informs user their email is not verified and resends the verification link. |

---

## UC2 – Submit RPL Application

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC2 |
| **Use Case Name** | Submit RPL Application |
| **Actor(s)** | Student |
| **Related Requirement** | FR-02, FR-03 |
| **Description** | Allows a registered student to complete and submit an RPL application form for a specific module or qualification, including uploading supporting evidence. |
| **Preconditions** | Student is logged in. At least one module/qualification is available for RPL in the current academic period. |
| **Postconditions** | Application is saved in the database with status "Submitted." Student receives a confirmation email with a unique application reference number. Duplicate check has been completed. |

**Basic Flow:**
1. Student navigates to "New Application" from their dashboard.
2. System displays the RPL application form with available modules/qualifications.
3. Student selects the module/qualification they are applying for.
4. System performs a duplicate check (UC14) in the background.
5. If no duplicate is found, student completes all required fields: personal details, prior learning description, and institution where prior learning was gained.
6. Student uploads supporting documents (UC3).
7. Student reviews the completed form on a summary screen.
8. Student clicks "Submit Application."
9. System saves the application with status "Submitted" and generates a unique reference number.
10. System sends a confirmation email to the student.
11. Student is redirected to their dashboard where the new application is visible.

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – Duplicate application detected** | At step 4, system blocks submission and displays: "You already have an active application for this module. You cannot submit a duplicate application." Student is shown a link to their existing application. |
| **AF2 – Required fields missing** | At step 8, system highlights all empty required fields and displays: "Please complete all required fields before submitting." |
| **AF3 – No modules available** | At step 2, system displays: "No modules are currently open for RPL applications. Please check back later or contact the Registrar." |

---

## UC3 – Upload Supporting Documents

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC3 |
| **Use Case Name** | Upload Supporting Documents |
| **Actor(s)** | Student |
| **Related Requirement** | FR-02, FR-06 |
| **Description** | Allows a student to upload evidence documents (certificates, transcripts, portfolios) as part of their RPL application or in response to an assessor's request for additional information. |
| **Preconditions** | Student is logged in. An active application exists (either being created or in "Additional Information Required" status). |
| **Postconditions** | Uploaded documents are securely stored and linked to the student's application. Assessors can view the documents in the application review screen. |

**Basic Flow:**
1. Student accesses the document upload section (within the application form or from the application detail page).
2. System displays an upload area with accepted file types: PDF, DOCX, JPG, PNG (max 10MB per file).
3. Student selects one or more files from their device.
4. System validates file type and size.
5. System uploads and stores the file(s) securely, encrypted at rest.
6. System displays a list of successfully uploaded documents with file names and upload timestamps.
7. Student confirms the uploads and continues with the application.

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – Invalid file type** | At step 4, system rejects the file and displays: "File type not supported. Please upload PDF, DOCX, JPG, or PNG files only." |
| **AF2 – File exceeds size limit** | At step 4, system rejects the file and displays: "File size exceeds the 10MB limit. Please compress the file and try again." |
| **AF3 – Upload failure (network error)** | At step 5, system displays: "Upload failed. Please check your connection and try again." The student may retry without losing their form progress. |

---

## UC4 – Track Application Status

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC4 |
| **Use Case Name** | Track Application Status |
| **Actor(s)** | Student |
| **Related Requirement** | FR-04 |
| **Description** | Allows a student to view the current status and history of their RPL application(s) through their personal dashboard. |
| **Preconditions** | Student is logged in. At least one application has been submitted. |
| **Postconditions** | Student has viewed their current application status. No data is modified. |

**Basic Flow:**
1. Student logs in and is directed to their dashboard.
2. Dashboard displays a list of all submitted applications with their current status.
3. Student clicks on a specific application to view its details.
4. System displays: application reference number, module applied for, submission date, current status, and a status history timeline.
5. If the status is "Additional Information Required," a prompt and upload button are displayed.
6. Student can return to the dashboard at any time.

**Status values displayed:** Submitted → Under Review → Additional Information Required → Approved / Rejected

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – No applications submitted** | At step 2, dashboard displays: "You have not submitted any applications yet." with a link to start a new application. |
| **AF2 – Status not yet updated** | At step 4, if status has not changed since submission, system displays the last known status and the date it was last updated. |

---

## UC6 – Review Application

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC6 |
| **Use Case Name** | Review Application |
| **Actor(s)** | Academic Assessor |
| **Related Requirement** | FR-05 |
| **Description** | Allows an assessor to open an assigned RPL application, review the student's prior learning evidence and documentation, add assessment notes, and proceed to make a decision. |
| **Preconditions** | Assessor is logged in. At least one application is assigned to the assessor with status "Submitted" or "Under Review." |
| **Postconditions** | Application status is updated to "Under Review." Assessor's notes are saved. The assessor proceeds to UC8 (Approve/Reject) or UC7 (Request Additional Information). |

**Basic Flow:**
1. Assessor navigates to their "Application Queue" from their dashboard.
2. System displays a list of applications assigned to the assessor, ordered by submission date.
3. Assessor selects an application to review.
4. System updates the application status to "Under Review" and records the assessor's ID and timestamp.
5. Assessor reviews the student's personal details, prior learning description, and all uploaded documents.
6. Assessor adds assessment notes in the provided text field.
7. Assessor chooses one of three actions: Approve, Reject (UC8), or Request Additional Information (UC7).

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – No applications in queue** | At step 2, system displays: "You have no applications assigned for review at this time." |
| **AF2 – Assessor attempts to access unassigned application** | System blocks access and displays: "You are not authorised to review this application." The attempt is logged in the audit trail. |

---

## UC7 – Request Additional Information

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC7 |
| **Use Case Name** | Request Additional Information |
| **Actor(s)** | Academic Assessor |
| **Related Requirement** | FR-06 |
| **Description** | Allows an assessor to send a formal request to the student for additional supporting documents or clarification needed to complete the assessment. |
| **Preconditions** | Assessor is logged in and has an application open in review (UC6). |
| **Postconditions** | Application status changes to "Additional Information Required." Student receives an in-app and email notification with the assessor's request and a response deadline. |

**Basic Flow:**
1. During UC6, assessor selects "Request Additional Information."
2. System displays a text field for the assessor to describe what is needed.
3. Assessor enters the specific request (e.g., "Please upload a certified copy of your transcript from UCT").
4. System sets a response deadline based on the administrator-configured timeframe (default: 14 days).
5. Assessor submits the request.
6. System updates application status to "Additional Information Required."
7. System sends an email and in-app notification to the student with the assessor's message and deadline.
8. Request details and timestamp are logged in the audit trail.

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – Assessor submits empty request** | At step 5, system displays: "Please describe what additional information is required before submitting." |
| **AF2 – Student does not respond by deadline** | System automatically flags the application and notifies the assessor and registrar. The registrar can then decide to extend the deadline or close the application. |

---

## UC8 – Approve / Reject Application

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC8 |
| **Use Case Name** | Approve / Reject Application |
| **Actor(s)** | Academic Assessor |
| **Related Requirement** | FR-05 |
| **Description** | Allows an assessor to formally record and submit a final decision (Approved or Rejected) on an RPL application after completing their review. |
| **Preconditions** | Assessor is logged in and has completed reviewing the application (UC6). Application status is "Under Review." |
| **Postconditions** | Application status is updated to "Approved" or "Rejected." Student receives an email and in-app notification with the outcome. Decision is permanently recorded in the audit trail with assessor ID and timestamp. |

**Basic Flow:**
1. After completing review in UC6, assessor selects either "Approve" or "Reject."
2. System prompts the assessor to enter a mandatory decision rationale/comment.
3. Assessor enters the rationale and confirms the decision.
4. System updates the application status to "Approved" or "Rejected."
5. System timestamps the decision and links it to the assessor's account.
6. System sends the student an email and in-app notification with the outcome and the assessor's comment.
7. Decision is recorded in the audit log (UC12).

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – No rationale provided** | At step 3, system blocks submission and displays: "A decision rationale is required. Please provide a reason for your decision." |
| **AF2 – Assessor attempts to change decision after submission** | System does not allow modification of submitted decisions. The assessor must contact the Registrar to escalate a review. |

---

## UC14 – Prevent Duplicate Applications

| Field | Detail |
|-------|--------|
| **Use Case ID** | UC14 |
| **Use Case Name** | Prevent Duplicate Applications |
| **Actor(s)** | Student (triggered automatically during UC2) |
| **Related Requirement** | FR-03 |
| **Description** | The system automatically checks whether a student already has an active RPL application for the same module or qualification before allowing a new submission to proceed. |
| **Preconditions** | Student is logged in and has selected a module/qualification in the application form. |
| **Postconditions** | If no duplicate exists, submission proceeds normally. If a duplicate is detected, submission is blocked and the student is informed. |

**Basic Flow:**
1. Student selects a module/qualification during application submission (UC2, step 3).
2. System immediately queries the database for any active applications linked to the student's ID and the selected module.
3. No active application found — system proceeds with the submission form and allows the student to continue.

**Alternative Flows:**

| Scenario | Steps |
|----------|-------|
| **AF1 – Active duplicate found** | At step 2, system blocks submission and displays: "You already have an active application for [Module Name]. Duplicate applications are not permitted." Student is shown a link to their existing application. |
| **AF2 – Rejected application found (reapplication)** | At step 2, system checks the rejection date. If the configurable waiting period has passed, submission is allowed. If not, the system displays: "You may reapply for this module after [date]." |

---

*Document prepared for Assignment 5 — RPL Application System*
*Author: Boniface Kabaso | March 2026*
