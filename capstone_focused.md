**Capstone Project Focus Areas**
Module 8 → feature engineering, overfitting, validation
Module 9 → cross-validation, GridSearchCV, regularization
Module 12 → metrics, thresholds, precision/recall/ROC
Module 13 → Logistic Regression baseline
Module 14 → Decision Trees
Module 20 → Random Forest + Gradient Boosting

Useful but secondary: Module 15 for bias-variance/optimization and Module 16/17 for comparing classifiers.

**1. Business Problem and Decisioning**
Define the objective clearly:
Predict whether an online-payment transaction is fraudulent and convert the fraud probability into an approve, review, or decline decision.
Explain the business trade-offs:
Missed fraud creates financial loss.
False positives reject legitimate customers.
Manual reviews create operational cost.
Describe the project as an online-payment fraud risk-decisioning capstone. Do not claim direct production PayFac, PSP, acquirer, or PayPal experience.
**2. Data Understanding and Quality**
Document:
Dataset size and fraud percentage
Available columns
Missing values and duplicates
Fraud distribution by transaction type
Fraud distribution by amount and time
Sender and receiver behavior
Potential data leakage, especially isFlaggedFraud
Potentially useful features:
amount
type
step
Sender balance
Receiver balance
Transaction frequency
Repeated transaction behavior
Balance-difference features
**3. Exploratory Data Analysis and Feature Engineering**
Create visualizations for:
Fraud versus legitimate transaction counts
Fraud rate by transaction type
Transaction-amount distributions
Fraud rate over time
Sender and receiver balance behavior
Correlations and feature relationships
Engineer features such as:
log_amount
time_bucket
balance_difference
sender_transaction_count
receiver_transaction_count
same_sender_frequency
same_receiver_frequency
Explain why each feature may help identify fraud.
**4. Learning Type and Modeling**
The project uses:
Supervised learning
Binary classification
Target: isFraud
Output: Fraud probability and fraud/legitimate prediction
Compare:
Logistic Regression as an interpretable baseline
Random Forest as a nonlinear ensemble model
XGBoost as the primary tabular-data model
Because fraud is highly imbalanced, use class weights or imbalance-handling techniques only on the training data.
**5. Model Evaluation**
Do not rely on accuracy alone.
Use:
Precision
Recall
F1-score
PR-AUC
ROC-AUC
Confusion matrix
False-positive rate
Estimated fraud loss
Approval rate
Manual-review rate
Evaluate multiple thresholds instead of automatically using 0.50.
Example:
Low risk       Approve
Medium risk    Review
High risk      Decline
Select the threshold based on:
Fraud cost
False-positive cost
Manual-review capacity
Desired approval rate
**6. Error Analysis and Explainability**
Analyze:
False positives
False negatives
Fraud patterns missed by the model
Feature importance
Model behavior across transaction types
Use SHAP explanations if appropriate.
The goal is not only to maximize a metric, but also to understand why the model makes each decision and what business impact it creates.
**7. Full ML Lifecycle**
Demonstrate the complete workflow:
Data ingestion
→ Data validation
→ Feature engineering
→ Model training
→ Model evaluation
→ Model selection
→ Threshold selection
→ Inference
→ Monitoring
→ Retraining
**8. Monitoring and Retraining**
Monitor:
Fraud-rate changes
Feature drift
Transaction-volume changes
Precision and recall degradation
Prediction-score distribution
Data-quality failures
Define when investigation or retraining should be triggered.
**9. Deployment Architecture**
Only claim GCP implementation if you actually build it. Otherwise describe it as a proposed or prototyped architecture.
Possible architecture:
Cloud Storage / BigQuery
→ Vertex AI Training
→ Model Registry
→ Vertex AI Endpoint
→ Monitoring
→ Retraining Pipeline
For this project, prioritize XGBoost, payment decisioning, threshold optimization, and lifecycle monitoring. BERT is unnecessary unless you add text data such as dispute descriptions or investigation notes.
10. Final Deliverables
The capstone should include:
Problem statement and business objectives
Data dictionary and data-quality report
EDA notebook
Feature-engineering pipeline
Logistic Regression, Random Forest, and XGBoost comparison
Threshold and cost-analysis report
Error-analysis report
Inference API or prediction script
Monitoring and retraining design
Final project summary with limitations
