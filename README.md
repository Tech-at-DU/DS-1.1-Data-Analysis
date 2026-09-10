# DS 1.1 Data Analysis & Visualization

## Course Description

In this course, students learn the foundational skills of data analysis, including data collection, cleaning, statistical analysis, and visualization with modern tools and libraries. Students gain a strong grounding in statistical concepts, learn to query data with SQL, pull data from real-world APIs, and use AI coding assistants effectively — then use all of it to build a simple machine learning pipeline.

### Why take this course?

The skills here are the foundation for a career as a Data Analyst, Data Scientist, or Data Engineer. If you're a Software Engineer, they'll let you work effectively with data teams and make sense of data-driven arguments in your own work.

### Prerequisites

Comfort with basic Python (variables, functions, loops, lists/dicts) and basic data structures. No prior statistics or data science background is assumed.

## Learning Outcomes

By the end of this course, students will be able to...

1. Perform exploratory data analysis and visualization of a dataset using histograms, correlations, and other tools
2. Query data with SQL and pull data from a live API
3. Understand and use descriptive statistics, probability distributions, and confidence intervals
4. Carry out hypothesis tests, and understand when to reject or accept a null hypothesis
5. Describe and implement a plan for cleaning and standardizing a dataset
6. Use an AI coding assistant effectively for data analysis, and verify its output rather than trust it blindly
7. Implement a machine learning pipeline for a simple regression and classification model

## How This Course Works

This course is designed to be worked through **at your own pace**, without needing an instructor present for every step. Every lesson lives in [`Lessons/`](Lessons/) as a markdown file with:

- An explanation and worked examples
- A short **Check Your Understanding** section — a few concept questions to answer before moving on, with answers in [`Solutions/`](Solutions/) so you can self-check as you go (these aren't the graded work, just a comprehension checkpoint)
- A **Challenges** section — the actual deliverable, completed in the matching notebook under [`Notebooks/`](Notebooks/)
- A **Self-Check** checklist — concrete, verifiable items (expected values where the answer is fixed, or process checks where it's open-ended) so you know whether your Challenge work is on track before anyone else looks at it

An instructor reviews finished Challenge notebooks at the end — the Self-Check lists are there so you catch problems yourself, early, rather than finding out much later. There are no external slide decks or accounts required beyond what's in [`binder/environment.yml`](binder/environment.yml) — everything is delivered through this repository.

## Schedule

20 lessons, roughly one per class session. Each links to its `Lessons/` file.

| # | Topic | Notes |
|:-:|---|---|
| 1 | [Introduction to Data Science](Lessons/01-IntroductiontoDataScience.md) | |
| 2 | [Data Science Process & Tools](Lessons/02-DataScienceProcess.md) | Environment setup |
| 3 | [Simple Data Manipulation](Lessons/03-SimpleDataManipulation.md) | pandas basics |
| 4 | [How to Combine DataFrames](Lessons/04-HowtoCombineDataFrames.md) | merge, concat, melt |
| 5 | [Data Manipulation & Visualization: Titanic Walkthrough](Lessons/05-DataManipulationVisualization.md) | |
| 6 | [Data Manipulation & Visualization](Lessons/06-DataVisualization.md) | Chart types, data literacy |
| 7 | [Data Cleaning & Descriptive Statistics](Lessons/07-DescriptiveStatistics.md) | |
| 8 | [Applied Descriptive Statistics](Lessons/08-AppliedDescriptiveStatistics.md) | Implement mean/median/mode from scratch |
| 9 | [Applied Probability on DataFrames](Lessons/09-AppliedProbabilitytodataframe.md) | PDF, CDF |
| 10 | [Conditional Probability](Lessons/10-ConditionalProbability.md) | |
| 11 | [Normal Distribution, CLT and Z-Scores](Lessons/11-NormalDistribution.md) | |
| 12 | [Statistical Distributions & Sampling](Lessons/12-StatisticalDistributions.md) | Includes counting/combinatorics |
| 13 | [Confidence Intervals & Outliers](Lessons/13-ConfidenceIntervals.md) | |
| 14 | [Statistical Analysis: GMM, KDE, and Correlation](Lessons/14-StatisticalAnalysis.md) | |
| 15 | [Hypothesis Testing & Acceptable Error](Lessons/15-HypothesisTesting.md) | |
| 16 | [Time Series Analysis](Lessons/16-TimeSeriesData.md) | |
| 17 | [SQL for Data Analysis](Lessons/17-SQL_DataAnalysis.md) | |
| 18 | [Working with APIs & Real-World Data](Lessons/18-WorkingWithAPIs.md) | |
| 19 | [AI-Assisted Data Analysis](Lessons/19-AI_AssistedAnalysis.md) | |
| 20 | [Intro to Machine Learning](Lessons/20-IntroToMachineLearning.md) | Capstone |

Extra project material lives in [`CA_lessons/`](CA_lessons/) ([Data Visualization Challenge](CA_lessons/Data_Viz_Challenge.md), [Linear Regression Tutorial](CA_lessons/Linear_Regression_Tutorial.md)) and [`Homework/`](Homework/).

## Setup

See [Setup.md](Setup.md) for forking/cloning this repo and setting up your environment.

## Assignments

Each lesson's **Challenges** section is its assignment — complete it in the matching notebook and commit/push your work. Larger projects are in [`Homework/`](Homework/) and [`CA_lessons/`](CA_lessons/).

## Data Analysis Technical Interview Topics Covered in This Course

- Data exploration and cleaning
- Data visualization
- SQL querying
- Outlier identification
- Applied probability and statistics
- Probability distributions
- Hypothesis testing
- Confidence intervals
- Working with APIs
- Machine learning models and pipelines
