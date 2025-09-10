# Model Card — Disclosure

**Problem**: Predict likelihood that a tech worker will **disclose** a mental-health condition at work.  
**Audience/Use**: Identify culture/process levers that increase safe disclosure; inform policy and programs.

## Data
- Source: Post-pandemic tech worker survey (N ≈ 1259 after cleaning).
- Target: `disclosure` (1 = would disclose via coworker/supervisor channel; scheme tuned to align with EDA ~50%).
- Key features: age, stigma_index, gender, company size, anonymity, leave policy, benefits, care options, seek help.

## Pre-processing
- Numeric: median imputation + standardization.
- Categorical: most-frequent imputation + one-hot encoding.
- Implemented with `ColumnTransformer` in a single `Pipeline`.

## Models Evaluated
- Logistic Regression (balanced class weights) — **best**
- Random Forest (balanced class weights)
- (Optional MLP in separate notebook; similar evaluation protocol)

## Validation
- Stratified **train/test split** (80/20) + **5-fold CV** on training.
- **Primary metric**: ROC-AUC; also report F1, precision, recall, accuracy on test set.

## Results (Disclosure)
- CV ROC-AUC: **0.726**
- Test ROC-AUC: **0.806**, F1: **0.702**, Precision: **0.672**, Recall: **0.734**, Accuracy: **0.730**
- Operating threshold: **0.50** (F1-optimized).  
- Calibration: Logistic regression well-calibrated (Brier lower than baseline; curve near diagonal).

## Key Drivers
- Culture/process signals dominate:
  - **Very easy leave** ↑ disclosure (largest positive coefficient).
  - **Seek-help channels known** ↑.
  - **Anonymity guaranteed** ↑; **No anonymity** ↓.
  - **Higher stigma_index** ↓.
  - **Very large org size** ↓.

**Top positive drivers** (increase odds of disclosure):

| feature                   |   odds_ratio |
|:--------------------------|-------------:|
| leave_Very easy           |      2.18705 |
| seek_help_Yes             |      1.92786 |
| gender_Neuter             |      1.88949 |
| gender_A little about you |      1.7736  |
| gender_p                  |      1.7736  |
| gender_queer/she/they     |      1.6823  |
| gender_Trans-female       |      1.62156 |
| anonymity_Yes             |      1.53108 |

**Top negative drivers** (decrease odds of disclosure):

| feature                     |   odds_ratio |
|:----------------------------|-------------:|
| stigma_index                |     0.514252 |
| anonymity_No                |     0.546661 |
| no_employees_More than 1000 |     0.571572 |
| leave_Very difficult        |     0.598802 |
| gender_msle                 |     0.647744 |
| gender_Male                 |     0.649996 |
| seek_help_No                |     0.683869 |
| seek_help_Don't know        |     0.716469 |

## Limitations & Notes
- Some raw `gender` entries include typos/rare strings; we recommend collapsing into **Male / Female / Non-binary/Other** to stabilize coefficients.
- Disclosure proxy definition affects prevalence; we fixed a scheme aligned to EDA (~50%).
- Observational survey; correlations ≠ causation. Use results to guide **hypothesis-driven interventions** and **A/Bs**.

## Reproducibility
- Artifacts saved under `models/` (`.joblib`, `.json` with metrics/threshold); encoded datasets under `data/processed/`.
- See `artifacts/model_comparison_disclosure.csv` for full comparison table.

*(Generated automatically from latest saved pipeline: `disclosure_LogReg_20250910-160101.joblib`)*