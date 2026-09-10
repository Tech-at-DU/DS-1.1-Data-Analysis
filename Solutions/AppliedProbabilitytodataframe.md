# Applied Probability on DataFrames — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/AppliedProbabilitytodataframe.md](../Lessons/AppliedProbabilitytodataframe.md). Try each question yourself before reading the answer.

1. The **joint** probability `P(Survived=1 and Sex='female')` is out of the *entire* dataset — how many passengers are both female and survived, divided by everyone. The **conditional** probability `P(Survived=1 | Sex='female')` restricts the denominator to *only* female passengers first, then asks what fraction of *that* group survived. Conditional probability answers "given this subgroup, what happened," not "what fraction of everyone falls into both categories."

2. `.sf(x)` (survival function). `.cdf(x)` gives `P(X <= x)` — everything at or below x. `.sf(x)` is defined as `1 - cdf(x)`, giving `P(X > x)` directly, which is what "probability above x" means. You could compute `1 - norm.cdf(x)` instead, but `.sf()` is the direct, more numerically stable way to get it.

3. **95%.** (68% within 1 std dev, 95% within 2, 99.7% within 3 — the empirical rule.)
