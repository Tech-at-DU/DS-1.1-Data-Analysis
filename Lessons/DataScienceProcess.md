## Data Science Process & Tools

### Learning Objectives
By the end of this lesson, students will be able to:
1. Describe the stages of a data analysis project, start to finish
2. Set up and use a Python data science environment (conda, Jupyter)
3. Explain what a pandas DataFrame/Series is and load one from a real source
4. Recognize common sources of bias in a dataset before analyzing it

### The Data Science Process

Most data analysis work follows the same rough loop, regardless of the tool or dataset:

1. **Ask a question** — what decision or claim does this analysis need to support?
2. **Get the data** — a CSV, a database, an API, a scrape. Know where it came from.
3. **Clean it** — handle missing values, fix types, remove duplicates, catch outliers.
4. **Explore it** — descriptive stats, visualizations, look for patterns and anomalies.
5. **Analyze/model it** — hypothesis tests, correlations, or a predictive model.
6. **Communicate it** — a chart, a report, a notebook someone else can rerun.

Every lesson in this course maps onto one of these stages. Keep this loop in mind — it's the throughline connecting "here's a stats formula" back to "here's why an analyst uses it."

**A quick word on bias:** the process above only works if the data is trustworthy. Before drawing conclusions, ask who or what is missing from this dataset, how it was collected, and whether the sample actually represents the population you're making claims about. A dataset can be clean and still be biased.

### Tools
- **conda / a Python environment manager** — keeps project dependencies isolated and reproducible. This repo ships a [`binder/environment.yml`](../binder/environment.yml) — `conda env create -f binder/environment.yml` gets you everything used in this course.
- **Jupyter notebooks** — mix code, output, and prose in one document. The primary format for hands-on work in this course.
- **pandas DataFrames and Series** — a DataFrame is a labeled 2D table (rows + named columns); a Series is a single labeled column. Almost everything else in this course operates on one of these two structures.

### Data Slicing

"Slicing" means pulling out a subset of a DataFrame — specific rows, specific columns, or both — without changing the original data. Three tools cover almost every case:

```python
df['Age']            # one column, by name -> Series
df[['Age', 'Fare']]   # multiple columns, by name -> DataFrame
df[0:5]               # rows 0-4, by position

df.loc[0:5, 'Age']         # rows AND columns, by label
df.iloc[0:5, 0:3]          # rows AND columns, by integer position

df[df['Age'] > 30]         # boolean filtering: rows matching a condition
```

Use `.loc` when you know column *names*, `.iloc` when you're working by position, and boolean filtering (`df[condition]`) whenever the slice depends on a value rather than a fixed position.

### Topics
- The data science process, end to end
- Environment setup: conda, Jupyter
- pandas DataFrames and Series
- Creating DataFrames from various sources (CSV, dict, API response)
- Data slicing: column selection, `.loc`, `.iloc`, boolean filtering
- Sources of bias in a dataset

### Resources
- Read and work through this [10-minute introductory exploration of Pandas](https://pandas.pydata.org/pandas-docs/stable/10min.html)
- Read Adi Bronshtein's [quick introduction to the Pandas Python library](https://towardsdatascience.com/a-quick-introduction-to-the-pandas-python-library-f1b678f34673)
- Solidify your knowledge with Ryan Abernathey and Kerry Key's [intermediate Pandas exploration with tabular data](https://rabernat.github.io/research_computing/pandas.html)
- Use this [Pandas data wrangling cheat sheet](http://pandas.pydata.org/Pandas_Cheat_Sheet.pdf) as a quick reference

### Challenges

Deliverable: a notebook that imports the course environment successfully, loads `Notebooks/titanic.csv`, and contains one code cell per slicing task below with its output.

1. Environment setup
   - Install the course environment: `conda env create -f binder/environment.yml`
   - In a new notebook, import `pandas`, `numpy`, and `matplotlib` and print their `__version__` to confirm setup
2. Data slicing on the Titanic dataset
   - Select the `Name` and `Fare` columns only
   - Select the first 10 rows using `.iloc`
   - Select all passengers older than 60 using boolean filtering
   - Select the `Age` and `Survived` columns for rows 50-60 using `.loc`
   - Select all female passengers who did **not** survive

### Rubric
| Criteria | Meets expectations |
|---|---|
| Setup | Environment imports without error, versions printed |
| Slicing | All 5 slicing tasks produce correct, non-empty results |
| Method choice | `.loc`/`.iloc`/boolean filtering used appropriately for each task (not just one method for everything) |
