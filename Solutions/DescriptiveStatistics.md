# Data Cleaning & Descriptive Statistics — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/07-DescriptiveStatistics.md](../Lessons/07-DescriptiveStatistics.md). Try each question yourself before reading the answer.

1. `Age` is right-skewed with some outliers (a handful of much older passengers). The mean gets pulled toward those extreme values; the median doesn't, since it only cares about the middle position of the sorted data. Filling with the median keeps the fill value representative of a "typical" passenger instead of skewed by a few outliers.

2. When the categories have **no natural order** (nominal data, like `Embarked` or `age_group` labels). Integer encoding would assign an arbitrary ranking (e.g. `C`=0, `Q`=1, `S`=2), which could mislead a model into thinking `S` is somehow "more" than `C`. One-hot encoding avoids implying any order.

3. The mode works on **non-numeric/categorical data**, where mean and median are meaningless (you can't average "S", "C", and "Q"). It's also the only one of the three that identifies the single most common value, which is sometimes what you actually want (the most frequent embarkation port, not some computed middle value).
