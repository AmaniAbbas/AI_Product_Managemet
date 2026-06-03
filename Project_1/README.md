# Machine Learning Foundations for Product Managers

## Power Plant Energy Output Prediction

### Project Overview

In this project, I built and evaluated machine learning models to predict the electrical energy output of a Combined Cycle Power Plant using environmental sensor readings.

This project was completed using two approaches:

* **Google Sheets** for exploratory data analysis, manual model building, and understanding the modeling process step by step.
* **Python (Jupyter Notebook)** using pandas and scikit-learn to implement the same workflow using industry-standard tools.

### Resources

* **Dataset:** `CCPP_data.csv`
* **Google Sheets Analysis:** [LINK HERE](https://docs.google.com/spreadsheets/d/11DVdXxi5TWKTAyX4DJJtx_AdBYMkeUCXJUcz08cieN8/edit?usp=sharing)
* **Python Notebook:** `ccpp_power_plant_project.ipynb`

---

### Dataset Description

The dataset contains **9,568 hourly observations** collected from sensors at a Combined Cycle Power Plant.

Features:

* **AT (Temperature):** 1.81°C – 37.11°C
* **AP (Ambient Pressure):** 992.89 – 1033.30 millibar
* **RH (Relative Humidity):** 25.56% – 100.16%
* **V (Exhaust Vacuum):** 25.36 – 81.56 cm Hg

Target:

* **PE (Net Hourly Electrical Energy Output):** 420.26 – 495.76 MW

The dataset contained a very small number of missing values, which were identified during the data understanding phase.

---

### Problem Definition

The goal is to predict the plant's electrical energy output (**PE**) based on environmental conditions.

This is a:

* **Supervised Learning** problem because historical inputs and target values are available.
* **Regression** problem because the target is a continuous numerical value.

Features (**X**):

* AT
* V
* AP
* RH

Target (**Y**):

* PE

---

### Exploratory Data Analysis (EDA)

Before building any models, I explored the dataset using:

* Descriptive statistics
* Scatter plots
* Correlation analysis

Key observations:

* **AT (Temperature)** showed the strongest negative relationship with PE.
* **V (Exhaust Vacuum)** also showed a strong negative relationship.
* **AP** and **RH** appeared to have weaker individual relationships with PE.

Correlation values:

| Feature | Correlation with PE |
| ------- | ------------------- |
| AT      | -0.948              |
| V       | -0.870              |
| AP      | 0.518               |
| RH      | 0.390               |

---

### Data Split

The dataset was split into:

* **Training Set:** 80%
* **Test Set:** 20%

The training set was used for model training and comparison, while the test set was reserved for final evaluation on unseen data.

---

### Models Compared

#### Model 1 — Multiple Linear Regression (AT + V + AP + RH)

Reasons for choosing this model:

* Strong baseline model
* Easy to interpret
* Common starting point for regression problems

#### Model 2 — Multiple Linear Regression (AT + V)

This model uses only the two features that appeared strongest during exploratory analysis.

The goal was to determine whether reducing the feature set would improve or hurt model performance.

---

### Evaluation Metrics

The following regression metrics were used:

* **RMSE (Root Mean Squared Error):** Measures average prediction error while penalizing larger errors more heavily.
* **MAE (Mean Absolute Error):** Average absolute prediction error.
* **R² (Coefficient of Determination):** Measures how much variation in the target variable is explained by the model.

RMSE was used as the primary metric when comparing models.

---

### Results

#### Model 1 — AT + V + AP + RH

| Dataset  | MAE  | RMSE | R²    |
| -------- | ---- | ---- | ----- |
| Training | 3.61 | 4.53 | ~0.93 |
| Test     | 3.69 | 4.68 | ~0.93 |

---

#### Model 2 — AT + V

| Dataset  | MAE  | RMSE | R²    |
| -------- | ---- | ---- | ----- |
| Training | 3.91 | 4.94 | ~0.92 |
| Test     | 3.95 | 5.03 | ~0.92 |

---

### Final Model Selection

I selected **Model 1 (AT + V + AP + RH)** as the final model because it achieved the lowest RMSE and MAE on both the training and test datasets.

One interesting finding was that although **AP** and **RH** appeared weaker during exploratory analysis, including them improved overall model performance. This demonstrates an important machine learning principle: features that appear less useful individually can still provide valuable predictive information when combined with other variables.

---

### Key Learning Outcomes

This project helped me practice the complete machine learning modeling workflow:

* Problem definition
* Data understanding
* Exploratory data analysis
* Feature selection
* Train/test splitting
* Model training
* Model comparison
* Model evaluation
* Communicating results

Most importantly, it reinforced the importance of validating assumptions with data rather than relying solely on initial observations.
