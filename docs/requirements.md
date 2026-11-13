# Requirements
**Project:** AI Student Success and Dropout-Risk Support System (Group 02)

### 1. Problem Definition and Scope
This project aims to develop an AI-powered Student Success and Dropout-Risk Support System that analyzes student enrollment and academic information to estimate academic outcomes (Estimates are decision-support information and never an automatic decision about a student). The system provides a dashboard for authorized users to review students records, view predicted outcomes, understand contributing factors, and document appropriate support actions.
**In Scope:** dashboard, prediction service, explanations, follow-up workflow, reports, audit log,
**Out of Scope:** real student data, integration with a real university system, automatic decisions or notifications to students, production-grade security.

### 2. Stakeholders and actors
| Actor | Description |
|-------|--------|
|Advisor| Reviews students, requests predictions, records follow-up actions|
|Administrator| Manages users, views cohort reports, review audit log, exports data|
|Data/ ML Engineer (team)| Trains and evaluates the model, publishes model versions|
| Instructor (external) | Evaluates the project|

### 3. Data Source
- **Dataset:** UCI "Predict Students' Dropout and Academic Success" (4,424 records, 36 features).
- **Target:** Outcome with three classes: Dropout, Enrolled, Graduate.

### 4. Functional Requirements

### 5. Non-Functional Requirements
