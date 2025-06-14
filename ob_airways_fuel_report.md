
# OB Airways Fuel Consumption Optimization Report

## Section 1: Overview

### 🎯 Problem Statement
OB Airways seeks to optimize flight fuel consumption by analyzing actual operational data and predicting the fuel required for planned flights. This will improve flight efficiency, reduce operational costs, and support sustainability goals.

### 📏 Metrics
To evaluate model performance, the following metrics were used:
- **MAE (Mean Absolute Error)**: Measures average magnitude of errors.
- **RMSE (Root Mean Square Error)**: Penalizes large errors more than MAE.
- **R² (R-squared)**: Measures proportion of variance explained by the model.

---

## Section 2: Analysis

### 📊 Data Exploration
Two datasets were provided:
- `actual_flights`: Real fuel consumption per flight.
- `flight_plan`: Planned fuel estimation and associated flight metadata.

Key features used included:
- Payload weight, air distance, flight duration, aircraft ID, departure/arrival airport, takeoff weight, etc.

### 📈 Data Visualization & Insights
Exploratory data analysis revealed:
- Strong correlation between planned flight hours and fuel consumption.
- Takeoff weight is a key driver of fuel needs.
- Some aircraft consistently use more fuel, possibly due to age or model.

Insights:
- Certain routes have consistently higher actual fuel than planned.
- Opportunities exist in refining flight plans for better alignment.

---

## Section 3: Methodology

### 🧹 Data Preprocessing
- Handled missing values (rows with missing fuel data were dropped).
- Converted timestamps to durations and extracted features like day, hour, etc.
- Scaled numerical features for ML models.

### ⚙️ Implementation
Three baseline models were tested:
- **Linear Regression**
- **Random Forest Regressor**
- **XGBoost Regressor**

Finally, a **Stacking Regressor** using `XGBoost` as base and `LinearRegression` as meta-model was developed for best results.

### 🔁 Refinement
- Used 5-fold cross-validation.
- Tuned hyperparameters manually and using validation scores.
- `StackingRegressor` set with `passthrough=True` for meta-model enrichment.

---

## Section 4: Results

| Model                      | MAE (kg) | RMSE (kg) | R²     |
|---------------------------|----------|-----------|--------|
| Linear Regression         | 1022.19  | 1505.89   | 0.9784 |
| Random Forest Regressor   | 540.76   | 944.51    | 0.9915 |
| XGBoost Regressor         | 459.80   | 875.69    | 0.9927 |
| **Stacking (XGBoost + LR)** | **393.88** | **772.12** | **0.9943** ✅ |

The stacking model achieved the best performance by combining the nonlinear learning capacity of XGBoost with the generalization ability of a linear model.

---

## Section 5: Conclusion

### 🔍 Reflection
This project addressed the challenge of predicting planned fuel consumption using historical flight data. Among all tested models, the stacking regressor delivered superior accuracy and generalization.

Key takeaways:
- Stacking improved results significantly over individual models.
- Even with moderate data size (~10,000 rows), stacking worked effectively.
- XGBoost captured non-linearities, while LinearRegression adjusted biases.

### 🚀 Improvement Suggestions
- Add weather data, aircraft age, and airport conditions as features.
- Use SHAP or LIME for interpretability.
- Deploy as an API for integration into flight planning tools.
- Consider time-aware validation for real-world deployment.

---

📌 *Prepared by a Data Scientist with 20 years of experience.*
