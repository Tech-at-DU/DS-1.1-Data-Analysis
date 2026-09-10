# AI-Assisted Data Analysis — Solutions

Answers to the **Check Your Understanding** questions in [Lessons/19-AI_AssistedAnalysis.md](../Lessons/19-AI_AssistedAnalysis.md). Try each question yourself before reading the answer.

1. It's two-sample because you're comparing two **separate, independent groups** against each other — the fares paid by survivors vs. the fares paid by non-survivors — rather than comparing one group's mean against a single fixed hypothesized value (like "is the average score 65?" in the Hypothesis Testing lesson). Two groups being compared to each other means `ttest_ind`, not `ttest_1samp`.

2. Any of: a **hallucinated column** that looks plausible but doesn't exist in your actual dataset (would only error if you try to use it — an AI could state a fabricated number without ever running real code); the **wrong statistical test** chosen for the situation (runs fine, produces a number, just the wrong number for the question asked); **silently dropping rows with missing data** (the code executes without error, but the answer is computed on a different, unstated subset of the data); or a **confidently wrong plain-language interpretation** of an otherwise-correct statistical result (e.g. calling a correlation "proof" of causation).

3. Summarizing an error message loses exactly the details that are often needed to diagnose it — the precise wording, the line number, the variable name involved, the exception type. A human's paraphrase can accidentally drop or distort the one detail that would have made the real cause obvious. Pasting the actual error preserves all of that information for the assistant to work with directly.
