# Requirements Traceability Matrix

**Project:** AI Student Success and Dropout-Risk Support System (Group 02)  
**Source of truth:** requirement IDs and wording in `docs/requirements.md`; design links refer to current documents/diagrams. Planned module and test names are targets, not claims of implemented code. Replace them with actual paths and test IDs as implementation proceeds.

## Functional requirements

| Requirement ID | Use case / design element | Increment / version | Implementation module(s) (planned) | Test(s) (planned) | Status |
|---|---|---|---|---|---|
| FR-01–FR-03 | Sign-in, role permissions, sign-out; roles in `docs/requirements.md` and use case diagram | v0.2.0 | Dashboard authentication/session; API authorization | Auth/session and role-access tests | Planned |
| FR-04 | Dataset loading and synthetic identities; data preparation in architecture | v0.2.0 | Data loader, synthetic identity generator, database seed | Loader, identity privacy, and reproducibility tests | Planned |
| FR-05–FR-07 | Student list, search, filters; “Review Student Records and Dashboard Analytics” | v0.2.0 | Student repository/API and dashboard pages | Pagination, search, and filter tests | Planned |
| FR-08 | Student profile; class diagram and ERD | v0.2.0 | Student API/repository and profile page | Profile field/display tests | Planned |
| FR-09 | Dashboard analytics; dashboard component in architecture | v0.2.0 | Analytics queries and dashboard widgets | Analytics aggregation tests | Planned |
| FR-10 | Input validation; prediction sequence and API boundary | v0.2.0 (baseline), v0.3.0 (prediction inputs) | Request schemas/validators | Valid, invalid, and incomplete input tests | Planned |
| FR-11–FR-12 | Offline training/evaluation and versioned model publication; model preparation flow | v0.3.0 | Training/evaluation pipeline and artifact metadata | Reproducibility, metrics, and artifact loading tests | Planned |
| FR-13–FR-17 | Advisor estimate request, class/probabilities/version/time, disclaimer; prediction sequence | v0.3.0 | Prediction service/API and estimate UI | Authorization, output, metadata, disclaimer, and failure-path tests | Planned |
| FR-18 | Prediction history; class diagram and ERD | v0.3.0 | Prediction repository/API and student history view | Persistence and per-student history tests | Planned |
| FR-19 | Override/dismiss with reason and original retained; use case and class diagram | v0.4.0 | Decision/override service and UI | Reason required, original retained, authorization tests | Planned |
| FR-20–FR-21 | Individual and global feature explanations; explanation design in architecture/model documentation | v0.4.0 | Explanation service and prediction/model information views | Explanation output and non-causal wording review/tests | Planned |
| FR-22–FR-24 | Create/update/view follow-up; activity diagram, class diagram, and ERD | v0.4.0 | Follow-up service/API, status history, dashboard views | Required fields, valid/invalid transitions, history tests | Planned |
| FR-25–FR-26 | Audit recording and administrator audit view; sequence/activity diagrams and ERD | v0.3.0 (prediction events), v0.4.0 (all specified actions) | Audit service/repository and admin audit page | Event coverage, attribution, timestamp, and access tests | Planned |
| FR-27–FR-28 | Cohort report filters and CSV export; administrator report workflow | v0.4.0 | Reporting queries, report UI/export | Aggregation, filters, permitted fields, and export audit tests | Planned |
| FR-29 | Administrator account creation/deactivation/role assignment; roles and user model | v0.4.0 | User administration API and UI | Role assignment, deactivation, and authorization tests | Planned |
| FR-30 | Model limitations and intended-use page; project description and architecture | v0.4.0 | Model information/limitations page | Required content and disclaimer review | Planned |

## Non-functional requirements

| Requirement ID | Use case / design element | Increment / version | Implementation module(s) (planned) | Test(s) (planned) | Status |
|---|---|---|---|---|---|
| NFR-01 | Usability and three-click navigation across core workflows | v0.2.0–v0.4.0 | Dashboard navigation and pages | Workflow usability check | Planned |
| NFR-02 | Dashboard/search response within 3 seconds in documented demo setup | v0.2.0 | Dashboard/API/data queries | Timed search, record, and dashboard checks | Planned |
| NFR-03 | Prediction response within 5 seconds, excluding startup/model load | v0.3.0 | Prediction service/API | Timed prediction check | Planned |
| NFR-04 | Clear validation/model errors; no fabricated or stale new estimate; no crash | v0.2.0–v0.4.0 | Validators, API error handling, prediction UI | Invalid input and unavailable-model tests | Planned |
| NFR-05 | Prediction, follow-up, user, and audit persistence across restarts | v0.2.0–v0.4.0 | Database/repositories | Persistence/restart integration tests | Planned |
| NFR-06 | Synthetic identities only in dashboard, exports, and repository | v0.2.0–v1.0.0 | Data loader, UI, reporting, repository practices | Data/export inspection | Planned |
| NFR-07 | Signed-in access, server-side role authorization, hashed passwords | v0.2.0–v0.4.0 | Authentication and API authorization | Authentication, role, and password-storage tests | Planned |
| NFR-08 | Attributable, timestamped audit records not editable/deletable in app | v0.3.0–v0.4.0 | Audit service/database/API | Audit attribution, timestamp, and mutation-access tests | Planned |
| NFR-09 | Understandable explanations that do not imply causation | v0.4.0 | Explanation service and UI copy | Explanation content review/tests | Planned |
| NFR-10 | No automated decisions/interventions/notifications; sensitive attributes addressed in ML documentation | v0.3.0–v0.4.0 | Prediction workflow and model documentation | Workflow inspection and documentation review | Planned |
| NFR-11 | Separable data, training/evaluation, prediction, and UI modules documented in architecture | v0.2.0–v0.4.0 | Project module structure and `docs/architecture.md` | Architecture/code review | Planned |
| NFR-12 | Dataset, preprocessing, evaluation, random seed, and model version documented for reproducibility | v0.3.0 | Training pipeline, model metadata, ML documentation | Repeated-run and metadata checks | Planned |
| NFR-13 | Current desktop Chrome, Edge, and Firefox compatibility | v0.2.0–v1.0.0 | Dashboard/UI | Browser compatibility checklist | Planned |
| NFR-14 | Readable text, meaningful labels, keyboard-operable primary workflows | v0.2.0–v0.4.0 | Dashboard components/forms | Accessibility review and keyboard workflow check | Planned |
| NFR-15 | Add records/users without major architecture change | v0.2.0–v1.0.0 | Data model, repositories, modular services | Design/code review; representative data check | Planned |
| NFR-16 | Automated tests pass for every working increment before PR merge | v0.2.0–v1.0.0 | CI/test suite | Increment test suite and PR checks | Planned |
| NFR-17 | Reproducible run instructions on a clean machine | v0.2.0–v1.0.0 | README/setup/dependency configuration | Clean-machine setup walkthrough | Planned |

## Design coverage note

The use case, sequence, and activity diagram acceptance criteria call for diagram elements to trace to requirement IDs. The grouped mappings above provide requirement coverage by workflow; when implementing or revising individual diagram elements, add the relevant FR/NFR IDs to the diagram notes or corresponding use case description and keep this matrix aligned. Actual implementation paths and test identifiers remain to be filled in as code is created.
