# Heart Disease Predictor

A machine learning model that predicts whether a patient is at high or low risk of heart disease based on clinical measurements. Built with a K-Nearest Neighbors classifier and served through a Streamlit interface.

---

## Overview

Cardiovascular disease is one of the leading causes of death globally. This project trains and benchmarks five classification models on 918 patient records from the [Kaggle Heart Failure Prediction dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction), selecting the best performer to power an interactive prediction tool that clinicians or individuals can use to assess risk in seconds.

---

## Project Structure

```
├── heart.csv                  
├── heart_disease_notebook.ipynb
├── heart_disease_model.pkl 
├── scaler.pkl          
├── columns.pkl            
└── app.py                 
```

---

## Notebook

### 1. Exploratory Data Analysis
- Inspected shape, dtypes, and class distribution of `HeartDisease` (binary target)
- Plotted distributions of `Age`, `RestingBP`, `Cholesterol`, and `MaxHR`
- Visualised attrition patterns by `Sex`, `ChestPainType`, and `FastingBS`
- Correlation heatmap on numeric features

### 2. Data Cleaning
- **Cholesterol:** zero values replaced with the non-zero column mean (physiologically invalid zeros treated as missing)
- **RestingBP:** same zero-replacement strategy applied
- No duplicate rows found; no null values in raw data

### 3. Feature Engineering
- **One-hot encoding** (`drop_first=True`): `Sex`, `ChestPainType`, `RestingECG`, `ExerciseAngina`, `ST_Slope`
- All boolean dummy columns cast to `int`
- **StandardScaler** applied to numeric columns: `Age`, `RestingBP`, `Cholesterol`, `MaxHR`, `Oldpeak`

### 4. Model Comparison

Five classifiers benchmarked on an 80/20 train/test split (scaled features):

| Model | Accuracy | F1 Score |
|---|---|---|
| Logistic Regression | 0.8696 | 0.88 |
| Naive Bayes | 0.8478 | 0.86 |
| Decision Tree | 0.7989 | 82 |
| SVM | 0.8478 | 0.87 |
| **KNN** | **0.8641** | **0.88** |

---

## Streamlit App

The app collects 11 clinical inputs:

| Input | Type | Range / Options |
|---|---|---|
| Age | Slider | 18 – 100 |
| Sex | Selectbox | M, F |
| Chest Pain Type | Selectbox | ATA, NAP, TA, ASY |
| Resting Blood Pressure | Number input | 80 – 200 mmHg |
| Cholesterol | Number input | 100 – 600 mg/dL |
| Fasting Blood Sugar > 120 mg/dL | Selectbox | 0, 1 |
| Resting ECG | Selectbox | Normal, ST, LVH |
| Max Heart Rate | Slider | 60 – 220 |
| Exercise Induced Angina | Selectbox | Y, N |
| Oldpeak (ST Depression) | Slider | 0.0 – 6.0 |
| ST Slope | Selectbox | Up, Flat, Down |

On clicking **Predict**, the app returns:
- ⚠️ **High Risk of Heart Disease**
- ✅ **Low Risk of Heart Disease**

---



## Tech Stack

| Layer | Library |
|---|---|
| Data manipulation | `pandas`, `numpy` |
| Visualization | `matplotlib`, `seaborn` |
| Machine learning | `scikit-learn` (KNN, Logistic Regression, Naive Bayes, Decision Tree, SVM) |
| Preprocessing | `StandardScaler` |
| Model serialization | `joblib` |
| Web UI | `streamlit` |

---

## Dataset

918 patient records with 12 features covering demographics, cardiac measurements, and ECG findings. Target: `HeartDisease` (1 = disease present, 0 = absent).

Source: [Kaggle – Heart Failure Prediction Dataset](https://www.kaggle.com/datasets/fedesoriano/heart-failure-prediction)

---

## Note

This tool is for **educational and demonstration purposes only**. It is not a substitute for professional medical advice, diagnosis, or treatment.

---
