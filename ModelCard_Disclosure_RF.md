# Model Card — Disclosure (RF)

**Problem**: Predict likelihood a tech worker will **disclose** a mental-health condition at work.  
**Use**: Identify culture/process levers; guide policy & program design.

## Data
- Source: Post-pandemic tech worker survey (after cleaning and proxy creation).
- Target: `disclosure` (via coworker/supervisor channels; definition aligned to EDA ≈ 50% prevalence).
- Features: age, stigma_index, gender, company size, anonymity, leave, benefits, care options, seek help (OHE + scaling).

## Pre-processing
- Numeric: median impute + **StandardScaler**  
- Categorical: most-frequent impute + **OneHotEncoder**  
- Implemented with a single scikit-learn **Pipeline** (ColumnTransformer → Estimator).

## Models compared
- Logistic Regression (balanced), Random Forest, Gradient Boosting, **MLP (neural net)** with GridSearchCV.

## Validation
- Stratified **train/test** split (80/20) + **5-fold CV** on training.  
- Primary metric: **ROC-AUC**; also Precision, Recall, F1, Accuracy on test.

## Results
- CV ROC-AUC (best): **0.735**  
- Test: AUC **0.775**, F1 **0.667**, Precision **0.647**, Recall **0.688**, Accuracy **0.702**  
- Operating threshold: **0.42** (F1-optimized)  
- Plots: ![](artifacts/ROC_Disclosure_RF.png)  |  ![](artifacts/PR_Disclosure_RF.png)

## Key Drivers

**Top drivers (permutation importance on raw features)**:

| raw_feature   |   importance_mean |   importance_std |
|:--------------|------------------:|-----------------:|
| stigma_index  |        0.14467    |       0.0273654  |
| leave         |        0.0539584  |       0.0183212  |
| anonymity     |        0.0202877  |       0.0119189  |
| seek_help     |        0.013476   |       0.0117605  |
| gender        |        0.0126917  |       0.00789955 |
| no_employees  |        0.00714217 |       0.00951739 |
| age           |       -0.00266408 |       0.00474906 |
| benefits      |       -0.00446686 |       0.00758832 |
| care_options  |       -0.00731379 |       0.0065765  |

## Notes & Risks
- Culture/process variables dominate impact (leave ease, anonymity, seek-help awareness, stigma).  
- Typos & micro-categories in raw gender can inflate coefficients; consider collapsing to 3–4 buckets.  
- Observational survey → correlational insights; use to prioritize **hypothesis-driven A/B** interventions.

*(Auto-generated from in-memory objects; artifacts stored under `artifacts/` and `models/`.)*