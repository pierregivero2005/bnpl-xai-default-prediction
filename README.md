# bnpl-xai-default-prediction

Code for the undergraduate thesis "Explainable Machine Learning (XAI) for Default Prediction in a Buy-Now-Pay-Later (BNPL) Platform Using Alternative, Behavioral, and Socio-Economic Data", BS Data Science and Analytics, College of Science, University of Santo Tomas.

The project compares Logistic Regression, Random Forest, and XGBoost for predicting loan default, using features grouped under a Modified Five Cs of Credit framework. Models are explained with SHAP, permutation importance with Benjamini-Hochberg correction, and accumulated local effects (ALE).

## Table of Contents

- [Repository Structure](#repository-structure)
- [Requirements](#requirements)
- [Data](#data)
- [Usage](#usage)
- [Results](#results)
- [Authors](#authors)
- [Acknowledgments](#acknowledgments)

## Repository Structure

```
bnpl-xai-default-prediction/
├── thesis_EDA_v4.ipynb          # EDA, feature construction, train/test split
├── thesis_models.ipynb          # model development with class weighting
├── thesis_models_smote.ipynb    # model development with SMOTE (comparison)
├── thesis_evaluation.ipynb      # test-set evaluation, SHAP, permutation tests, ALE, fairness
├── validate_appendix_v2.ipynb   # checks appendix tables against the result files
├── thesis_pipeline.py           # shared preprocessing and evaluation functions
├── results.zip                  # result tables and figures
├── requirements.txt
└── README.md
```

## Requirements

Python 3.13.9

```
pip install -r requirements.txt
```

## Data

This project uses the [Home Credit Default Risk](https://www.kaggle.com/competitions/home-credit-default-risk/data) dataset from Kaggle. The data is not included in this repository because the competition rules do not allow redistribution.

Download the dataset and place the CSV files in the root of the repository.

## Usage

Run the notebooks in the following order:

1. `thesis_EDA_v4.ipynb` - builds the features and saves `model_data.pkl`
2. `thesis_models.ipynb` - tunes and trains the three models, outputs to `layer4_outputs/matrix_class_weight/`
3. `thesis_models_smote.ipynb` - same as step 2 using SMOTE, outputs to `layer4_outputs/matrix_smote/`
4. `thesis_evaluation.ipynb` - evaluates the models on the test set, outputs to `layer56_outputs/matrix_class_weight/`
5. `validate_appendix_v2.ipynb` (optional) - checks the appendix tables against the outputs of steps 2 and 4

Before running, set `DATA_DIR` at the top of each notebook to the path of your local copy of the repository.

Steps 2 and 3 take several hours. Set `QUICK_MODE = True` in `thesis_models.ipynb` for a short test run on a 20% sample.

All random processes use seed 42.

## Results

To view the results without running the notebooks, extract `results.zip` in the repository folder. It contains:

- `layer4_outputs/` - cross-validation results, hyperparameter grids, selected parameters, thresholds, and multicollinearity checks
- `layer56_outputs/` - test-set metrics with bootstrap confidence intervals, SHAP importance, permutation tests, ALE, thin-file comparison, and fairness metrics

The trained models and `model_data.pkl` are not included due to file size. They are recreated by running the notebooks.

## Authors

- Pierre Justine M. Givero
- Thea Bianca B. Mangila

## Acknowledgments

- Home Credit Group for the Home Credit Default Risk dataset
- College of Science, University of Santo Tomas
