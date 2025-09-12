<img width="1536" height="1024" alt="ChatGPT Image Sep 10, 2025, 04_57_22 PM" src="https://github.com/user-attachments/assets/20bb75a8-b873-4d16-8975-a03ee7b8983f" />

# Mental Health Risk in Tech Workers Post-Pandemic

The COVID-19 pandemic dramatically shifted workplace culture, with remote work and rising mental-health challenges impacting the global tech workforce. Disclosure of mental-health conditions at work remains a critical issue: while many employees experience stigma, companies struggle to build cultures that encourage openness and provide adequate support.

In this project, I aim to analyze post-pandemic survey data of tech workers to predict disclosure likelihood and identify employee personas that can guide HR and People Ops teams in creating safer, more supportive workplaces.

# Data

The dataset comes from a post-pandemic mental health in tech survey (~1,259 responses after cleaning).

Key features: age, gender, company size, stigma index, leave policy, anonymity, benefits, care options, seek help

Target: disclosure (1 = would disclose; 0 = would not disclose)

Balance: roughly 50/50 split, supporting unbiased modeling

Artifacts:

survey.csv
 (raw data)

survey_clean.csv (cleaned dataset created during wrangling)

# Method

Three main approaches were explored in this project:

Exploratory Data Analysis (EDA):

Visualized disclosure distribution and relationships with workplace factors.

Key relationships emerged for leave policy clarity, anonymity, and stigma.

Supervised Learning Models:

Logistic Regression (with balanced class weights)

Random Forest (with balanced class weights)

Validation: stratified 80/20 train-test split, 5-fold cross-validation.

Winner: Logistic Regression with ROC-AUC = 0.806 on the test set.

Clustering for Personas:

Segmented employees into 3–5 personas (e.g., “High stigma, low support” vs. “Low stigma, high support”).

Personas linked directly to actionable HR interventions.

# Data Cleaning

Following the Springboard Data Wrangling rubric:

Standardized schema and column names

Removed duplicates and irrelevant fields

Treated missing values:

Numeric → median imputation

Categorical → mode imputation

Encoded categorical variables via one-hot encoding

Reviewed outliers in stigma index and capped extreme values

Outputs:

Cleaned dataset: survey_clean.csv

Documented in Wrangling Notebook

# EDA

The following relationships were key:

Leave policy vs disclosure – clearer leave policies = higher disclosure

Anonymity vs disclosure – availability of anonymous channels boosts disclosure

Stigma index – strongest negative correlation with disclosure

(See EDA Notebook
 for details.)

# Algorithms & Machine Learning

I implemented a Pipeline using scikit-learn’s ColumnTransformer:

Numeric features: median imputation + standardization

Categorical features: mode imputation + one-hot encoding

Results:

Logistic Regression (best model)

CV ROC-AUC: 0.726

Test ROC-AUC: 0.806

F1 score: ~0.75

Key predictors: stigma_index, leave policy, anonymity

(See Modeling Notebook
.)

# Personas

Employee clusters revealed distinct profiles:

High stigma, low support → at risk of non-disclosure

Medium stigma, partial support → uncertain, may disclose if culture improves

Low stigma, high support → most likely to disclose safely

These personas provide a practical framework for HR segmentation and tailored programs.

# Business Insights

Policy clarity matters: well-defined mental-health leave policies raise disclosure likelihood.

Anonymous pathways help: confidential reporting channels create safer environments.

Benefits breadth reduces stigma: counseling and care options buffer stigma effects.

Recommendations:

Publish clear mental-health leave guidelines

Expand anonymous reporting channels

Strengthen mental-health benefits portfolio

Monitor progress with dashboards

# Deliverables

Jupyter notebooks: Wrangling, EDA, Modeling

Cleaned dataset (survey_clean.csv)

Tableau/PostHog dashboards (interactive HR exploration)

GitHub repo with README + model card

#Future Improvements

Expand dataset (include HRIS and benefits usage data)

Longitudinal studies to measure disclosure trends over time

Build real-time HR dashboards for proactive intervention

10. Credits

Dataset: Tech Worker Mental Health Survey (post-pandemic)

Mentorship: Springboard Capstone guidance and rubric

Libraries: pandas, scikit-learn, matplotlib, seaborn


