## Introduction to Data Science

### Learning Objectives
By the end of this lesson, students will be able to:
1. Define data science, data analysis, and exploratory data analysis (EDA)
2. Set up a Python data science environment
3. Name the main sources data comes from (databases, CSVs, APIs, scraping)
4. Perform a first, simple analysis on a real dataset

### What is Data Science?

Data science is the practice of extracting knowledge and insight from data — combining statistics, programming, and domain knowledge to answer questions and support decisions. **Data analysis** is the part of that process focused on examining a dataset to find patterns and answer specific questions; it's the core skill this course builds.

### What is Exploratory Data Analysis (EDA)?

EDA is the process of investigating a dataset before drawing conclusions from it — looking for patterns, spotting anomalies, and sanity-checking assumptions using summary statistics and visualizations. It has three overlapping parts:

- **Data analysis** — e.g. given a telecom churn dataset, what percentage of customers are loyal vs. churned? Which state has the highest churn rate?
- **Data analysis + visualization** — the same questions, but plotted, because a chart is usually faster to read than a table of numbers.
- **Statistical analysis** — e.g. given the Titanic dataset, what's the age distribution of male passengers by embarkation port?

### Tools

This course uses a standard Python data science stack, all included in [`binder/environment.yml`](../binder/environment.yml):

- **pandas** — loading and manipulating tabular data
- **matplotlib** and **seaborn** — visualization
- **scipy** and **statsmodels** — statistical analysis
- **Jupyter notebooks** — the primary format for hands-on work in this course, mixing code, output, and prose in one document

### Where Data Comes From

- **Databases** — queried with SQL (see the SQL lesson)
- **CSV / flat files** — the most common format in this course
- **APIs** — programmatically requesting data from a service (see the APIs lesson)
- **Web scraping** — extracting data from web pages when no API exists (respect the site's terms of service and `robots.txt`)

### Check Your Understanding

Answer these before moving on. Answers: [Solutions/IntroductiontoDataScience.md](../Solutions/IntroductiontoDataScience.md).

1. Name the 3 overlapping parts of EDA listed above.
2. In this lesson's definitions, how does "data analysis" differ from "data science"?
3. Name 2 sources of data besides a static CSV file.

### Topics
- What is data science / data analysis / EDA
- The Python data science stack
- Sources of data: databases, CSVs, APIs, scraping
- A first analysis with and without pandas

### Resources
- [Python Data Science Handbook: What is Data Science?](https://jakevdp.github.io/PythonDataScienceHandbook/00.00-preface.html)
- [pandas: 10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html)

### Challenges

Deliverable: a notebook answering the question below two ways, plus 2 more questions of your own.

1. Using `Notebooks/titanic.csv`, answer **"how many female passengers survived?"** twice:
   - Once using only Python's built-in `csv` module (no pandas) — practice working with plain rows/lists
   - Once using pandas (`pd.read_csv` + boolean filtering) — confirm both give the same answer
2. Write 2 more EDA questions about the Titanic dataset and answer each with pandas — one should require a visualization to answer clearly
3. Work through the [companion notebook](../Notebooks/Data_Analysis_Intro.ipynb) for more worked examples

### Self-Check
- [ ] Both approaches (plain `csv` module and pandas) give the **same** count of surviving female passengers — if they don't, one of them has a bug
- [ ] I wrote 2 more EDA questions, and at least one is answered with a chart, not just a number
- [ ] Every answer is stated as a plain-language sentence ("X% of..."), not just raw code output
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/IntroductiontoDataScience.md))
