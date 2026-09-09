## Repository Setup Instructions

This repo contains all course materials — lessons, notebooks, datasets, and challenges. It's self-contained: no external accounts or slide decks required.

### 1. Fork and clone

Fork this repo on GitHub, then clone your fork:

```
git clone https://github.com/<your-username>/DS-1.1-Data-Analysis.git
cd DS-1.1-Data-Analysis
```

### 2. Set up your environment

```
conda env create -f binder/environment.yml
conda activate ds-1.1-data-analysis
```

This installs everything used across every lesson in this course — pandas, numpy, scipy, statsmodels, matplotlib, seaborn, plotly, scikit-learn, duckdb, and requests.

### 3. Work through a lesson

1. Read the lesson in [`Lessons/`](Lessons/)
2. Open its companion notebook in [`Notebooks/`](Notebooks/) and complete the **Challenges** section from the lesson
3. Commit your work as you go:

```
git add Notebooks/<the-notebook-you-edited>.ipynb
git commit -m "Complete <lesson name> challenges"
```

### 4. Share your work

If you want feedback or to submit your work, push to your fork and open a pull request against the upstream repo, or share the notebook/PR link directly with whoever's reviewing your work.

```
git push origin master
```

### 5. Pulling in course updates

If the upstream course repo gets updated, add it as a second remote and pull from it:

```
git remote add upstream https://github.com/<course-org>/DS-1.1-Data-Analysis.git
git pull upstream master
```
