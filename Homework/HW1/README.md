# HW1: Pandas & Custom Histograms

Builds on [Simple Data Manipulation](../../Lessons/03-SimpleDataManipulation.md) and [Data Manipulation & Visualization](../../Lessons/06-DataVisualization.md).

## Instructions

1. Open [`starter.ipynb`](starter.ipynb) — it loads `Notebooks/titanic.csv` and scaffolds both questions
2. **Q1**: Complete `custom_hist(ls, interval)` — it should bucket a numeric list into `interval` equal-width bins and return a dict of `{bin_label: count}`, without calling `np.histogram` or `pandas` binning functions internally (the point is to build the binning logic yourself)
3. Plot your Q1 histogram with `plt.bar()` (already scaffolded)
4. **Q2**: Using `.groupby()`, plot two overlaid histograms of `Age` — one for female passengers, one for male — on the same chart, with a legend distinguishing them
5. Commit and push your completed notebook

## Self-Check

- [ ] `custom_hist(df['Age'].dropna().values, 16)` returns a dict with exactly 16 keys
- [ ] The counts in your dict sum to the total number of non-null `Age` values (no passengers lost or double-counted)
- [ ] Your bin counts match `np.histogram(df['Age'].dropna().values, bins=16)[0]` — compute that separately and compare, don't just trust your function
- [ ] Your Q1 bar chart visually matches the shape of `df['Age'].dropna().plot.hist(bins=16)`
- [ ] Your Q2 chart shows both female and male histograms on one chart with a visible legend, not two separate charts

## Evaluation

This project will be evaluated as follows. **You must get an average score of 3 to pass this project:**

| Score | Rating | Correctness | Code Quality |
| :-: | --- | --- | --- |
| 1 | Needs Improvement | `custom_hist` doesn't work or Q2 is missing | Code is messy, uncommented, or full of unresolved TODOs |
| 2 | Basic | `custom_hist` works for some inputs but fails the self-check comparison against `np.histogram`; Q2 is incomplete | Code is hard to follow or sparsely commented |
| 3 | Proficient | `custom_hist` matches `np.histogram` exactly; Q2 chart has both groups and a legend | Code is clear, commented, and the self-check items all pass |
| 4 | Advanced | All of the above, plus handles edge cases (e.g. an empty list, or a list with one unique value) | Code is clear, commented, and the approach is explained in markdown |
