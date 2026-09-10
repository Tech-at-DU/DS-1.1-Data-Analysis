# Applied Descriptive Statistics — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/08-AppliedDescriptiveStatistics.md](../Lessons/08-AppliedDescriptiveStatistics.md). Try each question yourself before reading the answer.

1. Mean > median suggests the distribution is **right-skewed** — a handful of higher values (the data array has values up to 10, while most values cluster lower, around 0-5) pull the mean up without moving the median, since the median only cares about the middle position, not the magnitude of extreme values.

2. **Population standard deviation** divides the sum of squared deviations by `N` (the actual count). **Sample standard deviation** divides by `N - 1` instead (Bessel's correction) — this corrects for the fact that a sample's variance tends to underestimate the true population variance, since the sample mean itself was fit to the sample. `np.std()` defaults to population standard deviation (`ddof=0`); pass `ddof=1` for the sample version.

3. **Ties at the median value.** If several passengers paid exactly the median fare, they all count as "at or below," which can push the percentage slightly above (or, depending on how you count, slightly differently from) a clean 50%. With continuous, non-repeating data, splitting at the median gives almost exactly 50/50 — but real-world data often has repeated values.
