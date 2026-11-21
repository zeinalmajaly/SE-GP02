# Requirements
**Project:** AI Student Success and Dropout-Risk Support System (Group 02)

## 1. Problem Definition and Scope
This project aims to develop an AI-powered Student Success and Dropout-Risk Support System that analyzes student enrollment and academic information to estimate academic outcomes (Estimates are decision-support information and never an automatic decision about a student). The system provides a dashboard for authorized users to review students records, view predicted outcomes, understand contributing factors, and document appropriate support actions.
**In Scope:** dashboard, prediction service, explanations, follow-up workflow, reports, audit log,
**Out of Scope:** real student data, integration with a real university system, automatic decisions or notifications to students, production-grade security.

## 2. Stakeholders and actors
| Actor | Description |
|-------|--------|
|Advisor| Reviews students, requests predictions, records follow-up actions|
|Administrator| Manages users, views cohort reports, review audit log, exports data|
|Data/ ML Engineer (team)| Trains and evaluates the model, publishes model versions|
| Instructor (external) | Evaluates the project|

## 3. Data Source
- **Dataset:** UCI "Predict Students' Dropout and Academic Success" (4,424 records, 36 features).
- **Target:** Outcome with three classes: Dropout, Enrolled, Graduate.
- **License**: (CC BY 4.0) license
## 4. Role Permissions
|Function|Advisor|Administrator|
|--|--|--|
|Sign-in/ Sign out| Yes| Yes|
| View, search, and filter student records | Yes | Yes (read-only) |
| View dashboard analytics | Yes | Yes |
| Request an outcome estimate | Yes | No |
| View prediction history and explanations | Yes | Yes (read-only) |
| Override or dismiss an estimate | Yes | No |
| Create and update follow-up actions | Yes | No |
| View follow-up history | Yes | Yes (read-only) |
| View cohort reports | No | Yes |
| Export report data | No | Yes |
| Manage user accounts and roles | No | Yes |
| View audit log | No | Yes |
| View model limitations page | Yes | Yes |

## 5. Functional Requirements

### 5.1 Access, Data, and Records
| ID | Requirement | Description | 
|---|---|---|
| FR-01 | User sign-in | The system shall require a user to sign in with credentials before accessing student records, predictions, follow-up actions, or reports. |
| FR-02 | Role-based access | The system shall provide the roles Advisor and Administrator and restrict functions as defined in the role permissions table. | 
| FR-03 | Sign-out | The system shall allow a signed-in user to sign out and end the session. |
| FR-04 | Documented dataset and synthetic identities | The system shall provide a documented script that loads the UCI dataset into the database and assigns each record a synthetic student ID and name. | 
| FR-05 | Student list | The system shall display a paginated list of student records. | 
| FR-06 | Search students | The system shall allow a user to search students by student ID or name. | 
| FR-07 | Filter students | The system shall allow a user to filter students by course, enrollment attributes, and outcome. The latest predicted outcome shall be added as a filter once predictions exist. | 
| FR-08 | Student profile | The system shall display a selected student's enrollment, academic, and demographic information. | 
| FR-09 | Dashboard analytics | The system shall display summary statistics and charts of student outcomes (and risk levels once predictions exist). | 
| FR-10 | Input validation | The system shall validate user input and reject invalid or incomplete data with a clear message. |
### 5.2 Prediction Service

| ID | Requirement | Description |
|---|---|---|
| FR-11 | Train and evaluate model | The system shall provide a reproducible way for the project team to train and evaluate a model on the UCI dataset, reporting at least macro-F1, per-class recall, and a confusion matrix. | 
| FR-12 | Publish model version | The system shall allow the team to publish a versioned model file for use by the prediction service. |
| FR-13 | Request estimate | The system shall allow an Advisor to request an outcome estimate for an individual student using the published model. |
| FR-14 | Display estimate | The system shall present the estimate as one of Dropout, Enrolled, or Graduate. | 
| FR-15 | Display probabilities | The system shall display the probability of each outcome class alongside the estimate. | 
| FR-16 | Display model version | The system shall display the model version and the time of generation with every estimate. |
| FR-17 | Decision-support disclaimer | The system shall label every displayed estimate as decision-support information and state that it is not an automatic decision about the student. | 
| FR-18 | Prediction history | The system shall store each generated estimate and display the previous estimates for a student. |
| FR-19 | Override or dismiss estimate | The system shall allow an Advisor to override or dismiss an estimate by giving a reason, and shall keep the original estimate on record. |

### 5.3 Explanations

| ID | Requirement | Description | 
|---|---|---|
| FR-20 | Individual explanation | The system shall show the main factors contributing to an individual estimate, using the explanation method documented in the architecture. | 
| FR-21 | Global feature summary | The system shall provide a summary of the features that are most important to the model overall. |

### 5.4 Follow-up Workflow

| ID | Requirement | Description | 
|---|---|---|
| FR-22 | Record follow-up action | The system shall allow an Advisor to record a follow-up action for a student with action type, note, assignee, date, and initial status Open, optionally linked to a prediction. | 
| FR-23 | Update follow-up | The system shall allow an Advisor to add notes and change the status of a follow-up through Open, In progress, Resolved, and Closed, and shall reject invalid transitions. | 
| FR-24 | View follow-up history | The system shall allow authorized users to view a student's follow-up actions and their current status and history. | 

### 5.5 Administration, Reporting, and Responsible AI

| ID | Requirement | Description |
|---|---|---|
| FR-25 | Audit recording | The system shall record an audit entry (action, actor, time) for prediction requests, estimate overrides, follow-up changes, report exports, and user-management changes. |
| FR-26 | View audit log | The system shall allow an Administrator to view the audit log. |
| FR-27 | Cohort reports | The system shall allow an Administrator to view cohort-level summaries of predicted outcomes, filterable by course and risk level. |
| FR-28 | Export reports | The system shall allow an Administrator to export permitted report data as CSV. |
| FR-29 | Manage user accounts | The system shall allow an Administrator to create, deactivate, and assign roles to user accounts. | 
| FR-30 | Model limitations page | The system shall provide a page describing intended use, model performance, known limitations, and the decision-support disclaimer. | 



## 6. Non-Functional Requirements

| ID | Category | Requirement | 
|---|---|---|
| NFR-01 | Usability | The dashboard shall use consistent labels and navigation for records, predictions, explanations, follow-ups, reports, and model limitations, so an Advisor can reach any of them within three clicks of the home page. | 
| NFR-02 | Performance | Under the documented demonstration setup, student search, record view, and dashboard pages shall load within 3 seconds. | 
| NFR-03 | Prediction response time | Under the documented demonstration setup, a valid prediction request shall complete within 5 seconds, excluding initial startup and model loading. |
| NFR-04 | Reliability | If a prediction cannot be generated because of invalid input or an unavailable model, the system shall show an understandable error and shall not present a fabricated or stale estimate as a new result. The system shall not crash on invalid input. | 
| NFR-05 | Data integrity | Data stored by the system (predictions, follow-ups, users, audit entries) shall persist across application restarts. | 
| NFR-06 | Privacy | The dashboard, exports, and repository shall contain only synthetic identities and shall not require real student personal data. | 
| NFR-07 | Security | Protected functions shall be available only to signed-in users, role-based authorization shall be enforced on the server side, and passwords shall be stored hashed. | 
| NFR-08 | Auditability | Audit entries shall be timestamped and attributable to a user, and shall not be modifiable or deletable through the application. | 
| NFR-09 | Explainability | Explanations shall use language understandable to an Advisor and shall not imply that contributing factors establish causation. | 
| NFR-10 | Responsible use | The system shall not automate student decisions, interventions, or notifications. Sensitive attributes (gender, nationality, marital status, age at enrollment) shall be identified in the ML documentation together with how the team handles them. | 
| NFR-11 | Maintainability | Data access, model training and evaluation, prediction logic, and the user interface shall be organized as separable modules documented in `docs/architecture.md`. |
| NFR-12 | Reproducibility | Dataset source, preprocessing, evaluation process, and random seed shall be documented, and the model version used for every estimate shall be recorded, so that results can be repeated. |
| NFR-13 | Compatibility | The dashboard shall work on current desktop versions of Chrome, Edge, and Firefox. | 
| NFR-14 | Accessibility | The primary workflows shall use readable text, meaningful labels, and keyboard-operable controls. |
| NFR-15 | Scalability | The design shall allow more student records and users to be added without major architectural change. | 
| NFR-16 | Testability | Every working increment shall include automated tests that pass before the pull request is merged. 
| NFR-17 | Portability | The system shall run from documented, reproducible instructions on a clean machine. | 
