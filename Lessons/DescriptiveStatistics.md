## Data Cleaning & Descriptive Statistics

### Learning Objectives
By the end of this lesson, students will be able to:
1. Compute and interpret mean, median, mode, and range
2. Explain measures of central tendency vs. measures of spread
3. Clean a raw dataset: handle missing values, fix types, engineer new columns
4. Encode categorical values numerically (integer encoding, one-hot encoding)

### Descriptive Statistics

Descriptive statistics summarize a dataset with a small number of representative values:

- **Mean** — the average; sensitive to outliers (one huge value drags it up).
- **Median** — the middle value when sorted; robust to outliers.
- **Mode** — the most frequent value; the only one of the three that works on non-numeric (categorical) data.
- **Range** — max minus min; the crudest measure of spread.

Together these are sometimes abbreviated **MMMR**. Mean/median/mode describe **central tendency** — where the "middle" of the data is. Range (and later, variance/standard deviation — see [Statistical Distributions](StatisticalDistributions.md)) describes **spread** — how far values are scattered from that middle. Two datasets can share the same mean and look completely different once you look at spread.

### Data Cleaning and Processing

Raw data is rarely analysis-ready. Common cleaning steps:

- **Data wrangling** — reading CSVs with header rows (`pd.read_csv`), introducing new engineered columns, fixing column data types.
- **Normalizing values by unit** — e.g. converting all prices to the same currency/scale before comparing them (a form of integer/numeric encoding).
- **Encoding categorical values** — most stats/ML tools need numbers, not strings:
  - *Integer/label encoding*: map each category to an integer (`"low"→0, "medium"→1, "high"→2`) — fine when categories have a natural order.
  - *One-hot encoding*: create a separate 0/1 column per category (`pd.get_dummies`) — use when categories have no order, so the model doesn't infer a false ranking.
- **Data dictionaries** — a reference document describing what each column means, its type, and valid values. Write one for any dataset you hand off to someone else.

### Topics
- Descriptive statistics: mean, median, mode, range
- Central tendency vs. spread
- Data wrangling: CSVs, new columns, data types
- Integer encoding and one-hot encoding
- Data dictionaries

### Resources
- Read Jim Frost's [article on mean, median, and mode](https://statisticsbyjim.com/basics/measures-central-tendency-mean-median-mode/) — including real-world dataset examples

### Challenges

Deliverable: a notebook where the Titanic dataset ends with 3 new columns and no missing values in `Age`, `Embarked`, or `Fare`.

1. **Clean it**
   - Fill missing `Age` values with the column median (state why median, not mean, in a markdown cell)
   - Fill missing `Embarked` values with the most common port (the mode)
   - Confirm there are no remaining nulls in `Age`, `Embarked`, `Fare` with `.isnull().sum()`
2. **Engineer 3 new features**
   - `family_size` = `SibSp` + `Parch` + 1
   - `is_alone` = 1 if `family_size` == 1, else 0
   - `age_group` = `Age` discretized into bins (e.g. `Child` <18, `Adult` 18-59, `Senior` 60+) using `pd.cut`
3. **Encode**
   - Apply one-hot encoding to `age_group` and `Embarked` (`pd.get_dummies`)
   - Apply integer encoding to `Sex` (it's binary, so ordering doesn't matter)
4. Complete this [notebook on data collation and wrangling](../Notebooks/DescriptiveStatistics.ipynb)

### Rubric
| Criteria | Meets expectations |
|---|---|
| Cleaning | No nulls remain in `Age`, `Embarked`, `Fare`; fill strategy explained |
| Feature engineering | All 3 named columns (`family_size`, `is_alone`, `age_group`) present and correctly computed |
| Encoding | `age_group`/`Embarked` one-hot encoded, `Sex` integer encoded |
| Explanation | Markdown cell justifying the median-fill choice |