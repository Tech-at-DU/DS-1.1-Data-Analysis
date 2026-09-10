## Intro to Machine Learning

### Learning Objectives
By the end of this lesson, students will be able to:
1. Explain the difference between regression and classification
2. Split data into training and test sets, and explain why that split matters
3. Train and evaluate a regression model and a classification model with scikit-learn
4. Use cross-validation to get a more reliable estimate of model performance

### From Descriptive to Predictive

Every lesson so far in this course has been **descriptive** or **inferential**: summarizing what the data shows, or testing a specific claim about it (see [Data Visualization](06-DataVisualization.md) for that distinction). Machine learning is the next step — **predictive** analytics: using patterns in existing data to make a prediction about a new, unseen case. It's built entirely on the foundation from the rest of this course — the same DataFrame, the same cleaning and feature engineering from [Descriptive Statistics](07-DescriptiveStatistics.md), the same correlation ideas from [Statistical Analysis](14-StatisticalAnalysis.md).

Two categories cover most of what you'll do as a beginner:
- **Regression** — predicting a continuous number (a price, a score, a temperature)
- **Classification** — predicting a category (survived/didn't, spam/not spam, diabetic/not)

### Train/Test Split

If you evaluate a model on the same data it learned from, it can look artificially good — it may have just memorized the training examples rather than learned a generalizable pattern. The fix: hold out a portion of the data the model never sees during training, and evaluate on that instead.

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)
```

`X` is your features (a DataFrame of input columns), `y` is the target you're predicting. `random_state` makes the split reproducible — same split every time you rerun the notebook.

### Regression Example

Predicting a student's test score from hours studied, using `Datasets/student_scores.csv`:

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

scores = pd.read_csv('Datasets/student_scores.csv')
X = scores[['Hours']]
y = scores['Scores']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)

print('R²:', r2_score(y_test, predictions))
print('RMSE:', mean_squared_error(y_test, predictions) ** 0.5)
```

**R²** (0 to 1) says how much of the variation in the target the model explains — closer to 1 is better. **RMSE** is in the same units as the target (test points, here), so it's directly interpretable: "predictions are typically off by about N points."

### Classification Example

Predicting diabetes diagnosis from health measurements, using `Datasets/diabetes.csv`:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score, confusion_matrix, classification_report

diabetes = pd.read_csv('Datasets/diabetes.csv')
X = diabetes.drop(columns=['Outcome'])
y = diabetes['Outcome']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LogisticRegression(max_iter=1000)
model.fit(X_train, y_train)
predictions = model.predict(X_test)

print('Accuracy:', accuracy_score(y_test, predictions))
print(confusion_matrix(y_test, predictions))
print(classification_report(y_test, predictions))
```

**Accuracy** alone can be misleading on imbalanced data (predicting "no" every time can still score high if most cases are "no"). The **confusion matrix** breaks correctness down by actual vs. predicted class, and `classification_report` gives precision/recall/F1 per class — always look past accuracy alone.

### Cross-Validation

A single train/test split gives one performance number, which can vary depending on which rows happened to land in the test set. **K-fold cross-validation** splits the data into K parts, trains/evaluates K times (each part taking a turn as the test set), and averages the results — a more reliable estimate:

```python
from sklearn.model_selection import cross_val_score

scores_cv = cross_val_score(LogisticRegression(max_iter=1000), X, y, cv=5)
print(scores_cv.mean(), scores_cv.std())
```

### Check Your Understanding

Answers: [Solutions/IntroToMachineLearning.md](../Solutions/IntroToMachineLearning.md).

1. Why might cross-validated mean accuracy differ from a single train/test split's accuracy?
2. If a random forest scores lower than logistic regression on one dataset, does that mean random forests are worse in general?
3. Given a confusion matrix `[[TN, FP], [FN, TP]]`, how do you compute precision for the positive class by hand?

### Topics
- Regression vs. classification
- Train/test split, and why it matters
- Linear regression: R², RMSE
- Logistic regression: accuracy, confusion matrix, precision/recall
- K-fold cross-validation

### Resources
- [scikit-learn: Getting Started](https://scikit-learn.org/stable/getting_started.html)
- [scikit-learn: Model evaluation](https://scikit-learn.org/stable/modules/model_evaluation.html)
- Complete the [companion notebook](../Notebooks/IntroToMachineLearning.ipynb)

### Challenges

Deliverable: a notebook with both models trained and evaluated as above, plus the extensions below.

1. Complete the regression example on `student_scores.csv`. Plot the regression line against the actual data points.
2. Complete the classification example on `diabetes.csv`. Report accuracy, the confusion matrix, and precision/recall for both classes.
3. Run 5-fold cross-validation on the classification model. How does the cross-validated mean accuracy compare to your single train/test split accuracy?
4. Extension: swap `LogisticRegression` for `RandomForestClassifier` (`from sklearn.ensemble import RandomForestClassifier`) on the diabetes data. Does accuracy improve? Which of the two models would you trust more, and why (consider both performance and interpretability)?

### Self-Check
(Using `random_state=42` throughout, as in the lesson — your numbers should match closely if your code follows the same steps.)
- [ ] Regression: R² ≈ **0.97**, RMSE ≈ **4.35** points
- [ ] Classification: accuracy ≈ **0.747** (74.7%)
- [ ] 5-fold CV mean accuracy ≈ **0.772** — notice it's a bit *higher* than the single-split accuracy; that's the point of cross-validation, a single split's number can be a little lucky or unlucky
- [ ] Random forest accuracy ≈ **0.721** — *lower* than logistic regression here. If you concluded "random forest is a worse model, full stop," revisit question 2
- [ ] I can compute precision for the positive class from the raw confusion matrix numbers, not just by reading it off `classification_report`
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/IntroToMachineLearning.md))
