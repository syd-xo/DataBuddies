# Team 6 — Data Buddies
## Luganda Intent Classification

**Track:** A — Intent Classification  
**Language:** Luganda  
**Dataset version:** v1  
**Dataset size:** 250 original, human-authored utterances  
**Team:** 6 — Data Buddies

## Team members

| # | Name | Role | Contributor code |
|---|---|---|---|
| 1 | Sydney Aisha | Model training, Streamlit app and demo | `T06-B` |
| 2 | Poni Yokwe | Luganda data authorship; natural phrasing and label fit | `T06-A` |
| 3 | Tiffany Wanjiru | Data plan, annotation guide, dataset card, source log, quality report, manifest | `T06-C` |

## 1. Project Overview

This project develops a research prototype that identifies the intended action in a written Luganda request. It classifies each request into one of ten intent categories aligned with the MASSIVE intent label schema.

The prototype demonstrates how a Luganda-language request-routing assistant could recognise what a user wants and display an appropriate simulated response. It does not execute real-world actions.

The project uses a character-level TF-IDF and Logistic Regression baseline model.

## 2. Dataset

The team created a dataset of **250 original Luganda utterances**, with 25 examples for each of the ten intent categories.

| Dataset split | Records | Distribution per intent |
|---|---:|---:|
| Training | 150 | 15 |
| Development | 50 | 5 |
| Testing | 50 | 5 |
| **Total** | **250** | **25** |

The utterances were human-authored and independently reviewed by a fluent Luganda reviewer who did not author the reviewed records.

### Supported intents

1. `weather_query`
2. `datetime_query`
3. `alarm_set`
4. `calendar_set`
5. `calendar_query`
6. `lists_createoradd`
7. `lists_query`
8. `play_music`
9. `news_query`
10. `qa_definition`

The dataset is stored in `data/contribution.csv`.

## 3. Technology and Tools

- **Python 3.10 or later** — project implementation.
- **Scikit-learn** — character-level TF-IDF and Logistic Regression baseline.
- **Pandas** — dataset handling.
- **Streamlit** — interactive demonstration interface.
- **Git and GitHub** — version control and project management.

The exact dependency versions are specified in `requirements.txt`.

## 4. Installation

Clone the repository and navigate into its directory:

```bash
git clone https://github.com/syd-xo/DataBuddies.git Team-6-Data-Buddies
cd Team-6-Data-Buddies
```

Create and activate a virtual environment.

**Windows PowerShell:**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**macOS/Linux:**

```bash
python -m venv .venv
source .venv/bin/activate
```

Install the project dependencies:

```bash
python -m pip install -r requirements.txt
```

Use only the activation command appropriate for your operating system.

## 5. Running the Project

Run the following commands from the repository's root directory.

### Step 1: Validate the dataset

```bash
python validate.py --track intent --data data/contribution.csv
```

The validator checks structural requirements, review information, source methods, duplicate records and split-group consistency.

The submitted dataset passed structural validation with 250 records.

### Step 2: Train the model

```bash
python train.py --track intent --data data/contribution.csv
```

This trains the intent-classification baseline using the contributed dataset.

### Step 3: Evaluate the model

```bash
python evaluate.py --track intent --data data/contribution.csv
```

Evaluation produces accuracy, macro-F1 and per-label results. It also saves prediction and metric files in the relevant artifacts directory.

### Step 4: Launch the demonstration

```bash
python -m streamlit run app.py
```

The Streamlit application allows users to enter a Luganda request and view the predicted intent, model probability and simulated response.

**Note:** Train the model before launching the application. The displayed probability is uncalibrated and should not be interpreted as a guaranteed measure of prediction reliability.

## 6. Model Outputs and Evaluation Files

Model outputs are stored in:

```text
artifacts/intent/
```

| File | Description |
|---|---|
| `test_metrics.json` | Overall evaluation metrics, including accuracy and macro-F1. |
| `per_label_report.csv` | Per-intent F1 scores and support values. |
| `test_predictions.csv` | Individual test-set predictions. |

These files support the evaluation and error analysis documented in `QUALITY.md`.

## 7. Repository Structure

```text
Team-6-Data-Buddies/
├── app.py                          # Streamlit demo UI
├── train.py                        # trains the intent classifier (dev split for tuning)
├── evaluate.py                     # frozen test-set evaluation → writes artifacts/
├── validate.py                     # structural validator (columns, splits, uniqueness)
├── core.py                         # shared utilities imported by the above
├── taxonomy.csv                    # label set used by the pipeline
├── requirements.txt                # pinned dependencies
├── LICENSE_CODE.txt                # code licence
├── .gitignore
│
├── data/
│   └── contribution.csv            # 250 reviewed Luganda records (the contribution)
│
├── artifacts/
│   └── intent/
│       ├── test_metrics.json       # accuracy, macro-F1, majority baseline
│       ├── per_label_report.csv    # per-label F1 + support
│       └── test_predictions.csv    # real predictions → source of error analysis
│
├── evidence/
│   └── REVIEW_LOG.csv              # original review log (provenance)
│
├── templates/                      # starter-kit examples and practice fixtures
│   ├── CHANGELOG.md                #   (kept for reference; NOT our contribution)
│   ├── COMPLETED_*.md
│   ├── NATURAL_DATA.md
│   ├── NEXT_STEPS.md
│   ├── TRACKS.md
│   ├── sentiment_guidelines.md
│   └── practice_*.csv
│
├── build_contribution.py           # REVIEW_LOG.csv → data/contribution.csv
├── fix_ids.py                      # resolves the 50 duplicate record_id values
│
├── README.md                       # this file
├── DATA_PLAN.md
├── ANNOTATION_GUIDE.md
├── DATA_CARD.md
├── SOURCE_LOG.md
├── QUALITY.md
├── CONTRIBUTIONS.md
└── SUBMISSION_MANIFEST.md
```

The structure above describes the main project files and expected evaluation outputs.

## 8. Data Provenance and Acknowledgements

The 250 contributed utterances were originally authored for this project. They were not copied from the starter kit's practice datasets.

The project reuses the Strathmore NLP Hub starter kit v2.0 and the MASSIVE intent label schema. The starter kit's teaching fixtures are not counted as original contributions.

Written contributor permission is documented and retained privately. Private permission evidence is not included in the public repository.

Further information about data sources, permissions and reuse is available in `SOURCE_LOG.md`.

## 9. Limitations

This project is a small research prototype and is not intended for production deployment.

Its main limitations include:

- The dataset contains only 250 utterances, with five test examples per intent. Evaluation scores therefore have considerable uncertainty.
- The dataset represents one authored set of Luganda utterances and does not establish generalisation across Luganda varieties or regions.
- Character-level TF-IDF captures surface-level text patterns but may struggle with negation, paraphrasing and unfamiliar vocabulary.
- The model always selects one of the supported intent classes, even when an input does not clearly belong to any of them.
- The displayed model probability is uncalibrated.
- The application simulates responses; it does not set alarms, manage calendars, create lists, play music or retrieve live information.

See `QUALITY.md` for the evaluation discussion and documented limitations.

## 10. Project Documentation

The following documents provide further details about the project:

| Document | Purpose |
|---|---|
| `DATA_PLAN.md` | Dataset planning, sourcing and splitting approach. |
| `ANNOTATION_GUIDE.md` | Intent definitions, examples and annotation rules. |
| `DATA_CARD.md` | Dataset description, composition and intended use. |
| `SOURCE_LOG.md` | Data provenance, permissions and source records. |
| `QUALITY.md` | Validation, review, evaluation and limitations. |
| `CONTRIBUTIONS.md` | Team roles, individual contributions and AI-use disclosure. |
| `SUBMISSION_MANIFEST.md` | Submission contents and final verification information. |

## 11. Project Scope

The project focuses exclusively on **Track A — Intent Classification** using Luganda text.

It does not implement sentiment analysis or semantic parsing. It is a demonstration of intent recognition and request routing, not a complete virtual assistant or production-ready service.

## 12. Licence and terms

**Code:** The starter kit (`train.py`, `evaluate.py`, `validate.py`, `app.py`, `core.py`
and templates) is distributed under the MIT License; the full text is in `LICENSE_CODE.txt`.
Our own scripts (`build_contribution.py`, `fix_ids.py`) are released under the same MIT terms.
Our documentation files (`.md`) are released under CC BY 4.0 unless stated otherwise.

**Data (`data/contribution.csv`):** Not MIT. The Luganda utterances were authored by a
Team 6 member and are used under `documented_contributor_permission` — written consent from
the author is held privately (see `SOURCE_LOG.md`). The file is shared publicly for
evaluation of this submission only; it is not offered for redistribution or reuse.

**Upstream:** MASSIVE label schema (label names only — no MASSIVE rows are in the
contribution file). No Common Voice text is included.  

---

**Team 6 — Data Buddies**  
**Strathmore NLP Hub Datathon 2026**

