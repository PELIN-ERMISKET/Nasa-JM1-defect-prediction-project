
## Model Training Steps – NASA JM1 Defect Prediction

1) Overview

This document summarizes the training process built to predict defective software modules using NASA JM1 software metrics.
Compared models: XGBoost, Logistic Regression, SVM, Random Forest

2) Data & Split

Dataset: jm1.csv

Target: defects (0/1)

Split: train_test_split(test_size=0.2, random_state=42, stratify=y)

3) Feature Engineering
Set-A

Raw metrics (e.g., loc, v(g), iv(g), n, v, l, d, i, e, IOComment, IOBlank, etc.)

Set-B (Derived Ratios)
loc_per_branch        = loc / (branchCount + 1)
complexity_density    = v(g) / (loc + 1)
effort_per_loc        = e / (loc + 1)
difficulty_per_loc    = d / (loc + 1)
vocabulary_per_loc    = n / (loc + 1)
op_to_opnd_ratio      = total_Op / (total_Opnd + 1)
uniq_op_ratio         = uniq_Op / (total_Op + 1)
uniq_opnd_ratio       = uniq_Opnd / (total_Opnd + 1)


Missing values handled with fillna(0)

Scaling applied using StandardScaler (for Set-B models)

4) Modeling
4.1 XGBoost (Set-A)

Class imbalance: handled via scale_pos_weight

Hyperparameter tuning: performed with RandomizedSearchCV
Best parameters:

{'subsample': 1.0, 'scale_pos_weight': 4, 'n_estimators': 400,
 'min_child_weight': 1, 'max_depth': 8, 'learning_rate': 0.01,
 'gamma': 0.3, 'colsample_bytree': 1.0}


Threshold optimization: F1-max threshold from PR curve ≈ 0.347

Test Results:

ROC-AUC: 0.7236

PR-AUC: 0.4053

Accuracy: 0.7478

Confusion Matrix (tuned):

 ![Feature Importance Plot](XGBoost_Tuned_New_Threshold.png)


4.2 Logistic Regression (Set-B)

Parameters: class_weight='balanced', solver='lbfgs'

F1-max threshold ≈ 0.540

ROC-AUC: 0.7064, PR-AUC: 0.4048, Accuracy: 0.7170

4.3 SVM (RBF, Set-B)

Parameters: class_weight='balanced', probability=True

F1-max threshold ≈ 0.208

ROC-AUC: 0.7005, PR-AUC: 0.3456, Accuracy: 0.6991

4.4 Random Forest (Set-A)

Parameters: n_estimators=400, class_weight='balanced'

ROC-AUC: 0.7162, PR-AUC: 0.4037, Accuracy: 0.8025

4.5 Model Comparison (Test)

Model	                    ROC-AUC	                   PR-AUC                 	Notes
XGBoost 	                 0.724	                    0.405	                Best overall balance
Logistic Regression          0.706                  	0.405               	Simple & effective
Random Forest	             0.716	                    0.404	                High accuracy, low recall
SVM (RBF)                  	 0.700	                    0.346	                Lower PR performance

5) Threshold Effect & Confusion Matrices

XGBoost (default threshold = 0.5):

[[1429, 327],
 [231, 190]]

![Feature Importance Plot](XGBoost_Confusion_Matrix.png)

XGBoost (tuned threshold ≈ 0.347):

[[1412, 344],
 [205, 216]]

![Feature Importance Plot](XGBoost_Tuned_New_Threshold.png)

Lowering the threshold increases recall for defective modules but slightly increases false positives.

6) Feature Importance (Explainability)

XGBoost feature importance / SHAP revealed top contributing metrics:
loc, IOBlank, total_Op, d, v, total_Opnd, IOComment, IOCode, etc.

SHAP summary plot shows higher loc and related density values increase defect probability.

7) Saved Artifacts

Model: xgb_final.pkl

Config: bug_predict_config.json (feature list, threshold, etc.)

Demo Notebook: bug_prediction_demo.ipynb

8) Execution
# Environment
pip install -r requirements.txt  # (xgboost, scikit-learn, shap, matplotlib, seaborn, pandas, numpy)

# Demo
jupyter notebook bug_prediction_demo.ipynb

9) Conclusion

XGBoost achieved the best overall trade-off between precision and recall.

For production use: XGBoost + F1-max threshold (≈0.347) + SHAP interpretability is recommended.

