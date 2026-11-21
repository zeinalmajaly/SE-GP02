# Traceability Matrix

Derived from the Incremental Development Plan. The plan only gives requirement **ranges** for some items (for example FR-13 to FR-17), so individual descriptions marked with `*` are inferred from the acceptance criteria. Replace them with the exact wording from your requirements document. Test entries are planned test types from the plan, not file names; fill in real test IDs as you write them.

## Functional requirements

| Req | Description | Design version / artifacts | Implementation (module) | Verification (planned test) | Release |
|---|---|---|---|---|---|
| FR-01 | Sign-in * | v0.1.0-design: `use_case.puml`, `sequence_diagram.puml`, `use_cases.md` | `src/api`, `src/db` | API tests (access control) | v0.1.0 |
| FR-02 | Sign-out * | v0.1.0-design: `use_case.puml`, `use_cases.md` | `src/api`, `src/dashboard` | API tests | v0.1.0 |
| FR-03 | Role-based access * | v0.1.0-design: `use_case.puml`, `class_diagram.drawio` (roles, enums) | `src/api`, `src/db` | API tests (access control) | v0.1.0 |
| FR-04 | One student record per dataset row with synthetic ID and name | v0.1.0-design: `c4_container.drawio`, `erd.drawio` | `src/scripts/load_dataset.py`, `src/db` | Unit tests (loader) | v0.1.0 |
| FR-05 | Paginated student list * | v0.1.0-design: `use_case.puml`, `activity_diagram.puml` | `src/api`, `src/dashboard` | API tests, demo | v0.1.0 |
| FR-06 | Search by ID and name * | v0.1.0-design: `use_case.puml` | `src/api`, `src/dashboard` | API tests | v0.1.0 |
| FR-07 | Filter student list * | v0.1.0-design: `use_case.puml` | `src/api`, `src/dashboard` | API tests | v0.1.0 |
| FR-08 | Student profile (enrollment, academic, demographic fields) | v0.1.0-design: `class_diagram.drawio`, `erd.drawio` | `src/api`, `src/dashboard`, `src/db` | API tests, demo | v0.1.0 |
| FR-09 | Dashboard outcome distribution | v0.1.0-design: `use_case.puml` | `src/dashboard` | Demo, system check | v0.1.0 |
| FR-10 | Reject invalid input with clear message | v0.1.0-design: `activity_diagram.puml` | `src/api` (validation) | Unit tests (validation) | v0.1.0 |
| FR-11 | Train and evaluate models; macro-F1, per-class recall, confusion matrix | v0.2.0-design: `ml_documentation.md`, `erd.drawio` (confusion matrix field) | `src/ml/train.py`, `evaluate.py`, `preprocessing.py` | Unit tests (preprocessing), component tests | v0.2.0-model |
| FR-12 | Versioned model file with stored evaluation metadata | v0.2.0-design: `ml_documentation.md`, ERD update (model version metadata) | `src/ml`, `models/` | Component tests (model loading) | v0.2.0-model |
| FR-13 | Advisor requests an estimate and sees the outcome * | v0.2.0-design: `sequence_diagram.puml`, component diagram | `src/api` (prediction endpoint), `src/dashboard` | Integration tests, system test | v0.2.0 |
| FR-14 | All class probabilities shown * | v0.2.0-design: `sequence_diagram.puml` | `src/api`, `src/dashboard` | Integration tests (probability sum) | v0.2.0 |
| FR-15 | Generation time shown * | v0.2.0-design: `sequence_diagram.puml` | `src/api`, `src/dashboard` | Integration tests | v0.2.0 |
| FR-16 | Model version saved and shown with each prediction | v0.1.0-design: `sequence_diagram.puml`; v0.2.0-design: ERD update | `src/api`, `src/db` | Integration tests | v0.2.0 |
| FR-17 | Decision-support disclaimer on every estimate * | v0.2.0-design: `ml_documentation.md` | `src/dashboard` | System test | v0.2.0 |
| FR-18 | Estimates stored and shown in prediction history | v0.2.0-design: `erd.drawio` | `src/db`, `src/api`, `src/dashboard` | Integration tests | v0.2.0 |
| FR-19 | Override or dismiss estimate with reason; original estimate kept | v0.1.0-design: ERD (overridden outcome); v0.4.0-design: state and activity diagrams | `src/api`, `src/db` | Workflow and database tests | v0.4.0 |
| FR-20 | Per-student contributing factors in plain language | v0.3.0-design: sequence and class diagrams, method choice | `src/ml/explain.py`, `src/dashboard` | Unit tests (explanation consistent with prediction) | v0.3.0 |
| FR-21 | Global feature summary | v0.3.0-design: class diagram, `ml_documentation.md` | `src/ml/explain.py`, `src/dashboard` | Unit tests, demo | v0.3.0 |
| FR-22 | Create follow-up (type, note, assignee, date), starting Open, optionally linked to a prediction | v0.4.0-design: state diagram, ERD update | `src/api`, `src/db` | Workflow and database tests | v0.4.0 |
| FR-23 | Notes kept without overwriting | v0.1.0-design: ERD; v0.4.0-design: activity update | `src/api`, `src/db` | Workflow and database tests | v0.4.0 |
| FR-24 | Status workflow (Open, In progress, Resolved, Closed); invalid transitions rejected; history kept | v0.4.0-design: state diagram | `src/api`, `src/db` | Workflow tests (every valid and invalid transition) | v0.4.0 |
| FR-25 | Audit entries (actor, action, time) for predictions and changes | v0.1.0-design: `class_diagram.drawio`, `erd.drawio`; v0.5.0-design: DFD | `src/api`, `src/db` (audit table and writer) | Integration tests, database tests | v0.2.0 (start), v0.4.0 |
| FR-26 | Administrator views audit log; entries cannot be edited or deleted | v0.5.0-design: audit view mock-up | `src/api`, `src/dashboard` | Access-control tests | v0.5.0 |
| FR-27 | Cohort report filtered by course and risk level | v0.5.0-design: report mock-up, DFD | `src/api`, `src/dashboard` | Tests, demo | v0.5.0 |
| FR-28 | CSV export with synthetic identities only | v0.5.0-design: export mock-up, DFD | `src/api` | Tests (export content) | v0.5.0 |
| FR-29 | Administrator creates, deactivates, assigns roles; changes audited | v0.5.0-design: user management mock-up | `src/api`, `src/dashboard`, `src/db` | Tests, access-control tests | v0.5.0 |
| FR-30 | Limitations page (intended use, performance, limitations, disclaimer) | v0.5.0-design: limitations page mock-up | `src/dashboard` | Demo, tests | v0.5.0 |

## Non-functional requirements mentioned in the plan

| Req | Description | Design / evidence | Verification | Release |
|---|---|---|---|---|
| NFR-01 | Browser compatibility | Final checks | Browser compatibility check | v1.0.0 |
| NFR-02 | Pages load within 3 seconds in demo setup | v0.1.0 scope | Demo timing | v0.1.0 |
| NFR-03 | Prediction completes within 5 seconds | v0.2.0 scope | Demo timing, system test | v0.2.0 |
| NFR-04 | Clear error on invalid input or unavailable model; no estimate stored | v0.2.0-design: component and sequence diagrams (model loading, failures) | Integration tests | v0.2.0 |
| NFR-06 | CSV export contains only synthetic identities | v0.5.0-design: DFD | Export tests | v0.5.0 |
| NFR-07 | Passwords stored hashed | v0.1.0-design | Unit tests (password hashing) | v0.1.0 |
| NFR-08 | Audit entries not editable or deletable through the app | v0.5.0-design | Access-control tests | v0.2.0 (foundation), v0.5.0 |
| NFR-09 | Wording does not claim a factor causes the outcome | v0.3.0-design: wording rule stated | Tests on explanation wording | v0.3.0 |
| NFR-10 | ML requirement (referenced for v0.2.0 design and model; text not in the plan) | v0.2.0-design: `ml_documentation.md` | Component tests | v0.2.0-model |
| NFR-12 | Reproducible training (fixed seed, same metrics on rerun) | v0.2.0-design: split, seed, metrics documented | Rerun comparison | v0.2.0-model |
| NFR-13 | Accessibility | Final checks | Accessibility check | v1.0.0 |
| NFR-14 | Usability | Final checks | Usability check | v1.0.0 |
| NFR-17 | Clean-machine installation and run instructions | Run instructions | Clean-machine install | v1.0.0 |

NFR-05, NFR-11, NFR-15 and NFR-16 are not referenced in the plan; add them from your requirements document.

## Release roll-up

| Release | Requirements covered |
|---|---|
| v0.1.0-design | FR-01..FR-10, FR-25 (design) |
| v0.1.0 | FR-01..FR-10; NFR-02, NFR-07 |
| v0.2.0-design | FR-11..FR-18; NFR-04, NFR-10, NFR-12 |
| v0.2.0-model | FR-11, FR-12; NFR-10, NFR-12 |
| v0.2.0 | FR-13..FR-18, FR-25 (start); NFR-03, NFR-04, NFR-08 |
| v0.3.0-design / v0.3.0 | FR-20, FR-21; NFR-09 |
| v0.4.0-design / v0.4.0 | FR-19, FR-22..FR-25 |
| v0.5.0-design / v0.5.0 | FR-25..FR-30; NFR-06, NFR-08 |
| v1.0.0 | All FR and NFR; NFR-01, NFR-13, NFR-14, NFR-17 |
