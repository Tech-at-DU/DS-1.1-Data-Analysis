# Deliverables

Every assignment in this course, in one place. For each lesson: read it, work the Challenges in the listed file, run the lesson's own **Self-Check** before considering it done, then bring it to your weekly check-in.

| # | Lesson | Deliverable file | What you're turning in |
|:-:|---|---|---|
| 1 | [Introduction to Data Science](Lessons/01-IntroductiontoDataScience.md) | `Notebooks/01-Data_Analysis_Intro.ipynb` | Count surviving female Titanic passengers two ways (plain `csv` + pandas), plus 2 of your own EDA questions |
| 2 | [Data Science Process & Tools](Lessons/02-DataScienceProcess.md) | `Notebooks/02-DataScienceProcess.ipynb` *(new — create it)* | Environment import check, plus 5 pandas slicing tasks on the Titanic dataset |
| 3 | [Simple Data Manipulation](Lessons/03-SimpleDataManipulation.md) | `Notebooks/03-Pandas_Intro.ipynb` | 6 questions answered on a given `people` DataFrame using `.loc`/`.iloc`/boolean filtering/aggregation |
| 4 | [How to Combine DataFrames](Lessons/04-HowtoCombineDataFrames.md) | `Notebooks/04-Pandas_Merge_Concatenate.ipynb` | 4 join types compared on two given DataFrames, plus a melt exercise |
| 5 | [Data Manipulation & Visualization: Titanic Walkthrough](Lessons/05-DataManipulationVisualization.md) | `Notebooks/05-Pandas_Titanic.ipynb` | Repeat the lesson's Cherbourg analysis for Southampton passengers, plus 2 of your own questions |
| 6 | [Data Manipulation & Visualization](Lessons/06-DataVisualization.md) | `Notebooks/06-DataVisualization.ipynb` | 4 questions, each answered with pandas + one chart (scatter, bar/histogram, pie, and your choice) |
| 7 | [Data Cleaning & Descriptive Statistics](Lessons/07-DescriptiveStatistics.md) | `Notebooks/07-DescriptiveStatistics.ipynb` | Clean Titanic `Age`/`Embarked`/`Fare`, engineer 3 new columns, one-hot/integer encode them |
| 8 | [Applied Descriptive Statistics](Lessons/08-AppliedDescriptiveStatistics.md) | `Notebooks/08-Applied_Descriptive_Statistics.ipynb` | Implement mean/median/mode/range/std from scratch, verify against numpy/scipy, answer 3 Titanic fare questions |
| 9 | [Applied Probability on DataFrames](Lessons/09-AppliedProbabilitytodataframe.md) | `Notebooks/09-Applied_Probability.ipynb` | 5 Titanic conditional-probability questions + 1 tennis-dataset question |
| 10 | [Conditional Probability](Lessons/10-ConditionalProbability.md) | `Notebooks/10-ConditionalProbability.ipynb` | Build `probability()`/`conditional_prob()` functions, answer 7 of 10 given Titanic questions |
| 11 | [Normal Distribution, CLT and Z-Scores](Lessons/11-NormalDistribution.md) | `Notebooks/11-NormalDistribution.ipynb` | Demonstrate the CLT on `vgsales.csv` sales data, answer 3 Z-score questions |
| 12 | [Statistical Distributions & Sampling](Lessons/12-StatisticalDistributions.md) | `Notebooks/12-StatisticalDistributions.ipynb` | Summary stats + skew judgment on 3 Titanic columns, a sampling function, 5 counting problems |
| 13 | [Confidence Intervals & Outliers](Lessons/13-ConfidenceIntervals.md) | `Notebooks/13-ConfidenceIntervals.ipynb` | A 95% CI for Iris-versicolor (two methods), outlier detection on Titanic `Fare` (two methods), a box plot |
| 14 | [Statistical Analysis: GMM, KDE, and Correlation](Lessons/14-StatisticalAnalysis.md) | `Notebooks/14-StatisticalAnalysis.ipynb` | Fit a GMM and KDE to a generated sample, correlate Iris features, then Titanic `Fare`/`Pclass` vs. `Survived` |
| 15 | [Hypothesis Testing & Acceptable Error](Lessons/15-HypothesisTesting.md) | `Notebooks/15-HypothesisTesting.ipynb` | 3 hypothesis-testing functions, 2 reading-reflection answers, one applied test on `student_scores.csv` |
| 16 | [Time Series Analysis](Lessons/16-TimeSeriesData.md) | `Notebooks/16-TimeSeriesData.ipynb` *(new — create it)* | Trend/seasonality decomposition, a sampling/smoothing plot, a rate-of-return calculation + a second month of your choice |
| 17 | [SQL for Data Analysis](Lessons/17-SQL_DataAnalysis.md) | `Notebooks/17-SQL_DataAnalysis.ipynb` | 7 questions on `vgsales.csv`, each answered in both SQL and pandas |
| 18 | [Working with APIs & Real-World Data](Lessons/18-WorkingWithAPIs.md) | `Notebooks/18-WorkingWithAPIs.ipynb` | Pull live weather data from a public API, parse it into a DataFrame, answer 4 questions |
| 19 | [AI-Assisted Data Analysis](Lessons/19-AI_AssistedAnalysis.md) | `Notebooks/19-AI_AssistedAnalysis.ipynb` | Verify an AI assistant's answer to 2 Titanic stats questions against your own independent code |
| 20 | [Intro to Machine Learning](Lessons/20-IntroToMachineLearning.md) | `Notebooks/20-IntroToMachineLearning.ipynb` | Train/evaluate a regression and a classification model, cross-validate, compare to a random forest |

## Beyond the 20 lessons

| Assignment | Deliverable file | What you're turning in | Suggested timing |
|---|---|---|---|
| [Homework/HW1](Homework/HW1/README.md) | `Homework/HW1/starter.ipynb` | A from-scratch histogram-binning function, verified against `np.histogram`, plus a two-group Age histogram with a legend | After lesson 6 |
| [CA_lessons/Data_Viz_Challenge](CA_lessons/Data_Viz_Challenge.md) | `Notebooks/CA_DataVizChallenge.ipynb` | An open-ended 5-7 chart visual narrative on the streaming-platforms dataset, with a stated angle | After lesson 6 |
| [Homework/HW2](Homework/HW2/README.md) | `Homework/HW2/starter.ipynb` | Full EDA → cleaning → visualization → hypothesis test on a real cardiovascular-disease dataset | After lesson 15 |
| [CA_lessons/Linear_Regression_Tutorial](CA_lessons/Linear_Regression_Tutorial.md) | `Notebooks/CA_LinearRegressionTutorial.ipynb` | Multiple linear regression with 4 predictors, standardized coefficients, single- vs. multi-predictor comparison | After lesson 20 |

## Not a graded deliverable

[`Lessons/quiz1_study_guide.md`](Lessons/quiz1_study_guide.md) describes a quiz format (dataset + questions + a screen-recording) inherited from the old instructor-led version of this course. **This hasn't been adapted for the independent-study format yet** — decide with your mentor whether to use it as a self-check milestone, skip it, or replace it with something else before treating it as required.
