## Conditional Probability

### Learning Objectives
By the end of this lesson, students will be able to:
1. Compute basic probability of an event from counts (`event_count / sample_space`)
2. Distinguish independent, dependent, and mutually exclusive events
3. Compute conditional probability — the probability of B given A has occurred
4. Apply these to a real dataset (Titanic) with pandas

### Basic Probability

Probability measures how likely an event is, on a scale from 0 (never happens) to 1 (always happens):

```python
def probability(event_count, sample_space):
    return event_count / sample_space

# e.g. Google receives ~3,000,000 applicants, hires ~7,000
probability(7000, 3_000_000)  # -> 0.00233...
```

Express the same number as a percentage (`p * 100`) or a fraction (`event_count/event_count` over `sample_space/event_count`, rounded) — same probability, three different ways to read it depending on the audience.

### Types of Events
- **Independent events** — one event's outcome doesn't affect the other's probability (two separate coin flips).
- **Dependent events** — one event's outcome changes the other's probability (drawing cards without replacement).
- **Mutually exclusive events** — both can't happen at once (a single die roll landing on 3 *and* 5).

### Conditional Probability

Conditional probability answers: *given that A already happened, what's the probability of B?* Written `P(B|A)`. It's the probability of both A and B occurring, divided by the probability of A alone:

```python
def conditional_prob(subset_count, event_count, sample_space):
    subset_prob = subset_count / sample_space   # P(A and B)
    event_prob = event_count / sample_space     # P(A)
    return subset_prob / event_prob
```

Worked example on the hiring numbers above: of the 7,000 hires, 1,500 have brown hair. `conditional_prob(1500, 7000, 3_000_000)` gives the probability someone has brown hair *given that they were hired* — different from the unconditional probability of having brown hair in the whole applicant pool.

### Topics
- Review of basic data exploration and analysis
- Independent vs. dependent, mutually exclusive events
- Conditional probability, `P(B|A)`

### Resources
- Read this FiveThirtyEight [article on statistical trends across Bob Ross's artwork](https://fivethirtyeight.com/features/a-statistical-analysis-of-the-work-of-bob-ross/)
- [Math is Fun: Probability](https://www.mathsisfun.com/data/probability.html)

### Challenges

Deliverable: a notebook containing your `probability()` and `conditional_prob()` functions, answers to 7 questions from the list below, and a markdown cell for each answer stating the probability as a percentage.

1. Construct the `probability()` and `conditional_prob()` functions from this lesson in Python
2. Choose 7 of the following questions and answer each with the Titanic dataset (`Notebooks/titanic.csv`) using pandas — show your code and state the answer as a percentage:
   - What is the probability a passenger survived?
   - What is the probability a passenger was male?
   - What is the probability a passenger was in 1st class?
   - Given a passenger survived, what is the probability they were male? (conditional)
   - Given a passenger survived, what is the probability they were in 1st class? (conditional)
   - Given a passenger was female, what is the probability they survived? (conditional)
   - Given a passenger was in 3rd class, what is the probability they survived? (conditional)
   - What is the probability a passenger was both female and survived? (joint)
   - Given a passenger embarked at Southampton, what is the probability they were in 3rd class? (conditional)
   - Given a passenger was under 18, what is the probability they survived? (conditional)
3. Complete the [notebook on basic and conditional probability](../Notebooks/ConditionalProbability.ipynb)

### Stretch Challenges
- Create one visualization (bar chart) per conditional-probability question comparing the conditional probability against the unconditional baseline

### Rubric
| Criteria | Meets expectations |
|---|---|
| Functions | `probability()` and `conditional_prob()` implemented and produce correct results on the worked example |
| Questions | 7 questions answered, each with working pandas code and a stated percentage |
| Correctness | Conditional questions are actually computed as conditional (not unconditional) probabilities |
| Clarity | Each answer has a one-line markdown explanation of what it means |
