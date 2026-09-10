## Data Manipulation & Visualization: Titanic Walkthrough

### Learning Objectives
By the end of this lesson, students will be able to:
1. Combine pandas manipulation (filtering, grouping, crosstabs) with visualization in one workflow
2. Use `.groupby()` and `pd.crosstab()` to compare categories
3. Choose between a histogram, bar chart, box plot, and heatmap for a given comparison

### Titanic Dataset Description

VARIABLE DESCRIPTIONS:
survival        Survival
                (0 = No; 1 = Yes)
pclass          Passenger Class
                (1 = 1st; 2 = 2nd; 3 = 3rd)
name            Name
sex             Sex
age             Age
sibsp           Number of Siblings/Spouses Aboard
parch           Number of Parents/Children Aboard
ticket          Ticket Number
fare            Passenger Fare
cabin           Cabin
embarked        Port of Embarkation
                (C = Cherbourg; Q = Queenstown; S = Southampton)

```Python
import numpy as np
import pandas as pd

df = pd.read_csv('titanic.csv')
df.head()
```
### Plot how many of the passengers were children, youth, middle age and old?

```Python
import matplotlib.pyplot as plt

df['Age'].hist(bins=16)
plt.show()
```
### How many of Age values are empty (or null)?

```Python
# how many of Age values are null
df['Age'].isna().sum()
```
### Create a new column as gender, when Sex is female it is zero when sex is male it is one
```Python
# create a new column as gender, when Sex is female it is zero when sex is male it is one
df['Gender'] = df['Sex'].map( {'female': 0, 'male': 1} ).astype(int)
df.head()
```
### We have one more column (check it)

`df.shape`

### Show the majority of Age range

```Python
df['Age'].plot.box()
```

### List all of the Ages that are not null
```python
df['Age'].dropna().values
```

### Slice the dataframe for those whose Embarked section was 'C'

```Python
df[df['Embarked'] == 'C'].head()
```
### Plot the Age range for those whose Embarked were 'C'

```Python
# the age range of passenger whose their Embarked were 'C'
df[df['Embarked'] == 'C']['Age'].hist(bins=16)
```
### Apply couple of Normal Distributions to Histogram obtained above
```python
df[df['Embarked'] == 'C']['Age'].plot(kind='kde')
```
### Describe a specific column
```Python
df['Embarked'].describe()
```
### How many unique values does the 'Embarked' have?
```Python
df['Embarked'].nunique()
```
### Count the different 'Embarked' values the data-frame has
```Python
df['Embarked'].value_counts().plot(kind='bar')
```
### Count the different 'Embarked' values the data-frame has and plot horizontally
```Python
df['Embarked'].value_counts().plot(kind='barh').invert_yaxis()
```
### Another way to do the count and plot it

```Python
import seaborn as sns


# Bar Chart Example #1 (Simple): Categorical Variables Showing Counts
sns.countplot(x="Embarked", palette="spring", data=df)

df['Embarked'].value_counts()

df['Sex'].value_counts().plot(kind='bar')

df['Sex'].value_counts()
```

### Plot how many of the passengers were children, youth, middle age and old based on there Sex for those who 'Embarked' in section 'C'?

```Python
df[df['Embarked'] == 'C'].groupby('Sex')['Age'].hist(bins=16)

for i in df[df['Embarked'] == 'C'].groupby('Sex')['Age']:
    print(i)

df[df['Embarked'] == 'C'].groupby('Sex')['Age'].value_counts()
```

### What is the average Age for female and male (based on sex) for those who have 'Embarked' on section 'C'?

```Python
df[df['Embarked'] == 'C'].groupby('Sex')['Age'].agg(np.mean)
```
### Which Age is the oldest for female and male (based on sex) for those who have 'Embarked' on section 'C'?
```Python
df[df['Embarked'] == 'C'].groupby('Sex')['Age'].agg(np.max)
```
### For different Ages, plot the Fare they have paid?
```Python
sns.regplot(x="Age", y="Fare", fit_reg=False, data=df)
df.plot.scatter(x="Age", y="Fare")
```
### Plot how percentage Survived for two Sex group based on the passengers class
```python
sns.barplot(x="Sex", y="Survived", hue="Pclass", data=df)
```
### Plot how many male or female were in different Passenger classes
```Python
sns.countplot(x="Sex", hue="Pclass", data=df)
```
### Verify values obtained for pertentage
```Python
df[(df['Sex'] == 'female') & (df['Pclass'] == 1)]['Survived'].value_counts()
```
### Stack plot of count based on Sex for different Passenger Class

```Python
df.groupby(['Sex'])['Pclass'].value_counts().unstack().plot(kind='bar',stacked=True)
```

### Stack plot of count based on Sex and Survival for different Passenger Class
```python
df.groupby(['Sex', 'Survived'])['Pclass'].value_counts().unstack().plot(kind='bar',stacked=True)
```
### Sometimes it is hard to read values from plot, what are the number of female and male at each Passenger Class
```Python
# df.groupby(['Sex'])['Pclass'].value_counts().unstack()
# the above and crosstab are the same
pd.crosstab(df['Sex'], df['Pclass'])

pd.crosstab(df['Sex'], df['Survived'])

pd.crosstab(df['Sex'], df['Embarked'])

```
### How to represent the above cross tab in percentage and graphically present
```Python
sns.heatmap(pd.crosstab(df['Sex'], df['Embarked'], normalize='index'), cmap="YlGnBu", annot=True)
```

### Check Your Understanding

Answers: [Solutions/DataManipulationVisualization.md](../Solutions/DataManipulationVisualization.md).

1. `pd.crosstab(df['Sex'], df['Pclass'])` and `df.groupby('Sex')['Pclass'].value_counts().unstack()` produce the same table. Why?
2. When is `normalize='index'` in `pd.crosstab()` more useful than raw counts?
3. Name a chart type well-suited to comparing counts across two categorical variables at once.

### Topics
- Combining filtering, `.groupby()`, and `pd.crosstab()` with visualization
- Choosing a chart for a categorical comparison: histogram, bar, box, heatmap

### Resources
- [pandas: Group by: split-apply-combine](https://pandas.pydata.org/docs/user_guide/groupby.html)
- [pandas: `crosstab`](https://pandas.pydata.org/docs/reference/api/pandas.crosstab.html)
- Complete the [companion notebook](../Notebooks/Pandas_Titanic.ipynb)

### Challenges

Deliverable: a notebook repeating the same style of analysis as this lesson, but for passengers who embarked at **Southampton ('S')** instead of Cherbourg, plus 2 questions of your own.

1. Repeat the age-histogram, average-age-by-sex, and oldest-passenger-by-sex analysis above for `Embarked == 'S'`
2. Build a crosstab of `Sex` vs. `Pclass` for `Embarked == 'S'` passengers and visualize it as a heatmap
3. Write and answer 2 of your own questions using `.groupby()` or `pd.crosstab()` on any column combination not already covered above

### Self-Check
- [ ] My Southampton (`Embarked == 'S'`) subset has **644** passengers — if not, check your filter
- [ ] Average age: **~27.8** for female, **~30.3** for male Southampton passengers
- [ ] Oldest Southampton passenger: **63** (female), **80** (male)
- [ ] My heatmap's cell values match what `pd.crosstab(...)` prints as a plain table — check a couple of cells by eye
- [ ] My 2 original questions each use `.groupby()` or `pd.crosstab()`, not manual filtering + counting
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/DataManipulationVisualization.md))
