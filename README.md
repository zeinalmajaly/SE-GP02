# SE-GP02: AI Student Success and Dropout-Risk Support System

## 1. Group Information

| Item | Details |
|---|---|
| Group number | 02 |
| Case-study title | AI Student Success and Dropout-Risk Support System |
| Course | Software Engineering (CS13477), Fall 2026 (Academic Year 2026/2027) |
| Instructor | Dr. Samer El Kababji |
| Repository | [SE-GP02 on GitHub](https://github.com/zeinalmajaly/SE-GP02) |

| Student name | Student ID |
|---|---|
| Zein Al-Majali | 20230185 |
| Randa Altajee | 20230391 |
| Ahmed Sabri | 20230018 |
| Nicole Ansara | 20230273 |

## 2. Project Overview

**System purpose.** A decision-support system that estimates a student's academic outcome (Dropout / Enrolled / Graduate) from enrollment and academic variables. Estimates are decision-support information only; they are not automatic decisions about students.

**Expected outcome.** A web dashboard for authorized users to:

- inspect synthetic/demo student records;
- obtain model-based outcome estimates and see a clear disclaimer;
- view explanatory factors and feature summaries;
- record and track support follow-up actions with an audit trail; and
- review cohort reports and model limitations.

**Data.** The project uses the UCI *Predict Students' Dropout and Academic Success* dataset for model development. The raw dataset is not committed to this repository. See [requirements](docs/requirements.md) for project data details.

## 3. Architecture and Diagrams

The proposed system components and their communication are described in [docs/architecture.md](docs/architecture.md). The editable C4 diagrams are draw.io files; open them with [diagrams.net](https://app.diagrams.net/).  Rendered images are in `uml/rendered/`([uml/rendered/](https://vscode.dev/github/zeinmajali/SE-GP02/blob/main/uml/rendered))

| Diagram | Description |
|---|---|
| [C4 Level 1: System Context](uml/c4_context.drawio) | System boundary, user roles, and the external public dataset source. |
| [C4 Level 2: Containers](uml/c4_container.drawio) | Dashboard, API, prediction service, database, model artifact store, and communication paths. |
| Use case diagram | User-facing functions for Advisors and Administrators. |
| Sequence diagrams | Important interactions, such as student search and prediction generation. |
| [Class diagram](uml/class_diagram.drawio) | Main domain classes and their relationships. |
| [Entity Relationship Diagram (ERD)](uml/erd.drawio) | Proposed database entities, keys, and relationships. |
| Activity diagram | Workflows such as generating predictions and recording support actions. |

Other UML diagrams are maintained separately from the C4 draw.io diagrams.

## 4. Repository Structure

```text
README.md
docs/        Requirements, project description, architecture, plans, testing, and reports
uml/      Editable diagram sources; rendered/ holds exported images
src/ Application source, generated and maintained through Agentic AI
tests/ Unit, component, integration, and system tests
data/ README, small samples and configuration
prompts/ Markdown records of each agent task
config/ Configuration files
instructions/ Course project instructions
```

## 5. Incremental Development

The project is planned in five increments: student-data dashboard, prediction service, and explanations/follow-up/reporting. See [docs/incremental_development_plan.md](docs/incremental_development_plan.md) for details.

## 6. Contributions

| Member | Main responsibility | Commits |
|---|---|---|
| Zein Al-Majali |  | `<n>` |
| Randa Altajee |  | `<n>` |
| Ahmed Sabri |  | `<n>` |
| Nicole Ansara |  | `<n>` |

Commit count alone does not determine contribution quality. Members also review AI-generated output on a rotating basis; see [docs/ai_development_log.md](docs/ai_development_log.md).
