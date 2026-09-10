# SQL for Data Analysis — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/SQL_DataAnalysis.md](../Lessons/SQL_DataAnalysis.md). Try each question yourself before reading the answer.

1. `SELECT Genre, SUM(Global_Sales) FROM games GROUP BY Genre`.

2. `WHERE` filters individual **rows** before any grouping happens — it operates on the raw data. `HAVING` filters **groups** after `GROUP BY` has aggregated them — it operates on the result of an aggregate function like `SUM()` or `COUNT()`. You can't write `WHERE SUM(Global_Sales) > 500` because `WHERE` runs before the sum exists yet; that's exactly what `HAVING` is for.

3. An inner `JOIN` only keeps rows where the join key (`Platform`, here) has a match in **both** tables. If a game's platform isn't listed in `platform_makers`, that row disappears entirely from an inner join's result. `LEFT JOIN` keeps every row from the left table regardless of whether a match exists, filling in `NULL` for the unmatched columns instead of dropping the row.
