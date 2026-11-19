# Explainable Machine Learning for Default Prediction in a Buy-Now-Pay-Later Platform

Code and result files for the Capstone 2 thesis *Explainable Machine Learning (XAI) for Default Prediction in a Buy-Now-Pay-Later (BNPL) Platform Using Alternative, Behavioral, and Socio-Economic Data*.

**Authors:** Pierre Justine M. Givero and Thea Bianca B. Mangila, BS Data Science and Analytics, College of Science, University of Santo Tomas

## Data

The study uses the Home Credit Default Risk dataset (Home Credit Group, 2018). It is **not included** in this repository because the competition rules do not allow redistribution.

1. Download it from <https://www.kaggle.com/competitions/home-credit-default-risk/data> (a Kaggle account is required, and you must accept the competition rules).
2. Unzip all the CSV files into the **root folder of this repository**, next to the notebooks.

## Environment

Python 3.13.9. Install the packages with:

```
pip install -r requirements.txt
```

## How to reproduce the results

Run the notebooks from the repository folder, in this order. All randomness is fixed with seed 42.

| Step | Notebook | What it does | Main outputs |
|---|---|---|---|
| 1 | `thesis_EDA_v4.ipynb` | Exploratory analysis (Layer 1), feature construction (Layer 3), stratified 80/20 split | `model_data.pkl` |
| 2 | `thesis_models.ipynb` | Layer 4 with class weighting: multicollinearity check, 5-fold grid search, fold metrics, fold-level SHAP, final models | `layer4_outputs/matrix_class_weight/` |
| 3 | `thesis_models_smote.ipynb` | Same as step 2 with SMOTE inside the training folds (comparison reported in Chapter IV) | `layer4_outputs/matrix_smote/` |
| 4 | `thesis_evaluation.ipynb` | Layers 5 and 6 on the test set: performance and bootstrap CIs, thin-file results, Q2 feature sets, SHAP, permutation tests with Benjamini-Hochberg correction, model agreement, ALE, fairness | `layer56_outputs/matrix_class_weight/` |
| 5 | `validate_appendix_v2.ipynb` | Optional. Checks every number in the appendix tables against the files in steps 2 and 4 | `appendix_audit.xlsx` |

`thesis_pipeline.py` holds the shared preprocessing and evaluation code. Keep it in the same folder: the saved models refer to its classes.

Steps 2 and 3 take several hours each on a laptop. Set `QUICK_MODE = True` in step 2 for a test run on a 20% sample (minutes); its outputs go to a separate `_QUICK` folder and are not used in the thesis.

## Files in this repository

- **Notebooks and `thesis_pipeline.py`:** all code for the six layers of the analytical framework.
- **`results.zip`:** the result tables behind Chapter IV and the appendices (CSV and JSON) and the figures (PNG). Unzip it in the repository folder to get `layer4_outputs/` and `layer56_outputs/`, which the notebooks and `validate_appendix_v2.ipynb` read.
- **Not included:** the raw data, `model_data.pkl` (step 1), and the fitted models in `*/models/` (steps 2 and 3). They are too large for GitHub and are rebuilt by running the notebooks.

## Where the thesis tables come from

| Thesis table | Result file |
|---|---|
| Table C1 (hyperparameters) | `layer4_outputs/matrix_class_weight/grid_*.csv`, `best_params.json`, `thresholds.json` |
| Tables C2–C3 (multicollinearity) | `layer4_outputs/matrix_class_weight/vif.csv`, `collinearity_pairs_before.csv` |
| Table C4 (all features) | `layer56_outputs/matrix_class_weight/shap_mas_ci.csv`, `permutation_bh.csv` |
| Table C5 (grouped permutation) | `layer56_outputs/matrix_class_weight/permutation_bh.csv` |
| Table C6 (SHAP by data type) | `layer56_outputs/matrix_class_weight/shap_share_by_datatype.csv` |
| Table C7 (thin-file) | `layer56_outputs/matrix_class_weight/thin_vs_full_file.csv` |
| Table D1 (folds) | `layer4_outputs/matrix_class_weight/fold_metrics.csv` |
| Table D2 (fairness) | `layer56_outputs/matrix_class_weight/fairness.csv`, `fairness_summary.csv` |
