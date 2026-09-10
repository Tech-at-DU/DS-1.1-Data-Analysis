# Time Series Analysis — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/16-TimeSeriesData.md](../Lessons/16-TimeSeriesData.md). Try each question yourself before reading the answer.

1. Log returns are **additive** across periods (you sum log-price differences), while simple percent returns **compound multiplicatively**. For small returns the two are close approximations of each other, but they aren't mathematically identical — that's why they land near each other (3.20% vs. 3.22%) without matching exactly.

2. The **residual** is whatever is left over after the trend and seasonal components have been subtracted out — the irregular, unexplained noise in the series that doesn't follow a systematic long-term direction (trend) or a repeating seasonal pattern.

3. Because averaging over a window (e.g. the last 5 data points) cancels out short-term ups and downs, leaving a line that follows the underlying direction of the data more clearly than the jagged, noisy original — the same way smoothing a photo blurs out fine grain while keeping the overall shape.
