## Data Manipulation & Visualization

### Learning Objectives
By the end of this lesson, students will be able to:
1. Choose the right chart type for a given question (scatterplot, bar/histogram, pie)
2. Build charts with seaborn/matplotlib on a real dataset
3. Distinguish continuous vs. categorical data, and descriptive vs. predictive analytics
4. Slice, index, and filter a pandas DataFrame to answer a specific question

### Choosing a Chart

The right chart depends on the question, not personal taste:

- **Scatterplot** — relationship between two continuous variables (does age correlate with fare paid?).
- **Bar graph / histogram** — distribution or comparison of a single variable across categories or bins (how many passengers per class? what's the age distribution?).
- **Pie chart** — share of a whole across a *small* number of categories. Use sparingly — bar charts are almost always easier to read accurately than pie charts once you have more than 3-4 slices.

### Data Literacy

- **Continuous vs. discrete/categorical data** — continuous data (age, fare) can take any value in a range and supports averaging; categorical data (sex, embarked port) is a fixed set of labels and needs counts/proportions instead of means.
- **Descriptive vs. predictive analytics** — descriptive analytics summarizes what already happened in the data ("63% of first-class passengers survived"); predictive analytics uses that data to estimate what will happen for new/unseen cases (a model estimating survival odds for a new passenger). This course builds descriptive skills first because predictive work (see [Intro to Machine Learning](../README.md)) depends on it.

### Common Data-Handling Problems
- Missing values silently skewing an average or a chart
- Wrong dtype (a numeric column read in as text) breaking sort order or math
- Filtering with the wrong boolean logic and getting no rows — or all of them

### Check Your Understanding

Answers: [Solutions/DataVisualization.md](../Solutions/DataVisualization.md).

1. `Pclass` is stored as a number (1, 2, 3). Is it continuous or categorical data? Justify your answer.
2. What goes wrong, readability-wise, once a pie chart has more than 4-5 slices?
3. Give one descriptive claim and one predictive claim you could make about the same Titanic dataset.

### Topics
- Building visualizations with seaborn: scatterplots, bar graphs/histograms, pie charts
- Slicing, indexing, and filtering a pandas DataFrame
- Continuous vs. categorical data
- Descriptive vs. predictive analytics
- The data science process, revisited with a real dataset

### Resources
- [pandas: 10 minutes to pandas](https://pandas.pydata.org/docs/user_guide/10min.html)
- [seaborn: example gallery](https://seaborn.pydata.org/examples/index.html) — browse for chart-type inspiration

### Challenges

Deliverable: a notebook with 4 written questions, the pandas code that answers each using slicing/indexing, and one chart per question (4 charts total, at least one of each type: scatterplot, bar/histogram, pie).

1. Complete [this notebook](../Notebooks/DataVisualization.ipynb) on basic data visualization with seaborn on the _Titanic_ data
2. Write 4 descriptive analysis questions about the Titanic dataset. Answer each with pandas (slicing/indexing) and then chart it:
   - 1 question suited to a **scatterplot** (relationship between two continuous variables)
   - 1 question suited to a **bar graph or histogram** (distribution or comparison across categories/bins)
   - 1 question suited to a **pie chart** (share of a whole, few categories)
   - 1 question where you choose the chart type — justify the choice in a markdown cell
3. Every chart needs a title and axis labels

### Self-Check
- [ ] I have 4 questions, each clearly answerable from the Titanic data (not vague)
- [ ] My scatterplot compares two **continuous** variables (e.g. Age vs. Fare), not a continuous vs. categorical pair
- [ ] My pie chart has 4 or fewer slices — if it has more, switch to a bar chart instead
- [ ] All 4 charts have a title and labeled axes — glance at each one and check
- [ ] My free-choice chart (question 4) has a written justification for why I picked that chart type
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/DataVisualization.md))