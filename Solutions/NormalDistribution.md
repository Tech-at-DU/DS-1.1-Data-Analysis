# Normal Distribution, CLT and Z-Scores — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/11-NormalDistribution.md](../Lessons/11-NormalDistribution.md). Try each question yourself before reading the answer.

1. The spread **shrinks**. The standard error of the mean is `std / sqrt(n)` — as `n` grows, the denominator grows, so the sampling distribution of the mean gets narrower and more tightly clustered around the true population mean. Bigger samples give more reliable (less variable) mean estimates.

2. It tells you the raw data is **not normally distributed** — it's heavily skewed. The "beyond ±3 is unusual" rule of thumb only holds for data that actually follows a normal distribution. `Global_Sales` has a long right tail (a handful of blockbuster games selling far more than everything else), so an extreme value there can be tens of standard deviations out without anything being "wrong" — it's just evidence the column itself isn't normal, which is exactly why this lesson leans on the *sampling distribution of the mean* (which the CLT guarantees approaches normal) rather than assuming the raw data is normal.

3. **0.5.** `cdf(0)` asks "what fraction of the standard normal distribution lies at or below 0 (the mean)?" Since the normal distribution is symmetric around its mean, exactly half the probability mass is on each side — so `cdf(0) = 0.5` makes sense by symmetry alone, no calculation needed.
