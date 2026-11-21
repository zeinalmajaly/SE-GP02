# Dataset: Predict Students' Dropout and Academic Sucees 

## 1. Source
| Item | Details|
|---|---|
|**Name**| Predict Students' Dropout and Academic Success |
|**Repository**| UCI Machine Learning Repository, dataset 697|
|**Page**| https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success|
|**Creators*|  Valentim Realinho, Mónica Vieira Martins, Jorge Machado, Luís Baptista (Instituto Politécnico de Portalegre, Portugal) |
|**Donated**|  December 2021 |
|**License**|  	Creative Commons Attribution 4.0 International (CC BY 4.0) |
|**Task**|  Three-class classification|

## 2. What the dataset contains

| Characteristic | Value|
|---|---|
|**Records**| 4,424 (each record is one student)|
|**Features**| 36 plus target column|
|**Target Column**| `Target` with values **Dropout, Enrolled, Graduate**|
|**Missing Values**| None reported|
|**Class balance**| 	Strongly imbalanced toward one class (compute the exact counts in the training pipeline and record them in `docs/ml_documentation.md`)|

**Feature groups** (names as used by the dataset):

- **Enrollment and demographics:** marital status, application mode, application order, course, daytime/evening attendance, previous qualification and grade, nationality, mother's and father's qualification and occupation, admission grade, displaced, educational special needs, debtor, tuition fees up to date, gender, scholarship holder, age at enrollment, international.
- **Academic performance, first and second semester:** curricular units credited, enrolled, evaluated, approved, grade, and without evaluations.
- **Macroeconomic context:** unemployment rate, inflation rate, GDP.

## 3. Sensitive attributes

The dataset includes personal characteristics such as gender, nationality, marital status, and age at enrollment. The project handles them as follows (confirm in `docs/ml_documentation.md`):

- They are stored only for the synthetic demo records and are never linked to real people.
- Whether they are used as model inputs is a documented design decision, with its effect on performance and fairness described.
- Explanations describe associations, never causes.
- Estimates are decision support only, reviewed by a human.

## 4. Synthetic identities

The dataset contains no names or IDs. The loading script creates them:

- IDs are generated (for example `S0001`, `S0002`), not derived from any real identifier.
- Names are generated from a fixed random seed, so the demo data is reproducible.
- No real student name, ID, email, or contact detail may be added to the repository, the database, exports, or prompts.

## 5. How to obtain the data

Download to `data/raw/` (this folder is ignored by Git).

**Option A: direct download**

```bash
mkdir -p data/raw
curl -L -o data/raw/data.csv https://archive.ics.uci.edu/static/public/697/data.csv
```

**Option B: Python package**

```bash
pip install ucimlrepo
```

```python
from ucimlrepo import fetch_ucirepo
dataset = fetch_ucirepo(id=697)
X = dataset.data.features
y = dataset.data.targets
```

**Option C: manual download** from the dataset page (button "Download", then place `data.csv` in `data/raw/`).

Before use, check that the file has 4,424 rows and the expected columns, and check the field delimiter (it may be a semicolon, not a comma). The loading script must handle the actual format.

## 6. Folder layout

```text
data/
  README.md              this file
  sample/
    sample_students.csv  50 to 100 rows with synthetic IDs and names (committed)
  raw/                   downloaded dataset (ignored by Git)
  processed/             generated outputs, such as train and test splits (ignored by Git)
```

Add to `.gitignore`:

```text
data/raw/
data/processed/
*.db
*.sqlite
```

## 7. Creating the sample file

`data/sample/sample_students.csv` is a small stratified sample, used by tests and for quick demos when the full file is not available. Generate it with the loading script (do not edit it by hand), include a header row, and keep synthetic identities only. Record the seed and the date you created it at the top of this section when you generate it.

## 8. Loading into the system

The loading script (planned for v0.1.0 at `src/scripts/load_dataset.py`, requirement FR-04) will:

1. read `data/raw/data.csv` (or the sample file);
2. validate the columns and row count;
3. normalize column names and map codes to readable labels;
4. create a synthetic ID and name for each row;
5. write the records to the application database.

Run instructions will be added here after v0.1.0.

## 9. Related documents

- `docs/requirements.md`: FR-04, NFR-06, NFR-10, NFR-12
- `docs/ml_documentation.md` (to be created in v0.2.0-design): preprocessing, split strategy, metrics, handling of sensitive attributes
- `docs/architecture.md`: Data Loading Script and Model Training Pipeline containers