# Intro to Machine Learning — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/IntroToMachineLearning.md](../Lessons/IntroToMachineLearning.md). Try each question yourself before reading the answer.

1. A single train/test split's accuracy depends on exactly which rows happened to land in the test set — that's one particular sample out of many possible splits, and some splits are a little easier or harder than others by chance. Cross-validation trains and evaluates K times on K different splits and averages the results, giving an estimate that's less sensitive to any one split's luck.

2. **No.** It means that for *this specific dataset*, with *this specific split*, logistic regression happened to generalize slightly better. Model performance is dataset-dependent — a more complex model (like a random forest) isn't automatically better, especially on a dataset that's small or where the true relationship is close to linear, which logistic regression is already well-suited for. "More complex" doesn't mean "more accurate."

3. **Precision = TP / (TP + FP)**. Reading the matrix as `[[TN, FP], [FN, TP]]` (this course's confusion matrices from `sklearn.metrics.confusion_matrix` follow that layout): with `[[78, 21], [18, 37]]`, TP=37 and FP=21, so precision = 37 / (37 + 21) = 37/58 ≈ **0.638**.
