# Statistical Distributions & Sampling — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/12-StatisticalDistributions.md](../Lessons/12-StatisticalDistributions.md). Try each question yourself before reading the answer.

1. **Whether order matters.** If rearranging the selection produces a different, distinct outcome (1st/2nd/3rd place, a PIN code), use a **permutation**. If only *which* items are selected matters, not their order (a committee, a hand of cards), use a **combination**.

2. **`Fare`.** Ticket prices span a huge range — most passengers paid modest fares, but a small number of first-class tickets cost far more, pulling the distribution's tail to the right. This shows up numerically too: `Fare`'s standard deviation (~$49.67) is actually *larger* than its mean (~$32.20), which is a strong tell that the data is heavily skewed rather than roughly symmetric.

3. Random sampling means each sample has a chance to reflect the full range of variability in the population. Always taking the first N rows would give the exact same "sample" every time (no distribution of means at all — just one fixed number), and if the underlying data isn't in random order to begin with, the first N rows could be systematically unrepresentative (e.g. sorted by some other column).
