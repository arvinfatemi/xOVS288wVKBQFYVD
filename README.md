# Happy Customers Satisfaction Analysis

This notebook reproduces the ACME Happiness Survey challenge from Apziva: predict whether a customer is happy (`Y = 1`) or unhappy (`Y = 0`) using six 1–5 Likert-scale survey questions about delivery, order quality, pricing, courier experience, and app usability. I polished the original notebook so it can serve as a portfolio-ready artefact with a clear storyline, diagnostics, and conclusions.

## Dataset
- **Source:** `ACME-HappinessSurvey2020.csv` (included in the repo; originally provided via Apziva brief)
- **Rows:** 127 respondents
- **Target:** `Y` (1 = happy, 0 = unhappy)
- **Features:**
  - `on_time_delivery`: “My order was delivered on time”
  - `content_as_expected`: “Contents of my order were as expected”
  - `all_items_ordered`: “I ordered everything I wanted to order”
  - `perceived_value`: “I paid a good price for my order”
  - `courier_experience`: “I am satisfied with my courier”
  - `app_usability`: “The app makes ordering easy for me”

The questions are ordinal (1 = strongly disagree, 5 = strongly agree). Class balance: ~58% happy vs. 42% unhappy customers.

## Repository contents
| Path | Description |
| --- | --- |
| `HappyCustomers.ipynb` | Polished, narrated notebook covering EDA, modeling, diagnostics, and recommendations. |
| `ACME-HappinessSurvey2020.csv` | Raw survey responses used throughout the notebook. |
| `project-description.txt` | Original brief from Apziva outlining goals and success criteria. |
| `README.md` | You are here. |
| `.gitignore` | Prevents notebooks’ cache/virtualenv artifacts from being committed. |

## Getting started
1. **Create a virtual environment (optional but recommended)**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```
2. **Install dependencies** (everything required by the notebook):
   ```bash
   pip install pandas numpy seaborn scikit-learn xgboost matplotlib nbclient nbformat nbconvert ipykernel
   ```
3. **Run or reproduce the notebook**
   - Interactive: `jupyter notebook HappyCustomers.ipynb`
   - Automated: `jupyter nbconvert --to notebook --execute --inplace --ExecutePreprocessor.kernel_name=python3 HappyCustomers.ipynb`

## Highlights & results
- Added narrative cells, class-balance checks, missing-value audits, boxen plots, and mean-score lift calculations to clearly explain the data before modeling.
- Evaluated Logistic Regression, Random Forest, SVC, and XGBoost across accuracy/precision/recall/F1/ROC-AUC with cross-validation for both the full feature set and a reduced two-feature subset.
- Identified `on_time_delivery` and `courier_experience` as the dominant drivers; a Random Forest trained only on these two signals reaches **73.08% hold-out accuracy**, hitting the target while simplifying the survey.
- Included confusion matrix, classification report, and permutation-importance visualizations to show error trade-offs and confirm feature contributions.

## Next steps
- Layer in additional business features (actual delivery SLAs, courier IDs) to see if operational data can boost predictive power.
- Automate periodic retraining/reporting so operations teams can track the happiness mix over time.
- Convert the polished notebook into a short executive report or dashboard for non-technical stakeholders.
