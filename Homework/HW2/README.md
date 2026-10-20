# DS 1.1 Cardio Hypothesis Challenge

## Applying DS 1.1 Concepts to a Real World Problem 

This project empowers you to use a new and possibly never-before-seen dataset to go step-by-step through performing data exploration, cleaning, visualizations, and hypothesis testing for a real-world use case.

### Instructions:

1. Open [`starter.ipynb`](starter.ipynb) — it loads `data/cardio_train.csv` and scaffolds the 5 sections below
2. Work through each section, following the prompts in the notebook
3. Commit and push your completed notebook

### References

All of the materials you need to complete the steps are in the lessons. Some good references:

- [Applied Descriptive Statistics](../../Lessons/08-AppliedDescriptiveStatistics.md)
- [Applied Probability on DataFrames](../../Lessons/09-AppliedProbabilitytodataframe.md) (PDFs, CDFs)
- [Normal Distribution, CLT and Z-Scores](../../Lessons/11-NormalDistribution.md)
- [Hypothesis Testing & Acceptable Error](../../Lessons/15-HypothesisTesting.md)


### Self-Check

- [ ] My loaded dataset has **70,000** rows — if not, check the `sep=';'` argument on `read_csv`
- [ ] After converting `age` from days to years, the range is about **29.6 to 64.9** years
- [ ] `cardio` is a balanced target: about **50%** of rows have `cardio == 1`
- [ ] If using the default null hypothesis (average systolic BP the same with/without cardiovascular disease): mean `ap_hi` is about **137** for `cardio == 1` vs. about **120** for `cardio == 0` — a large, statistically significant difference (p is extremely small), so the null gets rejected
- [ ] I used an independent two-sample test (comparing two separate groups), not a one-sample test
- [ ] Every section has a plain-language sentence stating the result, not just code output

### Evaluation

This project will be evaluated as follows. **You must get an average score of 3 to pass this project:**

| Score | Rating   |        Correctness        |     Code Quality   |
| :------------- | :------------- | :------------- | :------------- |
|  1  | Needs Improvement | Required sections of submission are largely missing or not functional | Code is messy and hard to follow. Code includes TODOs or does not include comments explaining which exploratory or visualization steps were taken and why. Some follow up questions may not be answered completely. |
|  2  | Basic | Most sections are complete, some may be missing, or not fully complete. | Some sections have code that is messy and hard to follow, or is not properly commented to demonstrate understanding. Follow up questions may not be clearly answered. |
|  3  | Proficient | All sections are attempted, and 80% of sections are complete, and, if using the provided null hypothesis, arrive at the correct conclusion. | Code is clear and easy to follow, all code is commented, and comments explain which exploratory or visualization steps were taken and why. Follow up questions are clearly answered. |
|  4  | Advanced | All sections are complete, additional data explorations or visualizations have been provided, or a unique null hypothesis was created and evaluated. | All code is clear, commented, and explained. Additional visualization or statistical resources have been utilized. |
