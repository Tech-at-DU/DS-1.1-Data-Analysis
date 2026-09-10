## AI-Assisted Data Analysis

### Learning Objectives
By the end of this lesson, students will be able to:
1. Use an AI coding assistant effectively for EDA and code generation
2. Identify the specific ways AI-generated analysis fails silently
3. Verify AI-generated statistics and code against ground truth
4. Write prompts that give an AI assistant enough context to help correctly

### Why This Lesson Exists

By 2026, most data analysts write code alongside an AI assistant (Claude, ChatGPT, Copilot, or similar) rather than from a blank cell. That's a real productivity gain — but it's also a new failure mode this course hasn't covered until now: an AI assistant can produce code that runs without error and still be **wrong**, and unlike a syntax error, a wrong statistic doesn't announce itself. Everything else in this course has taught you to compute things correctly by hand first. This lesson is about using AI assistance *on top of* that foundation, not instead of it — you can only catch a wrong AI answer if you know what the right one looks like.

### What AI Assistants Are Good At

- Boilerplate: reading a CSV, setting up a plot, writing a `groupby` you already know the shape of
- Explaining an unfamiliar error message or an unfamiliar library function
- Suggesting a chart type or a statistical test for a question you describe
- Refactoring working code to be more readable

### Where It Silently Fails

- **Hallucinated columns or values** — an assistant may reference a column name that looks plausible but doesn't exist in *your* dataset, or state a statistic without actually having computed it
- **Wrong statistical test for the situation** — e.g. suggesting a Z-test when the sample is small and σ is unknown (a T-test is correct — see [Hypothesis Testing](HypothesisTesting.md))
- **Silently dropping or mishandling missing data** — code that "works" but quietly excludes rows with NaN values, changing the answer without telling you
- **Confidently wrong interpretation** — correct code, but an incorrect plain-language explanation of what the result means (e.g. treating a correlation as causation)
- **Outdated library APIs** — suggesting a deprecated function (this exact problem shows up several times elsewhere in this course's own history — see the fixed `.append()` and `sns.distplot` calls in [How to Combine DataFrames](HowtoCombineDataFrames.md) and [Applied Probability](AppliedProbabilitytodataframe.md))

### Verifying AI-Generated Analysis

Treat AI output the way you'd treat a claim from a coworker you don't fully trust yet — plausible, but check it:

1. **Does the code actually run against your data**, or does it reference columns/files that don't exist?
2. **Spot-check one number by hand.** If the assistant reports "average fare was $32.40," compute `df['Fare'].mean()` yourself and confirm.
3. **Ask the assistant to explain its own code, line by line**, in a separate follow-up. A vague or circular explanation is a signal the first answer wasn't well-grounded.
4. **Cross-check the statistical method** against what you learned in this course — is this actually the right test/metric for this question and this data?

### Writing Effective Prompts for Data Tasks

Vague prompts get vague, ungrounded answers. Give the assistant what it needs to be right, not just fast:

- **State the actual column names and dtypes**, not a paraphrase ("the `Fare` column, a float" beats "the price column")
- **State your actual question**, not the technique ("is there a meaningful difference in survival rate between classes?" beats "run a chi-square test")
- **Paste the real error message**, not a summary of it, when debugging
- **Ask for the assumptions**, explicitly: "what does this test assume about my data, and does my data meet those assumptions?"

### Check Your Understanding

Answers: [Solutions/AI_AssistedAnalysis.md](../Solutions/AI_AssistedAnalysis.md).

1. The Challenge 2 fare comparison (survivors vs. non-survivors) is a *two-sample* test, unlike the one-sample tests in [Hypothesis Testing](HypothesisTesting.md). What makes it two-sample?
2. Give one example from this lesson of an AI failure mode that wouldn't cause a Python error, yet would still produce a wrong answer.
3. Why is pasting the actual error message better prompting practice than summarizing it in your own words?

### Topics
- Where AI coding assistants help vs. where they fail silently
- Verifying AI-generated statistics and code
- Prompting for data analysis tasks

### Resources
- [Anthropic: Claude Code documentation](https://docs.claude.com/en/docs/claude-code/overview)
- Complete the [companion notebook](../Notebooks/AI_AssistedAnalysis.ipynb)

### Challenges

Deliverable: a notebook containing an AI assistant's original response, your verification of it, and a corrected version where needed, for both tasks below.

1. **Verify a claim.** Ask an AI assistant: *"Using the Titanic dataset, what percentage of passengers under 18 survived?"* Paste its full response (code + stated answer) into a markdown cell. Then independently compute the same statistic yourself with pandas. Do they match? If not, explain in a markdown cell what the assistant got wrong.
2. **Verify a test choice.** Ask an AI assistant to test whether the average `Fare` paid by survivors differs from non-survivors, and to choose and run the appropriate statistical test. Paste its response. Then, using what you learned in [Hypothesis Testing](HypothesisTesting.md), state whether it picked the right test (Z-test vs. T-test) and why, and re-run the test yourself to confirm the conclusion.
3. Write down 2 prompting mistakes you made or noticed during this exercise (e.g. a prompt that was too vague, or an answer you almost trusted without checking) and what you'd do differently

### Self-Check
- [ ] Ground truth for task 1: **54.0%** of passengers under 18 survived (n=113) — does the AI's number match? If not, did you correctly identify what it got wrong?
- [ ] Task 2 is an **independent two-sample t-test** (`scipy.stats.ttest_ind`, comparing two separate groups), not a one-sample test — did the AI get the test *type* right, not just the Z-vs-T choice?
- [ ] Ground truth for task 2: the fare difference between survivors and non-survivors is highly statistically significant (p is extremely small, far below 0.05) — survivors paid noticeably higher fares on average
- [ ] Both verifications used my own independently-written pandas/scipy code — not just re-asking the assistant to check itself
- [ ] My 2 reflection points are specific to what actually happened in this exercise, not generic advice like "always double-check AI answers"
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/AI_AssistedAnalysis.md))
