# Test Case Document
## RPL (Recognition of Prior Learning) Application System

**Author:** Boniface Kabaso
**Date:** March 2026
**Assignment:** Assignment 5

---

## Functional Test Cases

| Test Case ID | Requirement ID | Use Case | Description | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|---|
| **TC001** | FR-01 | UC1 | Successful student registration with valid institutional email | 1. Navigate to registration page. 2. Enter valid institutional email, full name, and strong password. 3. Click "Register". 4. Open verification email and click the verification link. | Account is created, verified, and user is redirected to login page. Confirmation email received within 2 minutes. | — | — |
| **TC002** | FR-01 | UC1 | Login blocked after 5 failed attempts | 1. Navigate to login page. 2. Enter correct email but wrong password. 3. Repeat 5 times. | After the 5th failed attempt, account is temporarily locked. User receives an account unlock email. Error message displayed: "Too many failed attempts. Your account has been locked." | — | — |
| **TC003** | FR-02 | UC2 | Successful RPL application submission | 1. Log in as a student. 2. Click "New Application". 3. Select an available module. 4. Complete all required fields. 5. Upload a valid PDF document (< 10MB). 6. Click "Submit Application". | Application is saved with status "Submitted". Unique reference number is generated. Student receives a confirmation email within 2 minutes. Application appears on the student dashboard. | — | — |
| **TC004** | FR-03 | UC14 | Duplicate application submission is blocked | 1. Log in as a student who already has an active application for Module X. 2. Click "New Application". 3. Select Module X. | System detects the duplicate immediately. Submission form is blocked. Error message displayed: "You already have an active application for this module." Link to the existing application is shown. | — | — |
| **TC005** | FR-04 | UC4 | Student can view real-time application status | 1. Log in as a student with a submitted application. 2. Navigate to the dashboard. 3. Click on the application. 4. (Assessor separately updates status to "Under Review".) 5. Student refreshes dashboard. | Application status updates to "Under Review" within 60 seconds of the assessor's action. Status history timeline shows both "Submitted" and "Under Review" entries with timestamps. | — | — |
| **TC006** | FR-05 | UC6 | Assessor reviews an assigned application | 1. Log in as an assessor. 2. Navigate to "Application Queue". 3. Click on an assigned application. 4. Review documents and add assessment notes. 5. Click "Approve". 6. Enter a decision rationale. 7. Confirm decision. | Application status changes to "Approved". Student receives email and in-app notification. Decision is recorded with assessor ID, rationale, and timestamp in the audit log. | — | — |
| **TC007** | FR-06 | UC7 | Assessor requests additional information from student | 1. Log in as an assessor. 2. Open an application under review. 3. Select "Request Additional Information". 4. Enter the request details. 5. Submit the request. | Application status changes to "Additional Information Required". Student receives an email and in-app notification with the assessor's request and response deadline. Request is logged in the audit trail. | — | — |
| **TC008** | FR-08 | UC2, UC8 | Automated email notification sent on status change | 1. Log in as an assessor. 2. Open a student's application. 3. Change status to "Rejected" with a rationale. | Student receives an email notification within 2 minutes of the status change. Email contains the application reference number, new status ("Rejected"), and the assessor's rationale. | — | — |
| **TC009** | FR-11 | UC1 | Helpdesk staff cannot modify application data | 1. Log in as a Helpdesk staff member. 2. Search for a student's application by student ID. 3. View the application details. 4. Attempt to click "Approve", "Reject", or edit any field. | Application details are visible in read-only mode. No edit, approve, or reject buttons are accessible to the Helpdesk role. Any direct URL-based access attempt to restricted actions returns a 403 Forbidden error and is logged. | — | — |
| **TC010** | FR-10 | UC8 | Audit log records all application decisions | 1. Log in as an assessor. 2. Approve an application with a rationale. 3. Log in as Registrar. 4. Navigate to the Audit Log. 5. Search for the application by reference number. | Audit log entry exists for the approval action, recording: user ID (assessor), action ("Application Approved"), application reference number, and timestamp. Log entry cannot be edited or deleted. | — | — |
| **TC011** | FR-09 | — | Registrar generates an application statistics report | 1. Log in as a Registrar. 2. Navigate to the Reports dashboard. 3. Select report type: "Application Summary". 4. Set date range for current academic period. 5. Click "Generate". 6. Click "Export as CSV". | Report is generated displaying: total applications, approval rate, rejection rate, and average processing time. CSV file downloads successfully and contains the correct data. Report generates within 5 seconds. | — | — |
| **TC012** | FR-07 | — | Admin configures a new module for RPL | 1. Log in as Institution Administrator. 2. Navigate to "Workflow Configuration". 3. Click "Add Module". 4. Enter module name, code, and academic period. 5. Save. | New module is immediately available in the student application form without requiring a system restart. Configuration change is logged in the audit trail. | — | — |

---

## Non-Functional Test Cases

### Performance Test

| Test Case ID | Requirement ID | Description | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| **TC-NFR-P01** | NFR-P01 | System handles 1,000 concurrent users without performance degradation | 1. Use a load testing tool (e.g., Apache JMeter or k6). 2. Simulate 1,000 concurrent users simultaneously accessing the student dashboard and application form. 3. Run the test for 10 minutes. 4. Record response times and error rates. | All pages load within 2 seconds for all simulated users. Error rate remains below 1%. No server crashes or timeouts occur during the test period. | — | — |
| **TC-NFR-P02** | NFR-P02 | Document upload completes within 5 seconds for 10MB files | 1. Log in as a student. 2. Prepare a valid PDF file of exactly 10MB. 3. Upload the file in the document upload section. 4. Measure time from clicking "Upload" to receiving the success confirmation. | Upload completes and success message is displayed within 5 seconds on a standard broadband connection (≥10 Mbps). | — | — |

### Security Test

| Test Case ID | Requirement ID | Description | Test Steps | Expected Result | Actual Result | Status |
|---|---|---|---|---|---|---|
| **TC-NFR-SEC01** | NFR-SEC02 | All data in transit is encrypted via HTTPS/TLS | 1. Use a network inspection tool (e.g., Wireshark or browser developer tools). 2. Navigate to the RPL system and submit an application. 3. Inspect network traffic during login and form submission. | All traffic between client and server uses HTTPS with TLS 1.2 or higher. No sensitive data (passwords, personal details, documents) is transmitted in plaintext. HTTP requests are automatically redirected to HTTPS. | — | — |
| **TC-NFR-SEC02** | NFR-SEC03 | Unauthorised cross-role access is prevented | 1. Log in as a Student. 2. Manually enter the URL for the Assessor's application review page (e.g., `/assessor/review/APP001`). 3. Observe the system response. | System returns a 403 Forbidden error. The student is not able to view or interact with the assessor's review interface. The access attempt is recorded in the security audit log. | — | — |

---

## Test Coverage Summary

| Category | Test Cases | Requirements Covered |
|----------|-----------|---------------------|
| Functional – Authentication | TC001, TC002 | FR-01 |
| Functional – Application Submission | TC003 | FR-02 |
| Functional – Duplicate Prevention | TC004 | FR-03 |
| Functional – Status Tracking | TC005 | FR-04 |
| Functional – Assessor Review | TC006 | FR-05 |
| Functional – Additional Information | TC007 | FR-06 |
| Functional – Notifications | TC008 | FR-08 |
| Functional – Access Control | TC009 | FR-11 |
| Functional – Audit Trail | TC010 | FR-10 |
| Functional – Reporting | TC011 | FR-09 |
| Functional – Admin Config | TC012 | FR-07 |
| Non-Functional – Performance | TC-NFR-P01, TC-NFR-P02 | NFR-P01, NFR-P02 |
| Non-Functional – Security | TC-NFR-SEC01, TC-NFR-SEC02 | NFR-SEC02, NFR-SEC03 |

**Total Test Cases: 16** (12 functional + 4 non-functional)

---

*Document prepared for Assignment 5 — RPL Application System*
*Author: Boniface Kabaso | March 2026*
