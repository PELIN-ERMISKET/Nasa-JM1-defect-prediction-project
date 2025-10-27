#  NASA JM1 Software Defect Prediction (Data Analysis & Machine Learning)

##  Project Overview
This project focuses on predicting software defects using the **NASA JM1 dataset** from the PROMISE repository.  
It combines **exploratory data analysis (EDA)** and **machine learning models** to identify which code modules are more likely to contain defects, helping improve software quality and maintenance efficiency.

---

## 📊 Exploratory Data Analysis (EDA)
Before building models, extensive data exploration was performed to understand structure, feature behavior, and relationships.

**Key analysis steps included:**
- **Distribution analysis** of numerical metrics (e.g., `loc`, `v(g)`, `n`, `e`, `d`, etc.)  
- **Correlation heatmap** to identify multicollinearity between McCabe and Halstead measures  
- **Outlier detection** using boxplots and quantile inspection  
- **Feature-target relationships** visualized through scatter and density plots  
- **Class imbalance check:** 80.65% defective vs 19.35% non-defective modules  
- **Feature importance exploration** using correlation and model-based ranking  

> The EDA revealed that metrics like **LOC**, **effort**, **volume**, and **complexity** show strong correlation with defect likelihood.

---

## 🧩 Dataset Information — NASA JM1 (PROMISE Repository)
The **NASA JM1** dataset is part of the **PROMISE Software Engineering Repository**, widely used for **software defect prediction research**.  
It contains **10,885 software modules** described by **22 static code metrics** derived from *McCabe* and *Halstead* complexity measures.

| Category | Description |
|-----------|-------------|
| **Code Metrics** | LOC, cyclomatic complexity *(v(g))*, essential complexity *(ev(g))*, design complexity *(iv(g))* |
| **Halstead Measures** | Volume, difficulty, effort, time, intelligence, etc. |
| **Comment Metrics** | Lines of code, comments, blank lines |
| **Target Variable** | `defects` — Boolean (true/false), indicates whether a module is defective |

**Class Distribution:**  
`false` → 2106 (19.35%) · `true` → 8779 (80.65%)

---

## ⚙️ Methodology (ML Pipeline Overview)
The project workflow integrates both **data analysis** and **predictive modeling**, structured as follows:

1. **Exploratory Data Analysis (EDA)** — descriptive statistics, visual correlations, and data distributions  
2. **Feature Engineering** — creation of two feature groups:  
   - **Set-A (Raw Metrics):** original McCabe & Halstead features  
   - **Set-B (Derived Ratios):** proportional relationships between complexity, volume, and effort  
3. **Model Training** — evaluation of four algorithms:  
   - XGBoost (Set-A)  
   - Logistic Regression (Set-B)  
   - Random Forest (Set-A)  
   - SVM (Set-B)  
4. **Hyperparameter & Threshold Optimization** —  
   Fine-tuning via `RandomizedSearchCV` and F1-based threshold tuning (≈ 0.347)  
5. **Evaluation Metrics** — ROC-AUC, PR-AUC, Accuracy, and Confusion Matrix  

---

## 📈 Model Overview

| Model | Dataset | ROC-AUC | PR-AUC | Note |
|--------|----------|:--------:|:--------:|------|
| **XGBoost** | Set-A | 0.724 | 0.405 | Best balance between recall and precision |
| **Logistic Regression** | Set-B | 0.706 | 0.405 | Simple and interpretable |
| **Random Forest** | Set-A | 0.716 | 0.404 | High accuracy, slightly lower recall |
| **SVM (RBF)** | Set-B | 0.700 | 0.346 | Lower PR performance |

---

## 📂 Project Files
| File | Description |
|------|--------------|
| `model_training_steps.md` | Detailed documentation of all ML steps |
| `bug_prediction_demo.ipynb` | Interactive Jupyter Notebook demo |
| `xgb_final.pkl` | Final trained model artifact |
| `bug_predict_config.json` | Configuration file (feature list, threshold) |
| `Images/` | Contains visual assets (EDA charts, SHAP plots, pipeline diagram) |

---

## 🙏 Acknowledgment
This dataset is provided by the  
**NASA Metrics Data Program (MDP)** and made publicly available through the  
**PROMISE Repository**.  

> 🔗 [http://promise.site.uottawa.ca/SERepository](http://promise.site.uottawa.ca/SERepository)

Dataset source: [NASA JM1 Dataset on Kaggle](https://www.kaggle.com/datasets/semustafacevik/software-defect-prediction)

---

## 📚 References
- Menzies, T. & Di Stefano, J. S. (2003). *How Good is Your Blind Spot Sampling Policy?* IEEE High Assurance Software Engineering Conference.  
- Menzies, T., DiStefano, J., Orrego, A., Chapman, R. (2004). *Assessing Predictors of Software Defects.* Workshop on Predictive Software Models.  
- McCabe, T. J. (1976). *A Complexity Measure.* IEEE Transactions on Software Engineering.  
- Halstead, M. H. (1977). *Elements of Software Science.* Elsevier.
# Nasa-JM1-defect-prediction-project
