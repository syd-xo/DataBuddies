# Submission Manifest — Team 6

| Item | Value |
|---|---|
| Team | 6 — Data Buddies |
| Primary language | Luganda |
| Track | A — Intent classification |
| GitHub URL | https://github.com/syd-xo/DataBuddies.git |
| Frozen commit SHA | [FILL: output of `git rev-parse HEAD`] |
| Tag | `submission-v1` |
| Data counts | 250 total; 150 train / 50 dev / 50 test; 25 per intent |
| Source licence/permission | Code: MIT (`LICENSE_CODE.txt`); Data: `documented_contributor_permission` (private evidence, see `SOURCE_LOG.md`) |
| Metric files | `artifacts/intent/test_metrics.json`, `artifacts/intent/per_label_report.csv`, `artifacts/intent/test_predictions.csv` |
| Demo run instructions | `python -m streamlit run app.py` (see `README.md`) |
| Demo recording | [FILL: link — 2–3 min; ≥3 successes, ≥2 failures explained, metrics shown] |
| Known unresolved issues | [FILL — or "none" if none] |
| ZIP snapshot | [FILL: filename, same commit as above] |

## Pre-submission checklist
- [ ] `data/contribution.csv` validated (`PASS: 250 records`).
- [ ] All 250 rows: `review_status = independently_reviewed`, `reviewer_code = REV-LG-2026`.
- [ ] `evidence/REVIEW_LOG.csv` present.
- [ ] All eight `.md` documents present and complete.
- [ ] `artifacts/intent/*` populated from a frozen model.
- [ ] `QUALITY.md` metrics and error table pasted from real artifacts.
- [ ] README results section matches `QUALITY.md`.
- [ ] Demo recording uploaded and linked.
- [ ] Commit tagged `submission-v1`, SHA captured, ZIP downloaded.
- [ ] Submitted via official NLP Hub channel before the deadline.