# Simple Data Manipulation with Pandas — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/SimpleDataManipulation.md](../Lessons/SimpleDataManipulation.md). Try each question yourself before reading the answer.

1. `df.loc[:2]` returns **3 rows** (index 0, 1, 2) — `.loc` slicing is label-based and *inclusive* of the endpoint. `df.iloc[:2]` returns **2 rows** (position 0, 1) — `.iloc` slicing is position-based and follows normal Python slicing rules, which exclude the endpoint.

2. `axis=0` applies `func` down each **column** (the default). `axis=1` applies `func` across each **row**. A helpful way to remember: `axis=1` moves "across" the row, left to right — the direction columns are laid out.

3. No — `df.drop()` returns a **new** DataFrame; the original `df` is untouched. To keep the change, either reassign it (`df = df.drop(["age"], axis=1)`) or pass `inplace=True`.
