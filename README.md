# Relax Inc. User Adoption Prediction

## Project Overview

Customer adoption is a critical driver of long-term business success for subscription-based software platforms. In this project, I developed a machine learning model to predict whether a newly registered Relax Inc. user would become an **adopted user** using only information available at the time the account was created.

The project was completed as a take-home data science challenge and demonstrates a complete end-to-end machine learning workflow, including data engineering, exploratory data analysis, feature engineering, model development, statistical inference, and business recommendations.

---

## Business Problem

Relax Inc. wanted to identify which newly registered users were most likely to become long-term adopted users. Early identification would allow the company to improve onboarding strategies, prioritize customer success efforts, and ultimately increase user retention.

An **adopted user** was defined as a user who logged into the platform on **three separate days within any rolling seven-day period**, following the definition provided in the challenge.

A key requirement of the project was that predictions could only use information available **when a user account was created**, making the resulting model applicable to new users.

---

## Project Workflow

- Created the adoption target variable from user login history
- Merged account information with login-derived outcomes
- Performed exploratory data analysis (EDA)
- Engineered and evaluated candidate features
- Removed redundant and potential data leakage variables
- Encoded categorical variables and standardized predictors where appropriate
- Compared multiple supervised machine learning models
- Performed limited hyperparameter tuning
- Selected the best-performing model
- Interpreted model coefficients, odds ratios, and statistical significance
- Developed business recommendations based on the results

---

## Models Evaluated

- Logistic Regression
- Random Forest
- Gradient Boosting
- Support Vector Machine

Model performance was evaluated using:

- ROC AUC
- Balanced Accuracy
- Precision
- Recall
- F1 Score
- Accuracy

Because the dataset was imbalanced, model selection emphasized **ROC AUC** and **Balanced Accuracy** rather than overall accuracy alone.

---

## Key Findings

- **Account creation source** was the strongest predictor of long-term user adoption.
- Users joining through **Guest Invites**, **Organization Invites**, **Direct Signup**, and **Google Authentication** were significantly more likely to become adopted users than users creating Personal Projects.
- **Organization size** had a statistically significant but relatively small effect.
- Marketing preferences collected during registration were **not significant predictors** of adoption.
- Logistic Regression provided the best balance of predictive performance and model interpretability.

---

## Business Recommendations

The analysis suggests several opportunities to improve user adoption:

- Encourage invitation-based onboarding and collaborative account creation.
- Improve the onboarding experience for users creating Personal Projects.
- Focus product improvements on early user engagement rather than marketing email preferences.
- Collect richer behavioral data during users' first weeks on the platform to improve future predictive models.

---

## Technologies Used

- Python
- pandas
- NumPy
- scikit-learn
- statsmodels
- matplotlib
- seaborn
- Jupyter Notebook

---

## Repository Structure

```
├── data/
├── notebooks/
├── README.md
└── requirements.txt
```

---

## Author

**Daryl Morris**

Senior Data Scientist | Statistician | Software Engineer

This project was completed as part of the Springboard Data Science Career Track and demonstrates an end-to-end machine learning workflow, emphasizing both predictive modeling and interpretable, data-driven business decision making.
