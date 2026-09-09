# Linear Regression Tutorial

A focused deep-dive on linear regression, building on the brief single-variable example in [Intro to Machine Learning](../Lessons/IntroToMachineLearning.md). That lesson predicts a score from one variable (hours studied); this tutorial extends to **multiple** predictors at once.

## Simple Linear Regression (recap)

One predictor, one target — a straight line: `y = mx + b`. See [Intro to Machine Learning](../Lessons/IntroToMachineLearning.md#regression-example) for the worked example on `Datasets/student_scores.csv`.

## Multiple Linear Regression

Real questions usually depend on more than one variable at once. `Datasets/petrol_consumption.csv` has 4 numeric predictors for petrol consumption per US state:

```python
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

petrol = pd.read_csv('Datasets/petrol_consumption.csv')

X = petrol[['Petrol_tax', 'Average_income', 'Paved_Highways', 'Population_Driver_licence(%)']]
y = petrol['Petrol_Consumption']

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

model = LinearRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)

print('R²:', r2_score(y_test, predictions))
print('RMSE:', mean_squared_error(y_test, predictions) ** 0.5)
```

### Reading the Coefficients

With multiple predictors, `model.coef_` gives you one coefficient per feature — how much the target changes for a one-unit increase in that feature, holding the others constant:

```python
pd.Series(model.coef_, index=X.columns).sort_values()
```

A larger absolute coefficient doesn't automatically mean "more important" — it depends on the feature's scale (a coefficient on `Average_income`, measured in thousands of dollars, isn't directly comparable to one on `Population_Driver_licence(%)`, measured in a 0-1 fraction). To compare feature *importance* fairly, standardize the features first (e.g. `sklearn.preprocessing.StandardScaler`) before fitting.

## Task

1. Run the multiple regression example above
2. Print and sort the coefficients — which feature has the largest effect on petrol consumption, in its original (unscaled) units?
3. Standardize the 4 features with `StandardScaler`, refit the model, and re-sort the coefficients — does the ranking change? Which feature actually has the biggest standardized effect?
4. Compare this model's R² to a simple regression using only `Population_Driver_licence(%)` as the single predictor — how much does adding the other 3 features improve the fit?

## Rubric
| Criteria | Meets expectations |
|---|---|
| Multiple regression | Model correctly trained on all 4 predictors, R²/RMSE reported |
| Coefficients | Correctly extracted, sorted, and interpreted (including the scaling caveat) |
| Standardization | `StandardScaler` applied correctly, ranking compared before/after |
| Comparison | Single-predictor vs. multi-predictor R² compared with a stated conclusion |
