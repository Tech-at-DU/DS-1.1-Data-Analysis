# Data Manipulation & Visualization: Titanic Walkthrough — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/DataManipulationVisualization.md](../Lessons/DataManipulationVisualization.md). Try each question yourself before reading the answer.

1. They're two different routes to the same result. `pd.crosstab()` is a convenience function purpose-built for cross-tabulating two columns; `.groupby(a)[b].value_counts().unstack()` does the same grouping/counting with more general-purpose pandas primitives, then reshapes the result (`.unstack()`) into the same row/column layout crosstab gives you directly.

2. When the groups being compared have **different sizes**. Raw counts make a bigger group look more "significant" just because it has more people in it. `normalize='index'` converts each row to percentages of that row's total, so you're comparing proportions (e.g. "what % of female passengers were in each class") instead of raw counts.

3. A **heatmap** of a crosstab, or a grouped/stacked **bar chart** — both let you compare counts across two categorical dimensions at a glance.
