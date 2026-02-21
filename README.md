# 🚗 Used Car Market Value Prediction | Rusty Bargain

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)

This project was developed for the used car sales service **Rusty Bargain**. The goal is to build an app that allows users to quickly find the market value of their vehicles based on historical data, technical specifications, and trim versions.

## 🎯 Business Objectives
Rusty Bargain's evaluation is based on three pillars:
1. **Prediction Quality:** Minimize the error (RMSE).
2. **Prediction Speed:** The model must provide prices quickly for the end-user.
3. **Training Time:** Efficient training cycles for model maintenance.

---

## 📊 Dataset Overview
The dataset contains historical data on used cars, including:
- **Target:** `Price` (Euros)
- **Features:** `VehicleType`, `RegistrationYear`, `Gearbox`, `Power`, `Model`, `Mileage`, `FuelType`, `Brand`, and `NotRepaired`.

### Key Preprocessing Steps:
- **Outlier Removal:** Filtered anomalous values in `Power` (10-1000 hp) and `RegistrationYear` (1900-2025).
- **Feature Engineering:** Created the `CarAge` column to capture the vehicle's age.
- **Dimensionality Reduction:** Grouped rare car models (outside the top 20) into an 'other' category.
- **Missing Values:** Handled unknown categorical data by tagging them as `'unknown'`, preserving information from non-responses in features like `NotRepaired`.

---

## 🔍 Exploratory Data Analysis (EDA)

During the EDA, we observed:
- A strong **negative correlation** (-0.39) between mileage and price.
- A **positive correlation** (0.50) between engine power and price.
- Higher market values for **SUVs and Sports cars** compared to small utility vehicles.
- Price distribution is **right-skewed**, with most cars priced below €10,000.

---

## 🏗️ Model Performance
We evaluated several models using a 75/25 train-test split and Cross-Validation for the baseline.

| Model | RMSE (Validation) | Training Time | Prediction Speed |
| :--- | :---: | :---: | :---: |
| **Linear Regression** | 2945.98 | **0.02s** | **0.0028s** |
| **Ridge (CV=5)** | 3219.41 | 0.08s | 0.0050s |
| **Decision Tree** | 1840.30 | 3.39s | 0.0490s |
| **Random Forest** | **1811.81** | 41.36s | 0.1167s |

### Final Model Selection: Random Forest
The **Random Forest Regressor** achieved the best predictive quality with an **RMSE of 1811.81**. Although it requires more training time (~41s) than simpler models, its prediction speed (0.11s) is well within the requirements for a real-time app, and it offers the best balance between accuracy and robustness.



---

## 🛠️ Key Technical Insights

- **Feature Importance:** The most influential factors in determining price were **Power**, **Car Age (Registration Year)**, and **Mileage**.
- **Data Pipeline:** Used `ColumnTransformer` and `Pipeline` from Scikit-Learn to ensure clean, reproducible, and leak-free data transformations.
- **Modern Metrics:** Implemented `root_mean_squared_error` from the latest `sklearn.metrics` for precise evaluation.

---

## 📈 Next Steps
- [ ] **Hyperparameter Tuning:** Use `RandomizedSearchCV` to optimize `n_estimators` and `max_depth` for the Random Forest.
- [ ] **Gradient Boosting:** Implement **CatBoost** (already imported in the project) to compare if it can reduce RMSE further with faster training.
- [ ] **Deployment:** Wrap the model in a FastAPI or Streamlit app for a live demo.

---

## 👤 Author
**Pedro Albuquerque**
*Business-Driven Data Analyst & BI Specialist* 

---

## 🤝 Contact
[![LinkedIn](https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/phaa/)