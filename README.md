# Recipe Site Traffic Prediction Project

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Completed-success)

## Overview

This project is a practical data science exercise focused on predicting high-traffic recipes for a recipe website. The goal is to assist the product manager in identifying recipes that drive significant traffic, thereby optimizing homepage promotions and increasing overall site engagement. 

The analysis involves data validation and cleaning, exploratory data analysis (EDA), model development using classification algorithms, performance evaluation, and business-oriented recommendations. The primary task is binary classification: predicting whether a recipe will generate "High" traffic based on features like nutritional values (calories, carbohydrate, sugar, protein), category, and servings.

**Key Business Objectives:**
- Predict high-traffic recipes with at least 80% precision.
- Minimize false positives (avoid promoting low-traffic recipes as high-traffic).

**Submitted by:** DECHRAOUI Mohammed

This repository contains the Jupyter notebook (`notebook (6).ipynb`) with all code, outputs, visualizations, and explanations.

## Dataset

- **Source:** `recipe_site_traffic_2212.csv` (included in the repository).
- **Description:** Contains 947 recipes with columns:
  - `recipe`: Unique ID (int).
  - `calories`, `carbohydrate`, `sugar`, `protein`: Nutritional values (float, with 52 missing values each).
  - `category`: Recipe type (e.g., Pork, Potato, Breakfast; 11 unique categories).
  - `servings`: Number of servings (object, cleaned to int; values like "4 as a snack" stripped).
  - `high_traffic`: Target variable ("High" or NaN; 574 High, 373 low/missing; encoded as binary True/False).
- **Size:** 947 rows, 8 columns.
- **Issues Handled:** Missing values (imputed/excluded for modeling), data type conversions (servings to int, high_traffic to binary), no duplicates.

## Requirements

To run the notebook, you'll need Python 3.11+ and the following libraries (install via `pip install -r requirements.txt`):

- pandas
- numpy
- seaborn
- matplotlib
- scipy
- scikit-learn

**requirements.txt** (generated for convenience):
```
pandas==2.2.2
numpy==1.26.4
seaborn==0.13.2
matplotlib==3.9.2
scipy==1.14.1
scikit-learn==1.5.1
```

## Methodology

The project follows a structured data science pipeline:

### 1. Data Validation & Cleaning
- Inspected data types, shapes, and summaries using `.info()`, `.describe()`, and `.shape`.
- Checked for duplicates: None found.
- Handled missings: 52 in nutritional columns (imputed or dropped for modeling); 373 in `high_traffic` (treated as low traffic).
- Conversions: `servings` stripped of text (e.g., "4 as a snack" → 4) and cast to int; `high_traffic` encoded as binary.
- Verified unique values: e.g., 11 categories, servings range 1-6.

### 2. Exploratory Data Analysis (EDA)
- **Univariate Analysis:**
  - Countplot of `category`: High frequency in Pork, Potato, Breakfast.
  - Boxplot of `calories`: Right-skewed with outliers (>3000 calories).
- **Bivariate/Multivariate Analysis:**
  - Crosstab/barplot of `category` vs. `high_traffic`: High traffic in Vegetable (95%), Potato (82%), Pork (81%); Low in Beverages (24%).
  - Correlation heatmap: Weak correlations between nutritional features and traffic, but used as predictors.
- **Key Findings:** Category is the strongest predictor; nutritional data skewed; ~60% recipes are high-traffic.

### 3. Model Development
- **Problem Type:** Binary classification (predict `high_traffic`).
- **Features:** Nutritional values, one-hot encoded `category`, `servings`.
- **Models Selected:**
  - Baseline: Logistic Regression (interpretable, handles binary outcomes).
  - Comparisons: Decision Tree (non-linear decisions), Random Forest (ensemble robustness), SVM (boundary optimization).
- **Rationale:** Logistic for simplicity; Trees for interactions; SVM for imbalance handling.
- **Preprocessing:** Train-test split (80/20), scaling/one-hot encoding.
- Code snippets for fitting models (e.g., `logreg.fit(X_train, y_train)`).

### 4. Model Evaluation
- **Metrics:** Accuracy, Precision (primary, target ≥80%), Recall, F1-Score, Confusion Matrix.
- **Results:**
  - Logistic Regression: Accuracy 76.8%, Precision 80%, Recall 81.4%, F1 80.7% (balanced, no overfitting).
  - Decision Tree: Accuracy 67.4%, Precision 72.2% (overfitting).
  - Random Forest: Accuracy 73.7%, Precision 75.2% (overfitting).
  - SVM: Accuracy 66.3%, Precision 63.8% (underfitting).
- Best Model: Logistic Regression meets 80% precision goal.

### 5. Business Metrics
- **Proposed KPI:** High Traffic Conversion Rate (TP / FP from confusion matrix; target ≥4.0 for efficient promotion).
- **Performance:**
  - Logistic Regression: Train 4.09, Test 4.0 (meets KPI).
  - Others: Fail due to overfitting/underfitting.
- **Impact:** Reduces mispromotion, potentially boosting site traffic by prioritizing high-hit categories.

### 6. Final Summary & Recommendations
- **Summary:** Logistic Regression excels for reliable predictions; Category drives traffic (promote Vegetable/Potato/Pork, de-emphasize Beverages).
- **Recommendations:**
  1. Deploy Logistic Regression for real-time recipe scoring.
  2. Collect more data (e.g., prep time, ingredients, user session duration).
  3. Enhance features (e.g., more categories) and A/B test promotions.
  4. Monitor KPI quarterly; retrain with new data.

## How to Run

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/recipe-site-traffic-prediction.git
   cd recipe-site-traffic-prediction
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Launch Jupyter Notebook:
   ```
   jupyter notebook
   ```
   Open `notebook (6).ipynb` and run all cells.

4. View Results: Outputs include tables, plots, metrics, and KPI calculations.


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or collaborations, reach out to DECHRAOUI Mohammed at [dechraoui.mohammed78@gmail.com].

---

This README provides a professional overview of your work. Upload the notebook, dataset, and any generated images/plots to your GitHub repo. If you have specific images or additional files, reference them accordingly. Feel free to customize further!
