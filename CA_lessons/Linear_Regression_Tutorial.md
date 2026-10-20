# Linear Regression Tutorial

A focused deep-dive on linear regression, building on the brief single-variable example in [Intro to Machine Learning](../Lessons/20-IntroToMachineLearning.md). That lesson predicts a score from one variable (hours studied); this tutorial extends to **multiple** predictors at once.

## Simple Linear Regression (recap)

One predictor, one target — a straight line: `y = mx + b`. See [Intro to Machine Learning](../Lessons/20-IntroToMachineLearning.md#regression-example) for the worked example on `Datasets/student_scores.csv`.

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

**Fit the scaler on training data only:**

```python
scaler = StandardScaler().fit(X_train)
X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)  # transform only, never fit, on test data
```

Fitting the scaler on the full dataset (including the test set) leaks information about the test set's distribution into training, before the model has even seen it — the whole point of a test set is that it's supposed to be unseen. Always `.fit()` on training data only, then `.transform()` (not `.fit_transform()`) on the test data.

## Check Your Understanding

Answers: [Solutions/Linear_Regression_Tutorial.md](../Solutions/Linear_Regression_Tutorial.md).

1. Why fit `StandardScaler` on the training data only, rather than on the full dataset before splitting?
2. `Average_income`'s raw coefficient looks tiny (~-0.06) but its standardized coefficient is nearly as large as `Petrol_tax`'s. Why?
3. What does a negative R² on a test set actually mean?

## Task

Create a new notebook at `Notebooks/CA_LinearRegressionTutorial.ipynb`.

1. Run the multiple regression example above
2. Print and sort the coefficients — which feature has the largest effect on petrol consumption, in its original (unscaled) units?
3. Standardize the 4 features with `StandardScaler` (fit on training data only), refit the model, and re-sort the coefficients — which feature actually has the biggest standardized effect, and does the picture change compared to the raw coefficients?
4. Compare this model's R² to a simple regression using only `Population_Driver_licence(%)` as the single predictor — how much does adding the other 3 features improve the fit?

## Self-Check
- [ ] Multi-predictor model: R² ≈ **0.39**, RMSE ≈ **64**
- [ ] Raw coefficients, largest to smallest by magnitude: `Population_Driver_licence(%)` (~1347) ≫ `Petrol_tax` (~-37) > `Average_income` (~-0.06) > `Paved_Highways` (~-0.004)
- [ ] Standardized coefficients (scaler fit on training data): `Population_Driver_licence(%)` (~77) > `Petrol_tax` (~-37) ≈ `Average_income` (~-34) > `Paved_Highways` (~-16) — note how much closer `Petrol_tax` and `Average_income` are once properly scaled
- [ ] Single-predictor (`Population_Driver_licence(%)` only) model: R² is **negative** (around -0.04) — worse than just guessing the mean, on this particular test split
- [ ] I can explain in one sentence why a small test set can produce a negative R² without anything being "broken"
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/Linear_Regression_Tutorial.md))
