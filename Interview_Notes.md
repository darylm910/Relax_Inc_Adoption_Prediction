# Relax Inc. Take-Home Challenge
## Interview Preparation Notes

---

# 1. Tell me about this project.

### Goal
- Predict which newly registered users will become long-term adopted users.
- Use **only information available when the account is created** so the model could be used immediately for new users.
- Identify actionable factors that influence adoption and provide business recommendations.

### Dataset
- Two datasets:
  - User account information
  - User login history
- Created the target variable from the login history.
- Final predictors came only from account creation data.

### Workflow
- Built the adoption label.
- Performed exploratory data analysis.
- Engineered and evaluated features.
- Removed redundant and potential leakage variables.
- Compared four supervised machine learning models.
- Performed limited hyperparameter tuning.
- Selected Logistic Regression.
- Interpreted coefficients, odds ratios, and statistical significance.
- Developed business recommendations.

### Key Findings
- Account creation source was the strongest predictor of adoption.
- Organization size had a statistically significant but relatively small effect.
- Marketing preferences were not significant predictors.
- Logistic Regression provided the best balance of predictive performance and interpretability.

### Business Takeaway
- Improve onboarding.
- Encourage invitation-based adoption.
- Improve the experience for Personal Project users.
- Collect richer behavioral data for future models.

---

# 2. What was the business problem?

### Business Problem
Relax wanted to identify which newly registered users were most likely to become long-term adopted users.

### Why it matters
- User acquisition is expensive.
- Adoption drives long-term customer retention.
- Early identification allows targeted onboarding and customer success efforts.

### Important Constraint
The model could only use information available **when the account was created**, making it suitable for predicting adoption for new users.

---

# 3. How did you define an adopted user?

### Business Definition
An adopted user was defined as a user who logged into the product:

- on **three separate days**
- within **any rolling seven-day period**

### My Approach
- Processed the login history.
- Aggregated login activity by user.
- Created a binary adoption variable.
- Merged the outcome back into the user dataset for modeling.

---

# 4. Walk me through your workflow.

1. Understand the business problem.
2. Load and inspect both datasets.
3. Engineer the adoption outcome.
4. Merge the datasets.
5. Perform exploratory data analysis.
6. Engineer candidate features.
7. Remove redundant and leakage variables.
8. Encode categorical predictors.
9. Standardize features where appropriate.
10. Split into training and testing sets.
11. Train four classification models.
12. Perform limited hyperparameter tuning.
13. Compare model performance.
14. Perform statistical inference using Logistic Regression.
15. Translate results into business recommendations.

---

# 5. Why did you choose those models?

### Logistic Regression
- Strong baseline classification model.
- Highly interpretable.
- Produces coefficients, odds ratios, confidence intervals, and p-values.

### Random Forest
- Captures nonlinear relationships.
- Handles interactions automatically.
- Provides feature importance.

### Gradient Boosting
- Often performs well on structured tabular data.
- Good benchmark against ensemble methods.

### Support Vector Machine
- Effective classification algorithm.
- Can capture more complex decision boundaries.

### Why compare multiple models?
- Never assume one algorithm is best.
- Evaluate several approaches.
- Let the data determine the best model.

---

# 6. How did you evaluate the models?

### Metrics Used
- ROC AUC
- Balanced Accuracy
- Precision
- Recall
- F1 Score
- Accuracy

### Why not rely on Accuracy?
The dataset was imbalanced.

A model predicting mostly non-adopted users could achieve relatively high accuracy while failing to identify adopted users.

ROC AUC and Balanced Accuracy provided a more meaningful evaluation.

---

# 7. Why did Logistic Regression win?

### Predictive Performance
- Highest ROC AUC.
- Comparable performance to Support Vector Machine.
- Outperformed Random Forest and Gradient Boosting.

### Interpretability
Could explain:
- coefficients
- odds ratios
- confidence intervals
- statistical significance

### Business Value
Business stakeholders often want to understand *why* predictions are made, not simply receive a prediction.

Logistic Regression provided both reasonable predictive performance and clear explanations.

---

# 8. What did you learn from the project?

### Main Finding
Account creation source was the strongest predictor of long-term adoption.

### Other Findings
- Organization size had a modest negative association.
- Marketing preferences were not significant predictors.

### Overall Lesson
The user's onboarding experience appears to have a greater influence on adoption than marketing preferences collected during registration.

---

# 9. What would you do next?

### Improve the Feature Set
Collect behavioral information such as:
- first-week activity
- number of login sessions
- feature usage
- invitations sent
- collaboration activity
- time spent in the product

### Additional Modeling
- Optimize probability thresholds.
- Perform temporal validation.
- Compare additional algorithms (e.g., XGBoost).
- Monitor performance after deployment.

---

# 10. What were the biggest challenges?

### Engineering the Target Variable
The adoption outcome had to be created from raw login history rather than being provided.

### Avoiding Data Leakage
Carefully ensured only account creation variables were used as predictors.

### Class Imbalance
Required selecting evaluation metrics beyond simple accuracy.

### Feature Selection
Removed redundant predictors to improve interpretability and avoid unnecessary complexity.

---

# 11. If you had another month?

I would:

- collect richer behavioral features
- optimize probability thresholds
- evaluate calibration
- investigate SHAP explanations
- compare additional boosting algorithms
- perform temporal validation
- build a deployment pipeline for new users

---

# 12. What recommendation would you give Relax?

### Recommendation 1
Improve the onboarding experience.

### Recommendation 2
Encourage invitation-based adoption through collaborative workflows.

### Recommendation 3
Improve engagement for users creating Personal Projects.

### Recommendation 4
Place less emphasis on marketing email preferences during registration.

### Recommendation 5
Collect richer behavioral data to improve future prediction models.

---

# 13. What are you most proud of?

Rather than simply building several machine learning models, I'm most proud of approaching the project as a complete data science workflow.

Specifically:

- Engineering the adoption outcome from raw login history.
- Being careful to avoid data leakage.
- Comparing multiple modeling approaches instead of assuming one would perform best.
- Selecting the final model based on both predictive performance and interpretability.
- Translating the statistical results into practical business recommendations.

---

# 14. How did your background in biostatistics influence this project?

My background strongly influenced how I approached the analysis.

Rather than focusing only on maximizing predictive performance, I emphasized building a model that was both statistically rigorous and useful for decision-making.

Specifically, I:

- Carefully avoided data leakage by limiting predictors to information available at account creation.
- Selected evaluation metrics appropriate for an imbalanced dataset rather than relying solely on accuracy.
- Performed statistical inference using confidence intervals, odds ratios, and significance testing.
- Balanced predictive performance with model interpretability.
- Focused on producing actionable business recommendations rather than simply identifying the highest-performing algorithm.



# Relax Inc. Take-Home Challenge
## Phase 2 – Technical Deep Dive

---

# 1. Why did you define an adopted user that way?

### Answer
- I used the business definition provided in the case study.
- An adopted user logged into the product on **three separate days within any rolling seven-day period.**
- This ensured my outcome matched the business objective rather than creating my own arbitrary definition.
- I engineered this outcome from the login history before any modeling began.

---

# 2. Why did you use organization_size instead of org_id?

### Answer
- Organization ID is simply an identifier.
- Machine learning models could incorrectly treat organization IDs as meaningful numeric values.
- Organization size contains actual business information about the user's environment.
- It is much more likely to generalize to unseen organizations.

---

# 3. Why didn't you use last_session_creation_time?

### Answer
- That information occurs after account creation.
- The goal was to predict adoption for a brand-new user.
- Using future activity would introduce **data leakage.**
- I intentionally limited predictors to variables available when the account was created.

---

# 4. Why did you remove was_invited?

### Answer
- The information was already contained in the creation_source variable.
- Including both variables would introduce redundant information.
- Removing redundant predictors simplified the model while preserving interpretability.

---

# 5. Why didn't you use duplicate names or email domains?

### Answer
- They were not likely to generalize well.
- They introduce unnecessary complexity.
- They may capture organization-specific artifacts rather than meaningful behavioral patterns.
- I preferred predictors with clear business interpretation.

---

# 6. Why compare multiple machine learning models?

### Answer
- Different algorithms make different assumptions.
- There is no universally best classifier.
- Comparing several models allows the data to determine which performs best.
- It also demonstrates that model selection was evidence-based rather than arbitrary.

---

# 7. Why did Logistic Regression outperform Random Forest?

### Answer
- The relationships appeared to be relatively simple and approximately linear.
- The dataset contained only a modest number of predictors.
- Random Forest can overfit smaller datasets when little nonlinear structure exists.
- Logistic Regression generalized slightly better and produced the highest ROC AUC.

---

# 8. What were the strongest predictors?

### Answer
- Account creation source was clearly the strongest predictor.
- Guest Invite
- Google Authentication
- Direct Signup
- Organization Invite

Other observations:
- Organization size had a statistically significant but small effect.
- Marketing preferences were not significant.

---

# 9. What were the limitations?

### Answer
- Limited predictor variables.
- No behavioral usage information.
- Class imbalance.
- Moderate predictive performance.
- Results show associations rather than causation.

---

# 10. What would you do next?

### Answer
I would collect:

- first-week activity
- feature usage
- session counts
- collaboration metrics
- invitations accepted
- early engagement statistics

I would also:

- optimize thresholds
- evaluate calibration
- perform temporal validation
- compare additional models

---

# 11. Why did you use StandardScaler?

### Answer
- Logistic Regression and Support Vector Machine perform better when predictors are on similar scales.
- Standardization prevents variables with larger numeric ranges from dominating optimization.
- Scaling was performed using only the training data to avoid data leakage.

---

# 12. Why didn't Random Forest require scaling?

### Answer
- Tree-based models split on feature values.
- They are generally insensitive to feature scale.
- Scaling primarily benefited Logistic Regression and SVM.

---

# 13. Why did you use one-hot encoding?

### Answer
- Machine learning models require numeric inputs.
- One-hot encoding avoids imposing an artificial ordering on categorical variables.
- It allows each category to have its own independent effect.

---

# 14. Why didn't you oversample with SMOTE?

### Answer
- The class imbalance was moderate rather than extreme.
- I evaluated models using metrics appropriate for imbalanced data.
- I preferred to avoid introducing synthetic observations unless necessary.
- Additional experimentation with resampling could be explored in future work.

---

# 15. Why ROC AUC instead of Accuracy?

### Answer
- Accuracy can be misleading for imbalanced datasets.
- ROC AUC evaluates how well the model separates adopted from non-adopted users across all classification thresholds.
- It provides a better overall assessment of classifier performance.

---

# 16. Why Balanced Accuracy?

### Answer
- It gives equal weight to both classes.
- It prevents performance on the majority class from dominating the evaluation.
- It is especially useful when one class is less common.

---

# 17. Why Precision and Recall?

### Answer
- Precision measures how many predicted adopters actually became adopters.
- Recall measures how many actual adopters the model successfully identified.
- Together they provide more insight than overall accuracy.

---

# 18. Why F1 Score?

### Answer
- F1 balances Precision and Recall.
- It is useful when both false positives and false negatives matter.
- It summarizes classification performance with a single metric.

---

# 19. Why did Gradient Boosting predict all negatives?

### Answer
- The default probability threshold of 0.5 resulted in all predictions falling below the cutoff.
- Although its ROC AUC was better than random, its probability calibration at that threshold was poor.
- This illustrates why ROC AUC and threshold-dependent metrics should both be considered.

---

# 20. Why did you perform only limited hyperparameter tuning?

### Answer
- The objective was to compare several modeling approaches rather than exhaustively optimize one algorithm.
- Limited tuning improved performance while keeping the analysis focused and computationally efficient.
- More extensive tuning could be explored in future work.

---

# 21. Why was interpretability important?

### Answer
- The objective was not only to predict adoption but also to understand what influences adoption.
- Business stakeholders benefit from knowing why predictions are made.
- Logistic Regression provides interpretable coefficients, odds ratios, confidence intervals, and p-values.

---

# 22. Why did you use odds ratios?

### Answer
- Odds ratios are easier for business audiences to interpret than raw coefficients.
- They quantify how the odds of adoption change for each predictor.
- Values above 1 indicate increased odds, while values below 1 indicate decreased odds.

---

# 23. Why include confidence intervals?

### Answer
- Confidence intervals quantify uncertainty.
- They show the plausible range of effect sizes.
- They help distinguish statistically meaningful findings from unstable estimates.

---

# 24. Why perform statistical inference after machine learning?

### Answer
- Machine learning identified the best predictive model.
- Statistical inference helped explain why the model behaved as it did.
- Combining predictive modeling with inference produced both accurate predictions and actionable insights.

---

# 25. How did your background in biostatistics influence this project?

### Answer
- I focused on avoiding data leakage.
- I selected evaluation metrics appropriate for an imbalanced dataset.
- I emphasized statistical inference rather than only predictive accuracy.
- I balanced predictive performance with interpretability.
- I translated the technical findings into business recommendations rather than stopping at model evaluation.