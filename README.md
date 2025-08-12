# Student Academic Stress Prediction

## Overview
This project predicts academic stress levels among students using a real-world dataset.  
Stress levels are represented as ordinal categories (1 = lowest stress, 5 = highest stress).  
Our primary evaluation metric is **Quadratic Weighted Kappa (QWK)**, chosen for its suitability in ordinal classification tasks.

## Objectives
- **Analyze** demographic, academic, and lifestyle factors influencing stress.
- **Build** predictive models to forecast stress levels accurately.
- **Optimize** models to achieve a target QWK score of **0.6 or higher**.
- **Evaluate** model performance on multiple metrics for a holistic view.

## Dataset
- Real-world student survey data.
- Features include demographics, academic workload, extracurricular activities, and lifestyle habits.
- Target variable: Stress level (1–5).

## Methodology
1. **Exploratory Data Analysis (EDA)**
   - Distribution analysis, correlation heatmaps, and categorical analysis.
2. **Feature Engineering**
   - One-Hot Encoding for categorical features (`sparse_output=False`).
   - Numerical features passed through after cleaning.
   - Unified transformation with `ColumnTransformer`.
3. **Model Selection**
   - Tested multiple regressors.
   - Selected top two performers: **RandomForest** and **CatBoost**.
4. **Custom QWK Scorer**
   - Predictions rounded & clipped before QWK calculation.
5. **Hyperparameter Tuning**
   - Performed `RandomizedSearchCV` with reduced parameter search for speed.
   - Stratified cross-validation to preserve class distribution.
6. **Final Evaluation**
   - Compared models on MAE, RMSE, R², and QWK.

## Results

### Cross-Validation QWK (Best Parameter Search)
| Model    | Best CV QWK |
|----------|-------------|
| CatBoost | 0.4406      |

### Test Set Performance (Tuned Models)
| Model       | MAE    | RMSE   | R²     | QWK    |
|-------------|--------|--------|--------|--------|
| RandomForest| 0.7289 | 0.9549 | 0.1693 | 0.5192 |
| CatBoost    | 0.7222 | 0.9061 | 0.2520 | 0.4949 |

## Conclusion
- **RandomForest** achieved the highest QWK on the test set (0.5192).
- Both models performed similarly in MAE and RMSE, with CatBoost slightly better in R².
- QWK target of 0.6 has not yet been reached.

## Future Work
- Engineer new interaction features and scale continuous variables.
- Explore ordinal-specific algorithms.
- Implement ensemble methods combining RandomForest and CatBoost.
- Perform feature selection to reduce noise and improve generalization.
