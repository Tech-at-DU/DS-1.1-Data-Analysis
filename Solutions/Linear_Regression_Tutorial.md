# Linear Regression Tutorial — Solutions

Answers to the **Check Your Understanding** questions in [CA_lessons/Linear_Regression_Tutorial.md](../CA_lessons/Linear_Regression_Tutorial.md). Try each question yourself before reading the answer.

1. Fitting the scaler on the full dataset means it computes its mean/std using the test rows too — so information about the test set's distribution leaks into a step that happens *before* the model is ever evaluated on unseen data. That undermines the whole point of holding out a test set. Fitting `.fit()` on training data only, then `.transform()` (never `.fit()`) on the test data, keeps the test set genuinely unseen throughout.

2. `Average_income` is measured in dollars (values in the thousands), while `Petrol_tax` is a small tax rate (single digits). A "one-unit" (one dollar) increase in income is a tiny, almost meaningless change on that scale, so its raw coefficient looks small purely because of the *units*, not because income doesn't matter. Standardizing rescales every feature to the same footing (one standard deviation), which reveals that a one-standard-deviation change in income actually has nearly as much effect on petrol consumption as a one-standard-deviation change in tax — the raw coefficients were misleading you about relative importance.

3. A negative R² means the model's predictions on the test set are **worse than simply predicting the training mean for every row**. It's not a sign of a bug — with a small dataset and only a handful of test rows, a weak single predictor can easily fail this badly on a particular random split. It's a sign this specific model doesn't generalize well, which is exactly why comparing it to the fuller multi-predictor model (R² ≈ 0.39) is useful.
