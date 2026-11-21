# System Architecture

## 1. Purpose and scope

This document describes the proposed architecture for Group 02's AI Student Success and Dropout-Risk Support System. The system is a course prototype for authorized Advisors and Administrators to review **synthetic/demo student records**, request an estimated academic outcome, inspect explanatory information, record follow-up actions, and review reports.

The estimate has three possible classes: **Dropout, Enrolled, or Graduate**. It supports a human review only. It must not automatically determine a student's status, trigger an intervention, or send a notification to a student. The prototype does not use identifiable real-student data or connect to a university system.

The architecture diagrams show logical software parts. They do not require each part to run on a separate computer or service. For a course demonstration, the dashboard, API, and prediction code may run in one application process while keeping their responsibilities separate in the design.

## 2. Architecture at a glance

The design has two main areas:

1. **Model preparation (offline):** the Data/ML Engineer obtains the public UCI dataset, prepares features, trains and evaluates a model, and publishes an evaluated model file with version metadata. This happens during development/model updates, not for each student prediction.
2. **Application (runtime):** an Advisor or Administrator uses the dashboard. The dashboard sends requests to the API. The API reads or writes application data and calls the prediction service when an estimate is requested. The prediction service uses the published model file and returns an estimate and explanation data.

The UCI dataset is a model-development source, not an online dependency of the running dashboard. The raw dataset must not be committed to this repository.

## 3. Components and proposed technologies

| Component | Responsibility | Proposed technology |
|---|---|---|
| Web dashboard (frontend) | Presents student lists/details, estimates, explanations, cohort reports, model limitations, and the decision-support notice. Collects Advisor and Administrator actions. | Streamlit with Python |
| Application API (backend) | Accepts dashboard requests, validates input, applies the prototype's role checks, coordinates database access and prediction requests, and returns results. | FastAPI with Python; HTTP/JSON |
| Prediction service | Prepares validated model features, loads the selected evaluated model, predicts one of the three outcome classes, and returns explanation information. | Python and scikit-learn; joblib for model serialization |
| Application database | Stores synthetic/demo records, demo user/role information, prediction history, follow-up actions, and audit events. | SQLite for a local demonstration; PostgreSQL could be considered if the deployment needs a shared hosted database. |
| Model artifact store | Holds the evaluated model file and metadata such as its version and evaluation summary. | Versioned joblib files in the project workspace or a release artifact. |
| Model preparation | Downloads/reads the UCI *Predict Students' Dropout and Academic Success* dataset, prepares training data, trains and evaluates candidates, and publishes an approved artifact. | UCI dataset, Python, pandas, scikit-learn, and joblib |

These are **proposed technologies**, not a record that the team has already implemented or finalized this stack. The team should confirm the choices before implementation. The current practical proposal is Streamlit, FastAPI, SQLite, scikit-learn, and joblib. If the course implementation uses a different technology, update this table and the diagrams together.

## 4. Component details

### 4.1 Web dashboard

The dashboard is the user-facing part of the application. Advisors use it to find and review synthetic records, request an estimate, read explanation information, and record or track a follow-up action. Administrators use it to review cohort reports, demo access, and audit history. It presents a visible note that estimates are decision-support information and must be reviewed by a person.

### 4.2 Application API

The API is the dashboard's application-facing backend. It is responsible for validating requests, checking the prototype's user role, coordinating reads and writes, and calling the prediction service. Keeping this logic behind an API avoids making the dashboard responsible for directly manipulating database records or loading the model.

Role checks in this course prototype are not a substitute for production authentication or authorization. The project scope excludes production-grade security.

### 4.3 Application database

The database stores application state, separate from the model-training dataset. Its planned records include:

- synthetic student profiles and their enrollment/academic input fields;
- demo users and roles needed by the prototype;
- prediction results, including the class, explanation data, timestamp, and model version;
- follow-up actions recorded by an Advisor, with notes and status changes kept as append-only history entries; and
- audit events for relevant actions and report/export activity.

SQLite is proposed because it is simple for a local course demo. PostgreSQL is an alternative if the team later needs a shared database for a hosted, multi-user demo. The database choice should be reflected in the implementation and deployment notes.

### 4.4 Prediction service and model artifact

The prediction service receives validated feature values from the API, applies the same feature preparation used for model training, loads the selected model artifact, and returns a predicted class and explanation information. It should report errors for invalid or incomplete input rather than presenting an untrustworthy estimate.

Each saved prediction should retain the model version used so that the result can be traced to the model that produced it. The artifact metadata should identify at least the model version and its evaluation information. The model file is an application dependency; it is distinct from the application database.

The prediction record keeps the original predicted outcome if an Advisor overrides or dismisses it. An override stores the replacement outcome and reason; the action is also recorded in the audit history. Follow-up notes are stored as history entries so later notes do not replace earlier ones. Model information includes intended use, limitations, macro-F1, per-class recall, a confusion matrix, and the global feature summary required for review.

The precise explanation method depends on the model selected and should be documented with the model evaluation. The architecture requires the service to return explanation information but does not prescribe an explanation algorithm.

### 4.5 Model preparation and public data

The Data/ML Engineer uses the public UCI dataset to prepare features and train/evaluate a candidate model. Only an evaluated, versioned model artifact and necessary metadata are made available to the running application. The application does not download training data from UCI for each request. Keep the raw dataset out of Git; follow the repository's data instructions for obtaining it locally.

## 5. Communication and data flow

### 5.1 Requesting an estimate

1. An Advisor opens a synthetic/demo student record in the dashboard.
2. The dashboard sends an HTTP request with JSON data to the Application API.
3. The API checks the request and the demo role, then sends validated model inputs to the Prediction Service over an internal application call/API.
4. The Prediction Service prepares the features, loads the versioned model artifact, and returns the estimated outcome, explanation information, and model version.
5. The API saves the prediction and model version in the Application Database, then returns the result to the dashboard.
6. The dashboard displays the result and the decision-support notice. The Advisor interprets it and decides whether to record a follow-up action.

### 5.2 Other application actions

- Student-record views, follow-up actions, report queries, and audit-history queries flow from the dashboard through the API to the Application Database.
- Saving a follow-up action writes the action and a corresponding audit event. The system records what the Advisor chose to do; it does not automatically initiate that action.
- Administrators request reports and audit information through the dashboard and API. Export/report data is limited to the synthetic/demo project data.

### 5.3 Publishing a model

1. The Data/ML Engineer obtains the UCI dataset for model development.
2. The Engineer prepares data, trains/evaluates a model, and records evaluation details.
3. The Engineer publishes an approved, versioned model artifact and its metadata to the Model Artifact Store.
4. The Prediction Service loads the selected artifact for inference. Model training and UCI access are not part of the normal prediction request path.

## 6. Architecture diagrams

- [C4 Level 1 — System Context](../uml/c4_context.drawio) shows the system, its user roles, and its relationship to the public UCI dataset.
- [C4 Level 2 — Containers](../uml/c4_container.drawio) shows the dashboard, API, prediction service, application database, model artifact store, and their communication paths.

Open either `.drawio` file with [diagrams.net](https://app.diagrams.net/) to view or edit it. In C4, a **container** is a major application or data store; it does not necessarily mean a Docker container. The diagrams show logical boundaries, not a requirement to deploy each box as a separate server.

## 7. Key design decisions and assumptions

| Topic | Current proposal / assumption |
|---|---|
| User identities | Synthetic/demo identities only; no live university integration. |
| Runtime dataset | Application records are in the Application Database. UCI is for offline model development. |
| Prediction output | Dropout, Enrolled, or Graduate, with explanatory information and the model version. |
| Human oversight | Estimates inform authorized staff; they do not automatically decide outcomes or trigger interventions/notifications. |
| Deployment | Logical components may run together for the local course demo. |
| Technology status | Streamlit, FastAPI, SQLite, scikit-learn, and joblib are proposals pending team confirmation. |
| Security scope | Demo role checks may support the prototype; production-grade security is outside the course scope. |

## 8. Quality and safety considerations

- Validate required fields and input ranges before requesting a prediction; show a clear error for invalid or incomplete input.
- Keep prediction results traceable by recording the model version and relevant timestamp.
- Make the decision-support limitation visible wherever prediction results are shown.
- Use synthetic/demo student data in development, reports, screenshots, and exports.
- Document model evaluation, limitations, and the explanation method in the model/report materials.
- Do not commit the raw UCI dataset or model artifacts unless the repository's data and release instructions explicitly call for a small approved artifact.
