# Confidence Intervals & Outliers — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/13-ConfidenceIntervals.md](../Lessons/13-ConfidenceIntervals.md). Try each question yourself before reading the answer.

1. `ci_z` assumes you **already know** the true population standard deviation (σ) and plugs it in directly, using a critical value from the normal distribution. `ci_t` doesn't assume you know σ — it **estimates** spread from the sample itself (the sample standard deviation) and uses the t-distribution instead of the normal, which has heavier tails to account for the extra uncertainty of estimating σ from a limited sample. That's why `ci_t` is often at least as wide as `ci_z`, sometimes wider.

2. The mean and standard deviation used by the 3-std-dev method are themselves **pulled by the same extreme values** you're trying to detect. On a right-skewed column, a few very high values inflate the standard deviation, which widens the `mean ± 3·std` cutoff — so it ends up wide enough that many genuinely unusual (but not *that* extreme) values fall inside the "normal" range and get missed. IQR's cutoff is based on the 25th/75th percentiles — the middle of the data — so it isn't dragged around by the extreme tail the same way.

3. It tells you the 3-std-dev method **doesn't fit this data**. `Fare` can never be negative, so a lower bound of -$117 is a logical impossibility — a clear sign that this method (which implicitly assumes something close to a symmetric, normal-ish distribution) is the wrong tool for a skewed, always-positive quantity like ticket price. The IQR method doesn't have this problem.
