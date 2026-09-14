## Applied Probability on DataFrames

### Learning Objectives
By the end of this lesson, students will be able to:
1. Apply probability and conditional probability directly to a pandas DataFrame
2. Compute a histogram, PDF, and CDF for a numeric column and read probabilities off them
3. Explain the empirical (68-95-99.7) rule for the normal distribution and verify it with `scipy.stats`

## A Brief Introduction to Probabilistic Thinking

- Probability is all about the **chances of an event occurring** or how likely an event is to occur, in a set of events.

- If you really think about it, you've been thinking about probability all of your life!

Ever wondered about...

> -  The chances of it raining today
> -  The chances of winning the lottery
> -  The chances of getting hired at Google

That's probabilistic thinking!

- We can draw immediate connections from the world of probabilistic thinking to the world of statistical inference and analysis.

- In mathematics, probability is modeled by the following expression:

- $P(A)= \frac{Count of A }{sample Space}$

- Don't fear at the sight of equations and non-numerical variables – this is much simpler than it looks!

- All this translates to is that **the probability of Event A occurring** in a set of observed events in _Sample Space S_ is equal to **the number of occurrences of Event A** across _Sample Space S_ divided by **the total number of observed events**

## Conditional Probability

- Probability on the surface simply describes the likelihood of individual events, but one concept we haven't spoken about yet is whether or not certain events are **dependent** on one another or not.

- As it turns out, understanding the interdependency of event occurrences is critical to fully grasping the role of probability and statistics in data science.

- Let's start with some conceptual examples

### Flip a coin three times. What is the probability of each event (H/T) occurring for each coin flip?

As you're likely already aware of, we consider the probability of each event occurrence across multiple trials to be **independent**.

In other words, the occurrence of one coin flip _does not influence_ the occurrence of another coin flip in any way.

### Dependent Events

- Consider we have a bag of marbles: two are **blue**, and three are **red**.

- We can model the probability of each outcome as the following:

- <img src="https://www.mathsisfun.com/data/images/probability-marbles-tree1.svg" />

- Notice that the probability of each outcome occurrence at the start is the number of marbles of one color divided by the total number of marbles.

### In general cases, the conditional probability of an event is described by the following equation.

<br><img src="https://www.mathsisfun.com/data/images/probability-independent-formula2.gif" /><br>

### Example Question: I Scream for Ice Cream

- 70% of your friends like Chocolate, and 35% like Chocolate AND like Strawberry.

- What percent of those who like Chocolate also like Strawberry?

Another way to refactor the question to fit our conditional probability model:

- Given that some friends like _Chocolate_, what is the probability that they like _Strawberry_ as well?

We can now attribute our events to the question parameters!

- **Event A: Chocolate**
- **Event B: Strawberry**

We're already given the following:

- $ P( Chocolate ) = 0.7 $
- $ P( Chocolate \cap Strawberry) = 0.35 $

And asked the following:

- $ P( Strawberry \mid Chocolate ) = ? $

- Therefore, our conditional probability model now looks a little like this:

- $ P( Strawberry \mid Chocolate ) = \frac{P( Chocolate \cap Strawberry )}{P( Chocolate )} $

- Plugging in our parameters gives us the following answer:

- $ P( Strawberry \mid Chocolate ) = \frac{0.35}{0.7} = 0.5 $

- which confirms to us that 50% of your friends who like chocolate also like strawberry.

- Makes sense when you think about it!

## Worked Example (Titanic)

- Given that some passengers paid over $100 for their ticket, what is the chance they survived?
    - Try, two approaches: P(survived = 1 | Fare > 100) directly
    - Another way: Use Bayesian -> P(survived = 1 and Fare > 100)/ P(Fare > 100)

### Answer

P(survived = 1 | Fare > 100) = P(survived = 1 and Fare > 100)/ P(Fare > 100)

```Python
len(df[(df['Survived'] == 1) &  (df['Fare'] >= 100)])/len(df[df['Fare'] >= 100])
# or
df[df['Fare'] >= 100]['Survived'].value_counts()
```

A second worked example — **what is the probability that a survived passenger was male?** (P(Sex = 'male' | Survived = 1)):

```Python
df[df['Survived'] == 1]['Sex'].value_counts()
109 / (233 + 109)
```

## Conditional Probability for Tennis dataset

```Python
import pandas as pd
# Outlook	Temp.	Humidity	Wind	Decision
df = pd.read_csv('tennis.txt', delimiter="\t", header=None, names=['a', 'b', 'c', 'd', 'e'])
df[df['d'] == 'Weak']
df[df['d'] == 'Weak']['e']
def conditional_prob(c1, c2, condition):
    df_new = df[df[c1] == condition][c2]
    s = df_new.unique()
    population_size = len(df_new)
    pr = {}
    for i in s:
        pr[i] = len(df[(df[c1] == condition) & (df[c2]== i)]) / population_size

    return pr

print(conditional_prob('d', 'e', 'Weak'))
print(conditional_prob('d', 'e', 'Strong'))
```

## Histogram, PDF, and CDF

A **histogram** counts how many values fall into each of a set of bins — it's the empirical (observed) shape of a distribution. A **PDF** (probability density function) is the smoothed, theoretical curve a histogram approximates — `sns.histplot(..., kde=True)` overlays one on top of the other. A **CDF** (cumulative distribution function) answers "what fraction of values are at or below X?" — it's the running total of the histogram, read left to right.

## Important Notes:

- When we have the dataset (the dataset is available), calculating probabilities is not hard

- However, if the dataset is small, our probabilities computation is not precise

- In many applications, we are interested to approximate the normalized histogram (density) with one of the known probability density function (pdf)

- The most well-known pdf is Normal or Gaussian

- Even if the dataset is not available but its pdf and its parameters be given, we can infer the desired statistics

- Also when the pdf and its parameters be given, we can arbitrarily generate samples that follows that density


## PDF and CDF on the Titanic `Age` column
```python
import seaborn as sns

# sns.distplot was removed in seaborn 0.14 — use histplot (with kde=True for a smoothed curve)
sns.histplot(df['Age'].dropna(), kde=True, bins=20)

chance_less_than_40 = len(df[df['Age'] <= 40]) / len(df['Age'].dropna())
cdf_age = df['Age'].value_counts().sort_index().cumsum() / len(df['Age'].dropna())
cdf_age.plot()
```

**Question:** using `cdf_age` above, what's the probability a passenger's age was between 20 and 40? (Hint: `P(20 <= Age <= 40) = P(Age <= 40) - P(Age < 20)` — read both values off the CDF.)

# Normal Distribution

- By now, we should have some familiarity of the types of distributions that we see in data science.

- After all, distributions are just arrangements of data values in space, and we're interested as data science to detect patterns in that space!

- There is one distribution that requires a good amount of attention, due to its relevance in data science for statistical inference and analysis.

- That is the ***Normal (Gaussian) Distribution***, otherwise known as the Bell Curve model.

<br><img src="https://ds055uzetaobb.cloudfront.net/image_optimizer/1dbcc5a80e3fb541aa4678fcff58bb26ca717902.png" /><br>

### Central Tendency

- As it turns out, the Normal Distribution is unique in that it is one of the few distributions where the three key measures of central tendency are _equivalent_.

- That's right: **the mean, median, and mode for a Normal Distribution are all the same value**.

- You can probably guess that it's the value at the dead center of the Normal Distribution, and you'd be right!

- It's the value that simultaneously is the average value, middle value, and most commonly occurring value across your data.

This allows us to make inferences regarding the data's distribution, including but not limited to the following:
- Symmetry across the center value
- Graphical peak at the mean/median/mode
- Tails get progressively smaller

- The Normal Distribution also is unique in having a direct known relationship between the standard deviation and the range of data captured across the dataset.

- In other words, **the standard deviation for a Normal Distribution can tell you how much data is contained within its bounds**.

## The shape and characteristics of Normal Distribution

Different amounts of data fall within each band of standard deviation from the mean — this is the **empirical rule**:
- 68% of the data is captured within one standard deviation from the mean.
- 95% of the data is captured within two standard deviations from the mean.
- 99.7% of the data is captured within three standard deviations from the mean.

- This makes it very effective for statistical testing and analysis to be able to grab set quantities of data using the standard deviation.

## Activity:

- Verify the above statements

```Python
import scipy.stats as st

print(st.norm.cdf(1) - st.norm.cdf(-1))

print(st.norm.cdf(2) - st.norm.cdf(-2))

print(st.norm.cdf(3) - st.norm.cdf(-3))

print(st.norm.cdf(1.64) + st.norm.sf(1.64))
```
## Activity

- The instructor of Math, graded students final exam. He is reporting that the mean was 60 out of 100 with standard deviation of 10. What is the probability that students got more than 70?

```Python
import numpy as np
import matplotlib.pyplot as plt

s = np.random.normal(60, 10, 100000)

plt.hist(s, bins=10)

plt.show()

from scipy.stats import norm

norm.sf(70, loc=60, scale=10)
```

### Check Your Understanding

Answers: [Solutions/AppliedProbabilitytodataframe.md](../Solutions/AppliedProbabilitytodataframe.md).

1. What's the difference between `P(Survived=1 and Sex='female')` (joint) and `P(Survived=1 | Sex='female')` (conditional)?
2. To get "the probability a value is *above* x" from `scipy.stats.norm`, would you use `.cdf(x)` or `.sf(x)`? Why?
3. Under the empirical rule, what percentage of data falls within 2 standard deviations of the mean?

### Topics
- Probability and conditional probability on a DataFrame
- Histogram, PDF, CDF
- The empirical (68-95-99.7) rule
- `scipy.stats.norm`: `cdf`, `sf`

### Resources
- Complete the [companion notebook](../Notebooks/09-Applied_Probability.ipynb)

### Challenges

Deliverable: a notebook answering all 5 Titanic questions below plus the tennis-dataset question, each with working pandas code and a stated numeric answer.

1. Given that a passenger is under 30 but over 20 years old, what are the chances they are in first class?
2. Given that a female passenger was unmarried (`Name` doesn't contain "Mrs"), what are the chances that she survived?
3. Given that a male passenger over 30 years did not survive, what are the odds he paid less than $25 for a ticket?
4. Using `cdf_age`, what's the probability a passenger's age was between 20 and 40?
5. A class's final exam scores are normally distributed with mean 60 and standard deviation 10. What's the probability a student scored above 70? Verify your `scipy.stats.norm` answer against a histogram of 100,000 simulated scores.
6. Using `Notebooks/Datasets/tennis.txt` and the `conditional_prob()` function from this lesson, what's the probability of playing tennis (`Decision`) given `Wind == 'Weak'` vs. `Wind == 'Strong'`? Which wind condition is more favorable to playing?

### Self-Check
- [ ] Q1 (1st class given age 20-30): **~16.6%**
- [ ] Q2 (survived given female, not "Mrs"): **~70.8%**
- [ ] Q3 (paid <$25 given male, >30, didn't survive): **~60.9%**
- [ ] Q5 (`norm.sf(70, loc=60, scale=10)`): **~0.1587** — and your simulated-histogram proportion should land close to that (it's random, so exact match isn't expected, but it should be in the same ballpark, roughly 15-16%)
- [ ] Q6: **P(Yes | Weak) = 0.75**, **P(Yes | Strong) = 0.5** — weak wind is more favorable to playing
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/AppliedProbabilitytodataframe.md))
