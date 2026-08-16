# Fraud Detection Project

## Summary

This project develops a **supervised binary-classification model** to predict whether an online-payment transaction is legitimate or fraudulent using `step`, `type`, `amount`, balance features, and engineered behavioral features. The model outputs a fraud label (`0` or `1`) and fraud probability.

The project includes data acquisition, cleaning, EDA, feature engineering, class-imbalance handling, and comparison of Logistic Regression, Random Forest, and XGBoost. Models are evaluated using precision, recall, F1-score, PR-AUC, ROC-AUC, and confusion matrices. This public-data capstone demonstrates foundational payment-fraud modeling.

## 1. Problem Statement

Payment teams need to decide whether an online transaction should be approved, reviewed, or declined while minimizing fraud loss, false declines, and review costs. This project will use transaction type, amount, timing, and sender/receiver balance features to predict fraudulent transactions and support safer payment decisions.

The main challenges are severe class imbalance, unusual transaction behavior, missing or limited production features, and the cost of incorrect predictions. The expected benefits are earlier fraud detection, reduced financial loss, fewer legitimate declines, and improved operational decision-making.

## 2. Model Outcomes or Predictions

**Type of learning:** Supervised learning — **binary classification**, not regression, because the target `isFraud` has two classes.

- `0` = legitimate transaction
- `1` = fraudulent transaction
- Expected output: a fraud class and/or fraud probability for each transaction

The model will use transaction type, amount, balance information, time, and engineered behavioral features. Candidate models include Logistic Regression, Random Forest, and XGBoost. Unsupervised anomaly detection may be explored as an additional method, but classification is the primary approach.

## 3. Data Acquisition

The primary source will be the Kaggle online-payment fraud dataset, containing:

`step`, `type`, `amount`, `nameOrig`, `oldbalanceOrg`, `newbalanceOrig`, `nameDest`, `oldbalanceDest`, `newbalanceDest`, and `isFraud`.

Additional data or derived features may include:

- Sender and receiver transaction frequency
- Historical transaction behavior
- Merchant, device, location, or IP information
- Authorization, decline, dispute, or chargeback indicators

The primary dataset provides labeled transactions for training and evaluation. Derived behavioral features help identify unusual activity, while payment and dispute fields would improve real-world risk detection. If confidential production data is unavailable, these additional fields may be simulated or omitted.

During acquisition, the data will be checked for missing values, duplicates, invalid balances, outliers, class imbalance, privacy issues, and data leakage. The sender and receiver IDs will be transformed into behavioral features rather than used directly as raw identifiers.

## 4. Data Preprocessing and Preparation

The data will be cleaned by:

- Checking missing values and filling numeric gaps with the median and categorical gaps with the mode, when necessary.
- Removing duplicate rows and correcting data types.
- Checking for invalid values, such as negative amounts or impossible balance changes.
- Encoding the categorical `type` field using one-hot encoding.
- Converting `nameOrig` and `nameDest` into frequency or behavioral features, then removing the raw IDs.
- Reviewing outliers and class imbalance without deleting valid fraud transactions.

The dataset will be split into **80% training data and 20% test data** using a stratified split. Stratification preserves the same legitimate-to-fraudulent ratio in both sets. A fixed `random_state=42` will make the split reproducible. Preprocessing statistics will be learned from the training set only to prevent data leakage.

```python
from sklearn.model_selection import train_test_split

X = df.drop(columns=["isFraud"])
y = df["isFraud"]

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.20,
    stratify=y,
    random_state=42
)
```

## 5. Modeling

The selected algorithms are:

- **Logistic Regression:** Baseline model that is simple, fast, and interpretable.
- **Random Forest:** Captures nonlinear relationships and interactions among transaction and balance features.
- **XGBoost:** Primary candidate for tabular fraud data because it handles complex patterns, mixed feature effects, and class imbalance effectively.

The models will be compared using precision, recall, F1-score, PR-AUC, ROC-AUC, and a confusion matrix. Accuracy will not be the primary metric because fraudulent transactions are a small minority. The final model and decision threshold will be selected based on the balance between fraud detection, false declines, and review cost.

## 6. Model Evaluation

This is primarily a **classification** problem because the target `isFraud` contains two labels. Regression is not appropriate because the goal is not to predict a continuous value. Unsupervised anomaly detection may be considered as an exploratory comparison, but it does not use the known fraud labels and is not the primary approach.

The classification models will be evaluated using:

- **Precision:** Percentage of flagged transactions that are actually fraudulent.
- **Recall:** Percentage of fraudulent transactions detected.
- **F1-score:** Balance between precision and recall.
- **PR-AUC:** Important for imbalanced fraud data.
- **ROC-AUC:** Overall ranking ability across thresholds.
- **Confusion matrix:** Counts of true positives, false positives, true negatives, and false negatives.

The optimal model will be selected by comparing Logistic Regression, Random Forest, and XGBoost on the same stratified test set. XGBoost is expected to be the strongest candidate for this tabular dataset, but the final choice will be based on measured PR-AUC, recall, precision, error costs, interpretability, and inference efficiency. Actual metric values will be reported from the completed notebook experiments.
