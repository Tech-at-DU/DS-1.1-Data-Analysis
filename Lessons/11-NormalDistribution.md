## Normal Distribution, CLT and Z-Scores

### Learning Objectives
By the end of this lesson, students will be able to:
1. Describe the standard normal (Gaussian) distribution and why it shows up so often
2. Explain the Central Limit Theorem and what it enables
3. Compute a Z-score and convert between Z-scores and probabilities
4. Apply these to a real, skewed dataset (video game sales) and show the CLT holds anyway

### The Normal Distribution

The normal distribution is the familiar bell curve: symmetric, centered on the mean, with most values clustered near the center and fewer as you move away. It's defined entirely by two numbers — mean (μ) and standard deviation (σ) — and shows up constantly in nature and data because of the **Central Limit Theorem**: if you take repeated random samples from *almost any* distribution and look at the distribution of their means, that distribution of means approaches normal as sample size grows — regardless of the shape of the original data. This is why so many statistical tests (t-tests, confidence intervals) can assume normality even when the underlying data isn't normal — they're relying on the CLT, not the raw data's shape.

### Z-Scores

A **Z-score** tells you how many standard deviations a value is from the mean:

```python
z = (x - mean) / std_dev
```

A Z-score of 0 is exactly average. A Z-score of +2 is two standard deviations above the mean — unusually high. Z-scores let you compare values across different scales/distributions on one common footing, and `scipy.stats.norm.cdf(z)` converts a Z-score into the probability of seeing a value that low or lower (and `.sf(z)` for that high or higher).

### Check Your Understanding

Answers: [Solutions/NormalDistribution.md](../Solutions/NormalDistribution.md).

1. If you increase the sample size from 30 to 300 in the CLT sampling exercise, what happens to the spread of the sampling distribution of the mean?
2. A Z-score beyond ±3 is usually called "unusual." What does a huge Z-score (like 50+) on a skewed raw column, such as `Global_Sales`, actually tell you?
3. What does `scipy.stats.norm.cdf(0)` return, and why does that number make sense?

### Topics
- Advanced Descriptive Statistics
  - The Standard Normal Distribution
  - Applications of the Central Limit Theorem
  - Intro to Z-Scores
  - Converting Z-Scores to Probabilities (and Vice Versa)

### Resources
- Go through [this article on the normal (Gaussian) distribution](https://www.mathsisfun.com/data/standard-normal-distribution.html) by Math Is Fun
- Read this [article on Z-scores and distributions](http://www.statisticshowto.com/probability-and-statistics/z-score/)
- Watch WSU math professor Dr. Poyser's [fascinating video on normal distributions and z-scores](https://www.youtube.com/watch?v=zZWd56VlN7w)

### Challenges

Deliverable: a notebook demonstrating the CLT on real data plus 3 answered Z-score questions.

1. **Sampling distribution of means** — using the `Global_Sales` column of `Datasets/vgsales.csv` (right-skewed: most games sell modestly, a few blockbusters sell far more):
   - Plot a histogram of `Global_Sales` and confirm it is *not* normally distributed
   - Write a function that draws 1,000 random samples of size 30 from the column, computes the mean of each sample, and returns the list of sample means
   - Plot a histogram of those 1,000 sample means and confirm it *does* look approximately normal — this is the Central Limit Theorem in action
2. **Z-scores** — using the same column, answer:
   - What is the Z-score of the best-selling game in the dataset?
   - Using `scipy.stats.norm.cdf`, what proportion of games would you expect to sell less than a game with Z-score 1.5?
   - Using `scipy.stats.norm.sf`, what proportion of games would you expect to sell more than a game with Z-score 2.0?
3. Complete [this notebook on CLT and distributions](../Notebooks/11-NormalDistribution.ipynb)

### Stretch Challenges
- Write a custom function to calculate the Z-Score of one or many data points in a distribution
- Write a custom `.describe()` function returning important descriptive stats in a tabular manner from a non-DataFrame dataset (NP array, Python list)

### Self-Check
- [ ] `Global_Sales` mean ≈ **0.54**, standard deviation ≈ **1.56** (population, i.e. `ddof=0`)
- [ ] The best-selling game's Z-score is huge — around **53** — because `Global_Sales` is extremely right-skewed, not because your code is wrong
- [ ] `norm.cdf(1.5)` ≈ **0.933**, `norm.sf(2.0)` ≈ **0.0228** — these are fixed values for any Z-score of 1.5/2.0, independent of the dataset
- [ ] My 1,000-sample-means histogram looks roughly bell-shaped and centered near 0.54, even though the raw `Global_Sales` histogram doesn't
- [ ] My sampling function takes sample size and column as arguments — I tested it with a different sample size (not just 30) and it still worked
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/NormalDistribution.md))
