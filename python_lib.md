##  Conversion
make_column_selector : To select specific type of columns

make_column_transformer : preprocessing steps to different column types.

Ex:
```python
transformer = make_column_transformer(
    (OneHotEncoder(drop="first"), selector),
    remainder=StandardScaler()
)
```
It convert to category to onehotencoder + number to standardsclar

**Feature extraction:**

1. feature importance values, such as:
2. Logistic Regression coefficients: coef_
3. Decision Tree: feature_importances_
4. Random Forest: feature_importances_
5. Gradient Boosting/XGBoost: feature_importances_
6. Linear SVM: coef_

   ```python
   SelectFromModel(
    LogisticRegression(
        penalty="l1",
        solver="liblinear"
    )
   ```
   The L1 penalty makes unimportant coefficients become zero,
   
**Comparison to Baseline**
**Confusion Matrix and ROC Curve**
1. The confusion matrix shows correct and incorrect predictions.
2. fp represents legitimate transactions incorrectly predicted as fraud.
3. fn represents fraud transactions incorrectly predicted as legitimate.
4. The ROC curve shows the model’s performance at different thresholds.
5. AUC measures how well the model separates legitimate transactions from fraud.
6. AUC closer to 1.0 indicates better performance.

**False/True positives**

```python
no_probs = lgr_pipe.predict_proba(X_test)[:, 0]

[:, 0]  # probability of No
[:, 1]  # probability of Yes


```
**Importent features**

Using co_effents (13.3 assign)


