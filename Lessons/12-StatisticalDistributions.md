## Statistical Distributions & Sampling

### Learning Objectives
By the end of this lesson, students will be able to:
1. Compute variance and standard deviation, and explain what they measure
2. Recognize skew and other distributional irregularities in a histogram
3. Explain sampling methods and why the Central Limit Theorem matters for them
4. Solve basic counting (combinatorics) problems that show up when computing probabilities

### Spread: Variance and Standard Deviation

Mean/median/mode (see [Descriptive Statistics](07-DescriptiveStatistics.md)) describe the center of a distribution, but two datasets can share a mean and look completely different once you measure spread:

- **Variance** — the average of the squared differences from the mean. Squaring keeps positive and negative deviations from cancelling out, but it also puts variance in squared units, which is hard to interpret directly.
- **Standard deviation** — the square root of variance, back in the original units. This is the number you'll actually reach for day to day ("the ticket price has a mean of $32 and a standard deviation of $50" is readable; "a variance of 2500 dollars-squared" is not).

```python
df['Fare'].var()   # variance
df['Fare'].std()   # standard deviation
```

### Skew

A distribution is **skewed** when it isn't symmetric — one tail is longer than the other. Right (positive) skew means a long tail of high values (income data is classically right-skewed: most people cluster at moderate income, a few earn far more). Skew matters because it pulls the mean away from the median — in a skewed distribution the median is often the more representative "typical value." Always plot a histogram before trusting a mean.

### Sampling and the Central Limit Theorem

You rarely have data for an entire population — you work with a **sample** and infer about the population from it. How you sample matters: a **random sample** (every member has an equal chance of selection) supports valid inference; a **convenience sample** (whoever's easiest to reach) can silently bias every conclusion drawn from it.

The **Central Limit Theorem** (see also [Normal Distribution](11-NormalDistribution.md)) is what makes sampling work in practice: take repeated random samples, compute the mean of each, and the distribution of *those means* approaches normal as sample size grows — even if the original data isn't normally distributed. That's why sample means can be used to estimate a population mean with a known, quantifiable margin of error.

### Counting Problems (Combinatorics)

Some probability questions require counting the number of possible outcomes before you can compute a probability:

- **Permutations** — order matters (how many ways can 3 runners finish 1st/2nd/3rd out of 10?): `n! / (n-r)!`
- **Combinations** — order doesn't matter (how many ways can you pick a 3-person team out of 10 people?): `n! / (r! (n-r)!)`

```python
from math import comb, perm

perm(10, 3)   # 720  — permutations
comb(10, 3)   # 120  — combinations
```

These show up whenever a probability question involves picking a subset — e.g. computing the odds of drawing a specific hand of cards or a specific sample from a dataset.

### Topics
- Variance and standard deviation
- Skew and distributional irregularities
- Sampling methods and the Central Limit Theorem
- Counting: permutations and combinations

### Resources
- [Math is Fun: Standard Deviation](https://www.mathsisfun.com/data/standard-deviation.html)
- [Math is Fun: The Standard Normal Distribution](https://www.mathsisfun.com/data/standard-normal-distribution.html)
- [Seeing Theory (Brown University): sampling distributions, interactive](https://seeing-theory.brown.edu/probability-distributions/index.html#section3)
- [Math is Fun: Combinations and Permutations](https://www.mathsisfun.com/combinatorics/combinations-permutations.html)

### Check Your Understanding

Answers: [Solutions/StatisticalDistributions.md](../Solutions/StatisticalDistributions.md).

1. What's the deciding factor between using a permutation formula vs. a combination formula for a counting problem?
2. Of `Fare`, `Age`, and `SibSp` in the Titanic dataset, which would you predict is the most skewed, and why?
3. Why does the sample-means function need to draw *random* samples, rather than always taking the first N rows?

### Challenges

Deliverable: a notebook with a stats summary table, 3 annotated histograms, a working sampling function, and 5 solved counting problems.

1. Calculate the mean, median, mode, variance, and standard deviation of the `Fare`, `Age`, and `SibSp` columns from the Titanic dataset — present as a small summary table
2. Plot histograms for those same 3 columns; for each, state in a markdown cell whether it looks skewed and in which direction
3. Write a function that draws repeated random samples from a column and plots the distribution of their means — confirm it looks normal even if the original column doesn't (reuse or adapt the one from [Normal Distribution](11-NormalDistribution.md))
4. Solve these 5 counting problems using `math.perm`/`math.comb`, showing your code and final answer for each:
   - How many ways can 4 of the 12 passengers in a lifeboat be seated in the 4 front-row seats? (order matters)
   - How many different 3-person committees can be formed from a class of 15 students? (order doesn't matter)
   - A password uses 4 distinct digits (0-9). How many possible passwords are there?
   - How many ways can you choose 5 cards from a standard 52-card deck?
   - A race has 8 runners. How many possible orderings are there for 1st, 2nd, and 3rd place?
5. Complete [this notebook on Measures of Center and Spread](../Notebooks/12-StatisticalDistributions.ipynb)

### Self-Check
- [ ] `Fare`: mean ≈ **$32.20**, median ≈ **$14.45**, std ≈ **$49.67** (note the std is *larger* than the mean — a strong right-skew signal)
- [ ] `Age`: mean ≈ **29.7**, median ≈ **28.0**, std ≈ **14.5**
- [ ] `SibSp`: mean ≈ **0.52**, median ≈ **0**, std ≈ **1.1**
- [ ] I correctly called `Fare` the most skewed of the three, with a reason (its std exceeds its mean; a small number of expensive tickets pull it right)
- [ ] My sampling-means histogram looks roughly bell-shaped, regardless of which column I sampled from
- [ ] Counting answers: (1) **11,880** — (2) **455** — (3) **5,040** — (4) **2,598,960** — (5) **336**
- [ ] For each counting problem I can say in one sentence whether order mattered and why that determined perm vs. comb
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/StatisticalDistributions.md))
