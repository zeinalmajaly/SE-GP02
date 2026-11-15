# SE-GP02-AI Student Success and Dropout-Risk Support System

## 1. Group Information

| Item | Details |
|---|---|
| Group number | 02 |
| Case-study title | AI Student Success and Dropout-Risk Support System |
| Course | Software Engineering (CS13477), Fall 2026 (Academic Year 2026/2027) |
| Instructor | Dr. Samer El Kababji |
| Repository | `https://github.com/zeinalmajaly/SE-GP02.git` |

| Student name | Student ID |
|---|---|
| Zein Al-Majali | 20230185 |
| Randa Altajee | 20230391 |
| Ahmed Sabri | 20230018 |
| Nicole Ansara | 20230273 |

## 2. Project Overview

**System purpose.** A decision-support system that estimates a student's academic outcome (Dropout / Enrolled / Graduate) from enrollment and academic variables. Estimates are shown as decision-support information only and never as an automatic decision about a student.

**Expected final outcome.** A functional web dashboard where authorized users (Advisor, Administrator) can:
- inspect student records (synthetic identities only);
- obtain model-based risk/outcome estimates with a visible disclaimer;
- view explanatory factors and global feature summaries;
- record and track follow-up actions with an audit log; and
- view cohort reports and a model-limitations page.

**Data.** UCI *Predict Students' Dropout and Academic Success* dataset (4,424 records, 36 features). The raw dataset is not committed; see `data/README` or `docs/requirements.md` for download instructions.

**Main technology / tools** 


## 3. Architecture and Diagrams

Editable sources are in `/uml/`, and rendered images are in `/uml/rendered/`. 

| Diagram | Description |
|---|---|
|C4 Level 1 - System Context | Illustrates the system, its users, and external dependencies.|
C4 Level 2 - Container Diagram | Shows the main application containers, including the frontend, backend, database, and machine learning component.|
|High-Level Architecture Diagram| Describes the main system components and their interactions.|
|Use Case Diagram| Illustrates the functionalities available to administators and academic advisors.|
|Sequence Diagrams | Describe important interactions, such as login, student search, and prediction generation.|
|Class Diagram | Represents the main application classes and their relationships.|
|Entity Relationship Diagram (ERD)| Represnts the database entities and their relationships.|
|Activity Diagram| Illustrates important workflows, such as generating predictions and recording support actions.|
## 4. Repository Structure

```
Group02-Student-Success-System/
│
├── README.md
│
├── docs/
│   ├── project_description.md
│   ├── requirements.md
│   ├── incremental_development_plan.md
│   ├── architecture.md
│   ├── ai_development_log.md
│   ├── traceability_matrix.md
│   ├── testing.md
│   └── report.md
│
├── uml/
│   └── rendered/
│
├── src/
│   ├── frontend/
│   ├── backend/
│   ├── models/
│   ├── database/
│   └── services/
│
├── tests/
│
├── data/
│   ├── raw/
│   ├── processed/
│   ├── samples/
│   └── README.md
│
├── prompts/
│
└── config/
```
### Main Directories

- **docs/** – Project documentation, requirements, development plan, testing, and reports.

- **uml/** – Editable architecture and UML diagrams, including rendered versions.

- **src/** – Application source code, including frontend, backend, database, and machine learning components.

- **tests/** – Unit, integration, API, and system tests.

- **data/** – Dataset instructions, small samples, and processed data where appropriate.

- **prompts/** – Markdown records of tasks and instructions provided to Agentic AI coding tools.

- **config/** – Application and environment configuration files.

## 5. Incremental Development

| Version | Capability introduced |
|---|---|

Details are in `docs/incremental_development_plan.md`.

## 6. Contributions

| Member | Main responsibility | Commits |
|---|---|---|
| `Zein Al-Majali` |  | `<n>` |
| `Randa Altajee` |  | `<n>` |
| `Ahmed Sabri` |  | `<n>` |
| `Nicole Ansara` |  | `<n>` |

*Commit count alone does not determine contribution quality. Each member also reviews AI-generated output on a rotating basis (see `docs/ai_development_log.md`).*
