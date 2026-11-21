# Incremental Development Plan

## Versioning convention

Versions follow `vMAJOR.MINOR.PATCH`.

| Suffix / form | Meaning |
|---|---|
| `v0.x.0-design` | Design checkpoint: specification, diagrams, and prompt plan for the increment, reviewed and merged. No new application code. |
| `v0.2.0-model` | Descriptive suffix for this project's ML-heavy increment: the trained, evaluated model and its documentation, before the prediction API and screens are built on it. Used once. |
| `v0.x.0` | Working increment: implemented through the Agentic AI workflow, reviewed, tested, merged, and tagged. |
| `v0.x.y` (y > 0) | Patch: a bug fix that adds no feature. |
| `v1.0.0` | Final integrated release. |

**Git rule (every row):** work on `feature/...`, `docs/...`, or `test/...` branches, open a pull request, have another member review and merge it into `dev`, merge `dev` into `main`, and **tag the merged commit**. Never delete branches.

## Plan table

| Version | Type | Capability / Scope | Deliverable / Evidence | Requirements / Design Links |
|---|---|---|---|---|
| v0.1.0-design | Design | Context, containers, roles, data model, use cases | C4 L1/L2, use cases, sequence, activity, class, ERD; prompt records | FR-01..FR-10, FR-25; [uml/](../uml/), [use_cases.md](use_cases.md) |
| v0.1.0 | Working | Data loading, synthetic identities, sign-in and roles, student list, search, filter, profile, dashboard charts | Code, unit and API tests, demo | FR-01..FR-10; `src/scripts`, `src/db`, `src/api`, `src/dashboard`; `tests/` |
| v0.2.0-design | Design | ML pipeline and prediction service | ML documentation, component and sequence updates, ERD update | FR-11..FR-18, NFR-10, NFR-12; `ml_documentation.md`, `uml/` |
| v0.2.0-model | Working | Training, evaluation, versioned model file and metadata | Model files, evaluation report, unit and component tests | FR-11, FR-12, NFR-10, NFR-12; `src/ml`, `models/`; `tests/` |
| v0.2.0 | Working | Prediction API, estimate display, probabilities, model version, disclaimer, history, audit foundation | Code, integration tests, demo | FR-13..FR-18, FR-25 (start), NFR-03, NFR-04; `src/api`, `src/dashboard`; `tests/` |
| v0.3.0-design | Design | Explanation module | Sequence and class updates, method choice | FR-20, FR-21, NFR-09; `uml/` |
| v0.3.0 | Working | Per-student contributing factors, global feature summary | Code, tests, demo | FR-20, FR-21, NFR-09; `src/ml/explain.py`; `tests/` |
| v0.4.0-design | Design | Follow-up workflow and estimate override | State diagram, activity update, ERD update | FR-19, FR-22..FR-24; `uml/` |
| v0.4.0 | Working | Follow-up actions, notes, status workflow, override or dismiss, audit of changes | Code, workflow and database tests, demo | FR-19, FR-22..FR-25; `src/api`, `src/db`; `tests/` |
| v0.5.0-design | Design | Reports, export, user management, limitations page | Report mock-ups, DFD, deployment view | FR-25..FR-30; `uml/` |
| v0.5.0 | Working | Cohort reports, CSV export, user accounts, audit log view, limitations page | Code, tests, demo | FR-25..FR-30; `src/api`, `src/dashboard`; `tests/` |
| v1.0.0 | Final | Integrated, documented release | Final diagrams, end-to-end tests, run instructions, report | All FR and NFR; full traceability matrix |

## Increment details

### v0.1.0-design: Context, containers, roles, data model, use cases

- **Main question:** Do we have a reviewed design of who uses the system, what the containers are, and what data is stored, before any code is written?
- **Tools:** draw.io, PlantUML, the coding agent for drafting (prompts recorded).
- **Deliverables:** `uml/c4_context.drawio`, `uml/c4_container.drawio`, `uml/use_case.puml`, `uml/sequence_diagram.puml`, `uml/activity_diagram.puml`, `uml/class_diagram.drawio`, `uml/erd.drawio`, `docs/use_cases.md`, `docs/architecture.md`, `prompts/v0.1.0-design-*.md`.
- **Acceptance criteria:**
  - Class diagram and ERD show **multiplicities** on every association, and the enumerations are defined.
  - Prediction stores the **overridden outcome** (FR-19), notes can be kept without overwriting (FR-23), and the model's confusion matrix has a field (FR-11).
  - Use case diagram includes the Data/ML Engineer (development-time) with the load-dataset and train-and-publish use cases, or `use_cases.md` states why not.
  - Sequence diagram saves the model version with each prediction (FR-16).
  - `traceability_matrix.md` links FR-01 to FR-30 to design elements.
  - Prompt records and AI log rows exist, with a reviewer other than the prompt author.
  - Pull request reviewed and merged, and `v0.1.0-design` is tagged on the merged commit.

### v0.1.0: Data, identities, sign-in, records, dashboard basics

- **Main question:** Can an authorized user sign in and browse synthetic student records?
- **Tools:** Coding agent, Python, SQLite, FastAPI, Streamlit, pytest.
- **Deliverables:** database schema creation, `src/scripts/load_dataset.py`, authentication and role checks, student list, search, filter, profile, summary charts, `prompts/v0.1.0-*.md`.
- **Acceptance criteria:**
  - The loading script reads the UCI CSV and creates one student record per row with a synthetic ID and name (FR-04). The raw dataset is not committed.
  - Sign-in, sign-out, and role-based access work, and passwords are stored hashed (FR-01 to FR-03, NFR-07).
  - List is paginated, search works by ID and name, and filters work (FR-05 to FR-07).
  - Profile shows enrollment, academic, and demographic fields (FR-08). Dashboard shows outcome distribution (FR-09).
  - Invalid input is rejected with a clear message (FR-10).
  - Unit tests (validation, password hashing, loader) and API tests (access control) pass.
  - Pages load within 3 seconds in the demo setup (NFR-02).

### v0.2.0-design: ML pipeline and prediction service

- **Main question:** How is the model built, evaluated, stored, and called, and what must be documented about the data and its risks?
- **Tools:** draw.io or PlantUML, `docs/ml_documentation.md`.
- **Deliverables:** `docs/ml_documentation.md` (dataset and license, target, preprocessing, split and validation strategy, metrics, how predictions are exposed, handling of sensitive attributes), updated component and sequence diagrams, ERD update (model version metadata).
- **Acceptance criteria:**
  - ML documentation covers every item in Section 5.5 of the course instructions.
  - Documented choice of baseline and stronger model, stratified split, random seed, and metrics (macro-F1, per-class recall, confusion matrix).
  - Handling of sensitive attributes (gender, nationality, marital status, age at enrollment) is stated.
  - Diagrams show where the model is loaded and how failures are reported (NFR-04).

### v0.2.0-model: Trained and evaluated model

- **Main question:** Does a reproducible pipeline produce a model whose weaknesses we understand?
- **Tools:** coding agent, scikit-learn, joblib, pytest.
- **Deliverables:** `src/ml/preprocessing.py`, `train.py`, `evaluate.py`, versioned model file and metadata in `models/`, evaluation report (in `docs/ml_documentation.md` or `docs/model_evaluation.md`), `prompts/v0.2.0-model-*.md`.
- **Acceptance criteria:**
  - One command trains and evaluates the models with a fixed seed, and reruns give the same metrics (NFR-12).
  - Baseline and stronger model are compared, with macro-F1, per-class recall (especially Dropout), and the confusion matrix reported (FR-11).
  - The published model has a version ID and stored evaluation metadata (FR-12).
  - Unit tests (preprocessing) and component tests (model loading, prediction output shape and probability sum) pass.

### v0.2.0: Prediction API, estimate display, audit foundation

- **Main question:** Can an advisor request an estimate and see a result that is clearly labelled and traceable to a model version?
- **Tools:** coding agent, FastAPI, Streamlit, pytest.
- **Deliverables:** prediction endpoint and service, estimate screen, prediction history, audit log table and writer, `prompts/v0.2.0-*.md`.
- **Acceptance criteria:**
  - Advisor can request an estimate and see the outcome, all class probabilities, model version, generation time, and the decision-support disclaimer on every estimate (FR-13 to FR-17).
  - Each estimate is stored and shown in the student's prediction history (FR-18).
  - Prediction requests write an audit entry with actor, action, and time (FR-25, NFR-08).
  - If input is invalid or the model is unavailable, the user sees a clear error and no estimate is stored or shown as new (NFR-04).
  - A prediction completes within 5 seconds in the demo setup (NFR-03).
  - Integration tests (API with database and model) and a system test of the main scenario pass.

### v0.3.0-design: Explanation module

- **Main question:** Where does explanation logic live, and how is it worded so it is not read as causation?
- **Tools:** draw.io or PlantUML.
- **Deliverables:** updated sequence and class diagrams, chosen explanation method (SHAP or feature importance) and its justification in `ml_documentation.md`.
- **Acceptance criteria:** the explanation call is in the sequence diagram, the explainer class and its relation to the model are in the class diagram, and the wording rule from NFR-09 is stated.

### v0.3.0: Contributing factors and global summary

- **Main question:** Can an advisor see why the model produced an estimate?
- **Tools:** coding agent, SHAP or scikit-learn, pytest.
- **Deliverables:** `src/ml/explain.py`, factors on the student estimate screen, global feature summary page, `prompts/v0.3.0-*.md`.
- **Acceptance criteria:**
  - Each estimate shows its main contributing factors in plain language (FR-20, NFR-09).
  - A global summary of the most important features is available (FR-21).
  - Explanation output is consistent with the prediction it accompanies (tested).
  - The wording does not claim that a factor causes the outcome.

### v0.4.0-design: Follow-up workflow and override

- **Main question:** What states can a follow-up have, and how does an advisor override an estimate while keeping the original?
- **Tools:** draw.io or PlantUML.
- **Deliverables:** state diagram (Open, In progress, Resolved, Closed), updated activity diagram, ERD and class updates if needed.
- **Acceptance criteria:** allowed and rejected transitions are shown, override and dismissal flow is shown, and the original estimate stays on record.

### v0.4.0: Follow-ups, notes, override, audit of changes

- **Main question:** Can advisors record and track support actions and record human decisions about estimates?
- **Tools:** coding agent, FastAPI, SQLite, pytest.
- **Deliverables:** follow-up create, update, and view; status history; override and dismiss with reason; audit entries; `prompts/v0.4.0-*.md`.
- **Acceptance criteria:**
  - Advisor creates a follow-up with type, note, assignee, and date, starting as Open, optionally linked to a prediction (FR-22).
  - Notes and status changes follow the allowed transitions, invalid transitions are rejected, and history is kept (FR-23, FR-24).
  - Override or dismissal requires a reason and keeps the original estimate (FR-19).
  - Follow-up and override changes write audit entries (FR-25).
  - Workflow tests (every valid and invalid transition) and database tests pass.

### v0.5.0-design: Reports, export, user management, limitations

- **Main question:** What aggregate views and transparency features do administrators need?
- **Tools:** draw.io, PlantUML, mock-ups.
- **Deliverables:** report mock-ups, DFD from dataset to prediction to report, deployment view, updated use cases if needed.
- **Acceptance criteria:** mock-ups cover cohort report, export, user management, audit view, and limitations page, and the DFD shows no path where an estimate triggers an action automatically.

### v0.5.0: Reports, export, accounts, audit view, limitations page

- **Main question:** Can an administrator monitor cohorts and understand the model's limits?
- **Tools:** coding agent, FastAPI, Streamlit, pytest.
- **Deliverables:** cohort report with filters, CSV export, user account management, audit log view, model limitations page, `prompts/v0.5.0-*.md`.
- **Acceptance criteria:**
  - Cohort report filters by course and risk level (FR-27). CSV export contains only synthetic identities (FR-28, NFR-06).
  - Administrator can create, deactivate, and assign roles (FR-29), and these changes are audited.
  - Administrator can view the audit log, and entries cannot be edited or deleted through the application (FR-26, NFR-08).
  - Limitations page shows intended use, performance, known limitations, and the disclaimer (FR-30).
  - Advisors cannot reach administrator functions (tested).

### v1.0.0: Final integrated release

- **Main question:** Does the whole system work end to end, and do the documents describe what was actually built?
- **Tools:** pytest, Pandoc (or another converter) for the PDF report.
- **Deliverables:** final diagrams and rendered images, complete `testing.md`, `ai_development_log.md`, and `traceability_matrix.md`, run instructions, `report.md`, `se_report_group_02.pdf`.
- **Acceptance criteria:**
  - All selected requirements are implemented, and the main use cases work end to end.
  - Diagrams match the final architecture and code.
  - Every requirement traces to design, module, and test.
  - Installation and run instructions work on a clean machine (NFR-17).
  - Browser compatibility, accessibility, and usability checks are done (NFR-01, NFR-13, NFR-14).
  - Repository is tagged `v1.0.0`.
