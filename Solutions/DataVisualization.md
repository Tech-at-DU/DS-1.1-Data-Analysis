# Data Manipulation & Visualization — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/DataVisualization.md](../Lessons/DataVisualization.md). Try each question yourself before reading the answer.

1. **Categorical** (specifically ordinal). Even though `Pclass` is stored as a number, 1/2/3 represent labeled groups (1st/2nd/3rd class), not a continuous measurable quantity. Averaging it doesn't produce a meaningful "typical class" the way averaging `Age` produces a meaningful typical age — the numbers are labels with an order, not measurements.

2. Slices become too small and too similar in size to visually compare accurately. Human eyes are much better at comparing bar *lengths* than pie *angles/areas*, so once you're past 4-5 categories a bar chart communicates the same data far more reliably.

3. **Descriptive:** "63% of first-class passengers survived, compared to 24% of third-class passengers." (Summarizes what already happened in this data — verify it yourself with `df.groupby('Pclass')['Survived'].mean()`.) **Predictive:** "Based on class, age, and sex, this new passenger has an estimated 70% chance of survival." (Uses patterns in the data to estimate an outcome for a case not in the dataset.)
