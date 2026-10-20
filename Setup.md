## Repository Setup Instructions

This repo contains all course materials — lessons, notebooks, datasets, and challenges. It's self-contained: no external accounts or slide decks required.

### 1. Fork and clone

Fork this repo on GitHub, then clone your fork:

```
git clone https://github.com/<your-username>/DS-1.1-Data-Analysis.git
cd DS-1.1-Data-Analysis
```

### 2. Set up your environment

This step needs `conda` — if `conda env create` says `command not found`, you don't have it installed yet. `conda` is the environment manager program itself (Miniconda/Anaconda), not a Python package, so `pip install` won't get it. Install it first:

- **macOS with Homebrew**: `brew install miniconda`, then `conda init zsh` (or `bash` if that's your shell), then close and reopen your terminal
- **No Homebrew, or Windows/Linux**: download and run the installer from [docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html), then close and reopen your terminal

Once `conda --version` works in a new terminal:

```
conda env create -f binder/environment.yml
conda activate ds-1.1-data-analysis
```

This installs everything used across every lesson in this course — pandas, numpy, scipy, statsmodels, matplotlib, seaborn, plotly, scikit-learn, duckdb, and requests.

**`conda activate ds-1.1-data-analysis` only lasts for your current terminal session.** Every time you close and reopen your terminal, run it again before doing anything else. If your prompt says `(base)` instead of `(ds-1.1-data-analysis)`, you haven't activated it yet — commands like `jupyter` won't be found until you do.

### 3. Work through a lesson

**Work inside your cloned copy of this repo — don't copy individual notebooks or datasets out to another folder.** Notebooks load data and images with relative paths (e.g. `Datasets/titanic.csv`, `Images/DS_process.png`) that only resolve correctly from inside this repo's folder structure. Copy a notebook out on its own and those paths — and any embedded images — break.

1. Read the lesson in [`Lessons/`](Lessons/)
2. Open its companion notebook **in place**, from inside the `Notebooks/` folder:
   ```
   conda activate ds-1.1-data-analysis
   cd Notebooks
   jupyter notebook 01-Data_Analysis_Intro.ipynb
   ```
   (swap in the actual filename for the lesson you're on — see [DELIVERABLES.md](DELIVERABLES.md) for the full list)
3. Complete the **Challenges** section from the lesson, then commit your work as you go:

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

The course repo (`Tech-at-DU/DS-1.1-Data-Analysis`) may get updated after you've forked it. To pull those updates into your fork, add it as a second remote (the conventional name is `upstream`) and merge from it:

```
git remote add upstream https://github.com/Tech-at-DU/DS-1.1-Data-Analysis.git
git fetch upstream
git merge upstream/master
git push origin master
```

If you haven't started any of your own work yet, `git pull upstream master` is equivalent and simpler. Once you've committed your own notebook edits, prefer `fetch` + `merge` (or GitHub's "Sync fork" button on your fork's page) so you can review what's incoming before it lands on top of your work.
