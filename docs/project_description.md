# Project Description

**Project:** AI Student Success and Dropout-Risk Support System 
**Group:** 02
**Course:** Software Engineering (CS13477), Fall 2026
**Instructor:** Dr. Samer El Kababji

## 1. Overview

This project designs, builds, tests, and demonstrates a decision-support system that estimates a student's academic outcome (Dropout, Enrolled, or Graduated) from enrollment and academic variables. The system is delivered as a web dashboard used by academic advisors and administrators.

The estimates are decision-support information only. The system never makes, triggers, or communicates a decision about a student. A human advisor reviews every estimate and decides what, if anything, to do.

The project follows the course process: requirements, case-specific incremental plan, architecture and UML, implementation through an Agentic AI coding workflow, student review, testing, and versioned releases in GitHub.

## 2. Problem Statement

Universities hold large amounts of enrollment and academic data, but advisors usually cannot review every student closely enough to notice who may need support early. Students at risk of dropping out are often identified late, after the chance for effective help has passed.

A model trained on historical data can highlight students whose profiles resemble those who previously dropped out. However, an unexplained score used carelessly can mislead advisors, reinforce bias, or be mistaken for a decision. The problem is therefore not only to predict an outcome, but to present it **carefully, with explanations, human oversight, and a record of the support actions taken**.

## 3. Objectives

1. Provide a dashboard where authorized users can browse, search, and filter synthetic student records.
2. Provide model-based outcome estimates with class probabilities, model version, and a visible decision-support disclaimer.
3. Explain each estimate by showing the main contributing factors, and summarize the features that matter most to the model overall.
4. Let advisors record and track follow-up support actions through a defined workflow, and override or dismiss an estimate with a reason.
5. Give administrators cohort reports, CSV export, user management, and an audit log.
6. Make the model's limitations visible to users.
7. Demonstrate disciplined software engineering: traceability from requirements to design, code, and tests, with the work built through reviewable, tagged increments.

## 4. Stakeholders and Users

| Stakeholder | Interest |
|---|---|
| Advisor | Identifies students who may need support, reviews estimates and explanations, records follow-up actions |
| Administrator | Monitors cohorts, exports reports, manages users, reviews the audit log |
| Project team (Data/ML Engineer role) | Trains, evaluates, and publishes model versions |
| Instructor | Evaluates the engineering process and each student's understanding |
| Students (indirect) | Affected by how estimates are used; protected by the human-review and privacy rules |

## 5. Scope

**In scope**
- Web dashboard with sign-in and two roles (Advisor, Administrator)
- Student list, search, filters, profile, and summary analytics using synthetic identities
- Training pipeline, evaluation, and a prediction service using the UCI dataset
- Per-student explanations and a global feature summary
- Follow-up workflow with statuses, notes, and assignee
- Override or dismissal of an estimate with a reason
- Audit log, cohort reports, CSV export, user management, and model limitations page

**Out of scope**
- Real student data or integration with a real university system
- Automatic decisions, interventions, or notifications to students
- Production-grade security, hosting, or scalability
- Physical hardware or external paid services

## 6. Data Source

| Item | Details |
|---|---|
| Dataset | UCI *Predict Students' Dropout and Academic Success* |
| Link | https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success |
| Size | 4,424 records, 36 features |
| Origin | Higher-education institution data (confirm the exact source and citation on the dataset page) |
| Target | Outcome: Dropout, Enrolled, Graduate |
| License | *To be confirmed from the dataset page and recorded in `docs/requirements.md`* |
| Handling | The raw dataset is not committed to the repository. A download script or instructions and, if useful, a small sample are stored instead. |

All student identities shown in the system (IDs and names) are **synthetic** and are generated and attached to dataset rows by the loading script. The dataset contains sensitive attributes (such as gender, nationality, marital status, and age at enrollment); how the team handles them will be documented in the ML documentation.

## 7. System Description

The system has two main areas:

1. **Model preparation (offline):** the team obtains the dataset, prepares features, trains and evaluates models, and publishes a versioned model file.
2. **Application (runtime):** advisors and administrators use the dashboard, which calls a backend API. The API reads and writes application data and calls the prediction service, which uses the published model and returns an estimate and explanation data.

Detailed components, communication, and diagrams are in `docs/architecture.md` and `/uml/`.

### Main workflows

1. **Review a student:** sign in, search or filter, open the student profile.
2. **Request an estimate:** an advisor requests an estimate, sees the outcome, probabilities, model version, disclaimer, and contributing factors.
3. **Support a student:** the advisor records a follow-up action, updates its status (Open, In progress, Resolved, Closed), or overrides the estimate with a reason.
4. **Monitor and report:** an administrator reviews cohort reports, exports data, manages users, and checks the audit log.

## 8. Proposed Technology

| Area | Proposed choice |
|---|---|
| Language | Python |
| Dashboard | streamlit with python  |
| Backend API |  FastAPI(HTTP/JSON) |
| Database | SQLite |
| Machine learning |  scikit-learn |
| Testing |  pytest |
| Diagrams | draw.io and PlantUML |
| Version control | GitHub with feature branches, pull requests, and tags |
| Implementation | Agentic AI coding tool |

## 10. Deliverables

- GitHub repository with full history, branches, pull requests, and tags
- Requirements, architecture, and UML/C4 diagrams (editable sources and rendered images)
- Incremental development plan, AI development log, prompt records, and traceability matrix
- Working dashboard, with automated tests and validation evidence
- Final report (`se_report_group_02.pdf`) with the README as its first page
- Two online oral examinations (first: Weeks 8 and 9; final: Weeks 14 and 15)
