# Hypothesis Testing & Acceptable Error — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/HypothesisTesting.md](../Lessons/HypothesisTesting.md). Try each question yourself before reading the answer.

1. **Two-tail.** The alternative hypothesis is "the drug has an effect on response time" (`μ ≠ 1.2`) — it doesn't specify the direction of the effect (faster *or* slower response). A two-tail test checks both directions at once. A one-tail test would only be appropriate if the alternative specifically claimed the drug makes response time *faster* (or specifically *slower*).

2. **Type I error** ("crying wolf") — rejecting a true null hypothesis, i.e. claiming there's an effect/difference when there really isn't one. **Type II error** ("missing a real effect") — failing to reject a false null hypothesis, i.e. concluding there's no effect when there actually is one.

3. Because the **population standard deviation (σ) is unknown** — you only have the sample's own standard deviation as an estimate. The t-distribution has heavier tails than the normal distribution, which accounts for that extra uncertainty; using a z-test here would understate how much the sample mean could plausibly vary just by chance, especially with a modest sample size like 25.
