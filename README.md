# Predictive-Modelling-of-Housing-Prices-Using-CRISP-DM-in-R
This project applies the CRISP-DM framework to a structured housing dataset to forecast **property sale prices** and evaluate price appreciation potential. Using R programming, multiple regression models were developed and evaluated, with the final model selected based on performance metrics and business alignment.
---

## CRISP-DM Phases
### 1. Business Understanding
- **Objective:** Maximise ROI by predicting property prices and identifying undervalued properties.
- **Business Success Criteria:**
  - Accurate sale price predictions (low MAE)
  - Identification of key investment opportunities
  - Insights into seasonal sales trends

### 2. Data Understanding
- Dataset contains property listings within the same region.
- Key features: location proximity (e.g., `OCEAN_DIST`, `CNTR_DIST`), structure quality, floor area, sale month.
- No missing or null values.
- Seasonal trends show **June as the peak sale month**, suggesting marketing strategy alignment.

### 3. Data Preparation & Feature Engineering
- **Duplicates** removed using `PARCELNO`
- Dropped irrelevant fields (e.g., `LATITUDE`, `LONGITUDE`, `avno60plus`)
- Engineered features based on correlation to `SALE_PRC`
- Applied correlation threshold (≥ 0.3) to remove weak predictors
- Final dataset ready for modelling

### 4. Modelling
Eight models were built using the training data (70/30 split):
- **Linear Regression**
- **Support Vector Regression (Linear + Poly)**
- **Decision Tree**
- **Random Forest (100, 200, 500 trees)**
- **Gradient Boosting**

#### 🎯 Model Performance Metric: Mean Absolute Error (MAE)

| Model               | MAE (Lower = Better) |
|---------------------|----------------------|
| Linear Regression   | Moderate             |
| SVR (Linear)        | Moderate             |
| SVR (Poly)          | Moderate             |
| Decision Tree       | Moderate             |
| **Random Forest (100 Trees)** | **Lowest MAE** ✅ |
| Random Forest (200/500 Trees) | Slightly higher MAE |
| Gradient Boosting   | Competitive          |

### 5. Model Tuning
- **Hyperparameter tuning** on the Random Forest model using `caret::train()`
- Parameters: `mtry`, `min.node.size`, `splitrule = "variance"`
- **5-fold Cross Validation** applied to reduce overfitting
- Tuned model showed **slightly improved accuracy** over the default

### 6. Evaluation
- The tuned Random Forest model was evaluated on a real-world test case.
- It predicted the property price of a parcel accurately (`≈1.35 million`).
- Model aligned with both technical goals (low MAE) and business objectives (investment insights & appreciation forecasting).

---


### 🧩 Integration
- Deploy model (`best_model.rds`) via **Shiny** or **Azure ML Web Service**
- Input features return a predicted price in real-time

### 🔄 Data Pipeline
- Automated input from property databases or APIs
- Keeps model up-to-date with new listings and trends

### 🖥️ User Interface
- Simple UI for non-technical users (e.g., analysts, realtors)
- Input fields: land area, structure quality, distance to city/ocean, etc.

### 📄 Documentation
- Technical and user guides for onboarding and model usage

---

## 🔍 Key Insights

- **Random Forest with 100 Trees** was the best-performing model (lowest MAE)
- **Land Area, Living Space, and Structure Quality** were top predictors
- **Seasonal trends** (sales peak in June, low in January) are useful for marketing
- **Geospatial proximity** (to ocean/centres) affects property value
- Model generalised well and is suitable for real-world deployment

---

## 🛠️ Tools & Libraries

- **Language:** R
- **Libraries:** `tidyverse`, `ggplot2`, `caret`, `randomForest`, `e1071`, `gbm`, `rpart`
- **Framework:** CRISP-DM
- **Deployment Plan:** Shiny + Azure ML
---

## 📈 Future Improvements

- Use larger or multi-region datasets
- Introduce geospatial modelling (e.g., spatial interpolation)
- Automate hyperparameter tuning via Bayesian or grid search
- Improve UI for stakeholder-facing deployment

---
