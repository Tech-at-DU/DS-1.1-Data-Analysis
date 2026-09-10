# How to Combine DataFrames — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/HowtoCombineDataFrames.md](../Lessons/HowtoCombineDataFrames.md). Try each question yourself before reading the answer.

1. `pd.merge(df1, df2, on='student_id')`.

2. `pd.concat([df1, df2])` (the default, `axis=0`) stacks the DataFrames **row-wise** — one on top of the other. `pd.concat([df1, df2], axis=1)` places them **column-wise** — side by side, aligned by index.

3. `pd.melt()` reshapes a *single* DataFrame's layout — turning columns into rows (wide → long). `merge()` and `concat()` combine *two separate* DataFrames together. Reach for melt when the problem is "this one table is the wrong shape," not "I have two tables to combine."
