# Data Visualization Challenge

An open-ended project applying everything from [Data Manipulation & Visualization](../Lessons/DataVisualization.md) and [Data Manipulation & Visualization: Titanic Walkthrough](../Lessons/DataManipulationVisualization.md) to a new dataset.

## Dataset

`Datasets/MoviesOnStreamingPlatforms_updated.csv` — movies and their availability across Netflix, Hulu, Prime Video, and Disney+, along with IMDb/Rotten Tomatoes ratings, genre, country, language, and runtime.

## Task

Produce a short visual analysis (5-7 charts) that tells a coherent story about this dataset — not 5-7 unrelated charts, but a narrative with a beginning, middle, and end. Pick a angle and follow it, for example:

- How does content availability differ across the 4 platforms (volume, genre mix, ratings)?
- Has average IMDb rating for streaming content changed over time (by `Year`)?
- Which genres or countries dominate a given platform's catalog?

You're not required to use one of these — pick your own angle if you have one, but state it explicitly.

## Requirements

1. **State your angle** in a markdown cell at the top of the notebook, in 1-2 sentences
2. **Clean the data first** — this dataset has messy fields (e.g. `Rotten Tomatoes` is a string percentage, `Genres`/`Country`/`Language` are comma-separated lists in one column). Handle at least 2 of these before charting.
3. **5-7 charts**, each with a title, axis labels, and a one-sentence markdown takeaway underneath it — what does this chart show, in plain language?
4. **Use at least 3 different chart types** across your 5-7 charts (see [Data Visualization](../Lessons/DataVisualization.md) for chart-type guidance)
5. **A closing summary** (3-4 sentences) tying the charts back to your stated angle

## Rubric
| Criteria | Meets expectations |
|---|---|
| Angle | Clearly stated, and every chart supports it (no unrelated charts) |
| Data cleaning | At least 2 messy fields handled correctly before charting |
| Chart quality | All charts titled, labeled, and legible; at least 3 chart types used |
| Narrative | Each chart has a takeaway; closing summary ties them together |
