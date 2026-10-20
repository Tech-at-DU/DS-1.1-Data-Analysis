# Data Visualization Challenge

An open-ended project applying everything from [Data Manipulation & Visualization](../Lessons/06-DataVisualization.md) and [Data Manipulation & Visualization: Titanic Walkthrough](../Lessons/05-DataManipulationVisualization.md) to a new dataset.

## Dataset

`Datasets/MoviesOnStreamingPlatforms_updated.csv` — movies and their availability across Netflix, Hulu, Prime Video, and Disney+, along with IMDb/Rotten Tomatoes ratings, genre, country, language, and runtime.

## Task

Create a new notebook at `Notebooks/CA_DataVizChallenge.ipynb`. Produce a short visual analysis (5-7 charts) that tells a coherent story about this dataset — not 5-7 unrelated charts, but a narrative with a beginning, middle, and end. Pick a angle and follow it, for example:

- How does content availability differ across the 4 platforms (volume, genre mix, ratings)?
- Has average IMDb rating for streaming content changed over time (by `Year`)?
- Which genres or countries dominate a given platform's catalog?

You're not required to use one of these — pick your own angle if you have one, but state it explicitly.

## Check Your Understanding

Answers: [Solutions/Data_Viz_Challenge.md](../Solutions/Data_Viz_Challenge.md).

1. `Rotten Tomatoes` is stored as a string like `"96%"`. What do you need to do before you can compute a numeric average of it?
2. Why pick your angle *before* making charts, rather than making charts first and seeing what turns up?
3. Name one thing a coherent-narrative deliverable like this one checks for that a fixed "here's the correct number" answer key wouldn't catch.

## Requirements

1. **State your angle** in a markdown cell at the top of the notebook, in 1-2 sentences
2. **Clean the data first** — this dataset has messy fields (e.g. `Rotten Tomatoes` is a string percentage, `Genres`/`Country`/`Language` are comma-separated lists in one column). Handle at least 2 of these before charting.
3. **5-7 charts**, each with a title, axis labels, and a one-sentence markdown takeaway underneath it — what does this chart show, in plain language?
4. **Use at least 3 different chart types** across your 5-7 charts (see [Data Visualization](../Lessons/06-DataVisualization.md) for chart-type guidance)
5. **A closing summary** (3-4 sentences) tying the charts back to your stated angle

## Self-Check

This project is open-ended, so there's no single correct chart set — check your *process* and a couple of fixed facts instead:

- [ ] The dataset has **16,744** total rows. Platform counts: Netflix **3,560**, Hulu **903**, Prime Video **12,354**, Disney+ **564** — if your counts are wildly different, check your filter logic
- [ ] My stated angle is 1-2 sentences, written *before* the charts, and every chart I made actually supports it (if a chart doesn't fit the angle, cut it or change the angle)
- [ ] I handled at least 2 messy fields (e.g. `Rotten Tomatoes` converted to a number, or `Genres`/`Country` split out of their comma-separated string)
- [ ] I used at least 3 different chart types across my 5-7 charts
- [ ] Every chart has a title, labeled axes, and a one-sentence takeaway underneath it
- [ ] My closing summary explicitly refers back to my stated angle, not just a generic wrap-up
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/Data_Viz_Challenge.md))
