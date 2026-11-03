# Student Performance Prediction

<div align="center">

<p><strong>END-TO-END MACHINE LEARNING PROJECT</strong></p>

<img src="https://img.shields.io/badge/Python-0F172A?style=for-the-badge" alt="Python" />
<img src="https://img.shields.io/badge/Scikit-learn-0F172A?style=for-the-badge" alt="Scikit-learn" />
<img src="https://img.shields.io/badge/Flask-0F172A?style=for-the-badge" alt="Flask" />

<a href="https://github.com/rahat-codes/mlproject"><img src="https://img.shields.io/github/stars/rahat-codes/mlproject?style=social" alt="GitHub stars" /></a>

</div>

---

An end-to-end machine-learning application that predicts a student's **mathematics score** from demographic and academic input features. The project demonstrates a Python workflow spanning data ingestion, preprocessing, model comparison, artifact persistence, and a Flask-based prediction interface.

> **Project status:** Educational ML application. Predictions are model estimates, not official academic assessments. The repository's current implementation and dataset should be reviewed before using the model for any consequential decision.

## Problem and Inputs

The prediction pipeline uses these input features:

- Gender
- Race/ethnicity group
- Parental level of education
- Lunch category
- Test preparation course
- Reading score
- Writing score

**Target:** `math_score`

The data-ingestion component reads the student dataset from `notebook/data/stud.csv` and creates a reproducible 80/20 train/test split using `random_state=42`.

## Engineering Workflow

```text
Student dataset
      |
      v
Data ingestion
      |
      v
Train / test split
      |
      v
ColumnTransformer
  |             |
  |             +--> Categorical imputation
  |                  One-hot encoding
  |                  Scaling
  |
  +--> Numeric imputation
       Standard scaling
      |
      v
Model comparison and tuning
      |
      v
Serialized model + preprocessor
      |
      v
Flask prediction interface
```

## Models Included

The model-training component compares several regression estimators:

- Random Forest Regressor
- Decision Tree Regressor
- Gradient Boosting Regressor
- Linear Regression
- K-Neighbors Regressor
- XGBoost Regressor
- CatBoost Regressor
- AdaBoost Regressor

The current trainer uses an evaluation helper to compare models and selects a candidate based on its reported score. The prediction pipeline applies the saved preprocessor before calling the saved model.

**No fixed accuracy or R² result is claimed here.** Add a measured score, evaluation protocol, and error analysis after rerunning the experiment and verifying the output.

## Technology Stack

| Area | Tools |
|---|---|
| Language | Python |
| Data processing | Pandas, NumPy |
| Machine learning | scikit-learn, XGBoost, CatBoost |
| Web interface | Flask |
| Model persistence | Serialized model and preprocessing artifacts |
| Visualization dependencies | Matplotlib, Seaborn |

## Repository Structure

```text
mlproject/
├── app.py
├── application.py
├── artifacts/
│   ├── data.csv
│   ├── train.csv
│   ├── test.csv
│   ├── model.pkl
│   └── preprocessor.pkl
├── notebook/
│   ├── data/
│   │   └── stud.csv
│   └── notebooks for EDA and training
├── src/
│   ├── components/
│   │   ├── data_ingestion.py
│   │   ├── data_transformation.py
│   │   └── model_trainer.py
│   ├── pipeline/
│   │   └── predict_pipeline.py
│   ├── exception.py
│   ├── logger.py
│   └── utils.py
├── templates/
│   ├── home.html
│   └── index.html
├── requirements.txt
└── setup.py
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/rahat-codes/mlproject.git
cd mlproject
```

### 2. Create and activate a virtual environment

**Windows PowerShell**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**macOS / Linux**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Run the training workflow

From the repository root, run:

```bash
python src/components/data_ingestion.py
```

This script runs data ingestion, preprocessing, model training, and prints the returned evaluation score. It expects the dataset at `notebook/data/stud.csv`.

### 5. Run the Flask application

```bash
python app.py
```

Open the local address printed by Flask in your browser.

## Engineering Notes and Next Steps

- [ ] Add pinned dependency versions and document the tested Python version.
- [ ] Add tests for preprocessing, feature validation, and prediction behavior.
- [ ] Move model paths and configuration into a single configuration module.
- [ ] Make model selection reproducible with fixed random seeds and documented cross-validation.
- [ ] Report MAE, RMSE, and R² on a held-out test set; include residual analysis.
- [ ] Validate incoming form values and return user-friendly errors.
- [ ] Add model/data version metadata and document artifact provenance.
- [ ] Avoid committing sensitive data or unnecessary generated training artifacts.
- [ ] Add screenshots of the web interface.

## Author

**Rahat** · [GitHub](https://github.com/rahat-codes)
