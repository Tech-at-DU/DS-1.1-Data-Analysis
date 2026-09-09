## SQL for Data Analysis

### Learning Objectives
By the end of this lesson, students will be able to:
1. Run SQL queries directly against a CSV file using DuckDB — no database server required
2. Translate between pandas operations and their SQL equivalents
3. Filter, sort, group, and aggregate data with SQL
4. Join two tables together with SQL

### Why SQL?

Pandas is great for exploratory work in a notebook, but most real-world data lives in a database, and SQL is the language every database speaks — Postgres, MySQL, SQLite, Snowflake, BigQuery, all of them. It's arguably the single most-used tool by working data analysts, and job postings for "data analyst" list SQL more often than any other tool, including Python. This lesson teaches SQL by mapping it directly onto operations you already know from pandas.

We'll use **DuckDB**, an embedded SQL engine that can query a CSV file directly with zero setup — no server, no separate install beyond what's already in [`binder/environment.yml`](../binder/environment.yml).

```python
import duckdb

# Query a CSV file directly — DuckDB reads it like a SQL table
duckdb.sql("SELECT * FROM 'Datasets/vgsales.csv' LIMIT 5").df()
```

That `.df()` at the end converts the SQL result back into a pandas DataFrame, so you can keep working with it however you like.

### Pandas ↔ SQL Equivalence

| Task | pandas | SQL |
|---|---|---|
| Select columns | `df[['Name', 'Genre']]` | `SELECT Name, Genre FROM games` |
| Filter rows | `df[df['Year'] > 2010]` | `SELECT * FROM games WHERE Year > 2010` |
| Sort | `df.sort_values('Global_Sales', ascending=False)` | `SELECT * FROM games ORDER BY Global_Sales DESC` |
| Limit | `df.head(10)` | `SELECT * FROM games LIMIT 10` |
| Group + aggregate | `df.groupby('Genre')['Global_Sales'].sum()` | `SELECT Genre, SUM(Global_Sales) FROM games GROUP BY Genre` |
| Count | `len(df)` or `df['Genre'].value_counts()` | `SELECT COUNT(*) FROM games` / `SELECT Genre, COUNT(*) FROM games GROUP BY Genre` |
| Filter after grouping | `df.groupby('Genre').filter(lambda g: g['Global_Sales'].sum() > 100)` | `... GROUP BY Genre HAVING SUM(Global_Sales) > 100` |

### Joins

A **join** combines rows from two tables based on a matching column — the SQL equivalent of `pd.merge()`. Given a small lookup table of platform makers:

```python
import pandas as pd

platform_makers = pd.DataFrame({
    'Platform': ['Wii', 'NES', 'X360', 'PS3', 'DS'],
    'Maker': ['Nintendo', 'Nintendo', 'Microsoft', 'Sony', 'Nintendo'],
})

duckdb.sql("""
    SELECT g.Name, g.Platform, p.Maker, g.Global_Sales
    FROM 'Datasets/vgsales.csv' AS g
    JOIN platform_makers AS p ON g.Platform = p.Platform
    ORDER BY g.Global_Sales DESC
    LIMIT 10
""").df()
```

This is an **inner join** — only rows with a matching `Platform` in both tables survive. Just like `pd.merge()`, SQL also supports `LEFT JOIN`, `RIGHT JOIN`, and `FULL OUTER JOIN` for when you want unmatched rows to survive too (see [How to Combine DataFrames](HowtoCombineDataFrames.md) for the pandas side of this same concept).

### Topics
- Querying a CSV directly with DuckDB
- `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`
- `GROUP BY`, aggregate functions, `HAVING`
- `JOIN`

### Resources
- [DuckDB: SQL Introduction](https://duckdb.org/docs/sql/introduction)
- [W3Schools: SQL Tutorial](https://www.w3schools.com/sql/) — good reference for syntax
- Complete the [companion notebook](../Notebooks/SQL_DataAnalysis.ipynb)

### Challenges

Deliverable: a notebook answering all 7 questions below in **both** SQL (via `duckdb.sql()`) and pandas, confirming both approaches agree.

Using `Datasets/vgsales.csv`:
1. What are the 10 best-selling games by `Global_Sales`?
2. How many games were released for the `Wii` platform?
3. What is the total `Global_Sales` for each `Genre`, sorted highest to lowest?
4. Which `Publisher` has the most games in the dataset?
5. What is the average `Global_Sales` for games released after 2010, grouped by `Genre`?
6. Using `HAVING`, which genres have combined `Global_Sales` over 500 (million units)?
7. Using the `platform_makers` join example above, what's the total `Global_Sales` per `Maker`?

### Stretch Challenges
- Write a query using `LEFT JOIN` instead of `JOIN` against `platform_makers` — how many more rows show up, and what does that tell you about platforms missing from the lookup table?
- Load `Datasets/starbucks_drinkMenu_expanded.csv` into DuckDB and write 2 questions and answers of your own

### Rubric
| Criteria | Meets expectations |
|---|---|
| SQL/pandas agreement | All 7 questions answered both ways, with matching results |
| Aggregation | Questions 3, 5, 6 use correct `GROUP BY`/`HAVING` syntax |
| Join | Question 7's join correctly matches platforms to makers |
