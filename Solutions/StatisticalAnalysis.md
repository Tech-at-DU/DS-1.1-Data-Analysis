# Statistical Analysis: GMM, KDE, and Correlation — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/StatisticalAnalysis.md](../Lessons/StatisticalAnalysis.md). Try each question yourself before reading the answer.

1. Near **0** means little to no *linear* relationship between the two variables. Near **+1** means a strong positive linear relationship — as one variable increases, the other tends to increase too, in a fairly straight-line way. Near **-1** means a strong negative linear relationship — as one increases, the other tends to decrease.

2. A GMM gives you a **parametric model** — a set of means, variances, and weights describing the underlying sub-populations that (it estimates) generated the data. Unlike a histogram, which just summarizes the data you observed, a fitted GMM lets you compute exact probability densities at any point and generate new synthetic samples that follow the same estimated distribution.

3. Because the sign tells you the *direction* of the relationship, and getting it backwards flips the conclusion entirely. Since `Pclass` 3 is the *worst* class, a negative correlation with `Survived` means "worse class, lower survival" — which matches what actually happened historically. Reading only the magnitude (0.339) without the sign would leave you unable to say whether better class improved or hurt survival odds.
