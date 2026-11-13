# SE-GP02-AI Student Success and Dropout-Risk Support System

## 1. Group Information

| Item | Details |
|---|---|
| Group number | 02 |
| Case-study title | AI Student Success and Dropout-Risk Support System |
| Course | Software Engineering (CS13477), Fall 2026 (Academic Year 2026/2027) |
| Instructor | Dr. Samer El Kababji |
| Repository | `<URL>` |

| Student name | Student ID |
|---|---|
| `Zein Al-Majali` | `20230185` |
| `Randa Altajee` | `20230391` |
| `Ahmed Sabri` | `20230018` |
| `Nicole Ansara` | `20230273` |

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

## 4. Repository Structure

```
README.md
docs/        Requirements, plan, architecture, AI log, traceability matrix, testing, report
uml/         Editable diagram sources (.puml / .mmd / .drawio); rendered/ holds images
src/         Application source, generated and maintained through Agentic AI
tests/       Unit, component, integration, and system tests
data/        Small samples and configuration only
prompts/     Markdown records of every meaningful agent task
config/      Configuration files
```

## 5. Incremental Development

| Version | Capability introduced |
|---|---|

Details are in `docs/incremental_development_plan.md`.

## 6. Contributions

| Member | Main responsibility | Commits |
|---|---|---|
| `<Member A>` |  | `<n>` |
| `<Member B>` |  | `<n>` |
| `<Member C>` |  | `<n>` |
| `<Member D>` |  | `<n>` |

*Commit count alone does not determine contribution quality. Each member also reviews AI-generated output on a rotating basis (see `docs/ai_development_log.md`).*
