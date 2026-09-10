## Simple Data Manipulation with Pandas

### Learning Objectives
By the end of this lesson, students will be able to:
1. Create a pandas DataFrame from a Python dictionary
2. Select rows/columns with `.loc`, `.iloc`, and boolean filtering
3. Apply functions across a DataFrame with `.apply()`
4. Sort, aggregate, and pivot a DataFrame

### Let's create a simple DataFrame in Pandas

- If we pass a Python dictionary as the `data` to the Pandas DataFrame input argument, we can create a Pandas DataFrame

```Python
import pandas as pd

df = pd.DataFrame(data= {'name':['john', 'mary', 'peter','jeff','bill', 'lisa'], 'age':[23, 78, 22, 19, 45, 33],
                         'state': ['iowa', 'dc', 'california', 'texas', 'washington', 'dc'], 'num_children': [2, 2, 0, 1, 2, 1],
                        'num_pets' : [0, 4, 0, 5, 0, 0]})
```

`df.columns`

## If we are only interested in the first three column

`df[['name', 'age', 'state']]`

### Select the second to fourth rows based on columns (name and age for example)

`df.loc[2:4, 'name']`

`df.loc[2:4, ['name', 'age']]`

### Select the first two rows

```Python
# select the first 2 rows
df.iloc[:2]
```
### Select the last two rows
```Python
# select the last 2 rows
df.iloc[-2:]
```
### Select rows up to and including the assigned one

```Python
# select rows up to and including the one
# with index=2 (this retrieves 3 rows)
df.loc[:2]
```
### Select the first column without specifying the name of column

```python
# first column of data frame with index
df.iloc[:,0]
```
```Python
# select columns by name
df.loc[:,['age', 'state']]
# df[['age', 'state']]
```
### Select the second row of dataframe
```Python
# second row of data-frame
df.iloc[1]
```

### Filter or conditional selection of data-frame
```Python
# people whose "age" is greater than 30
df[df['age'] > 30]
```
### Another way of the above selection
`df[df.age> 30]`

### Select data-frame such that the return data-frame has more pets than children

```Python
# people who have more pets than children
df[df["num_pets"] > df[ "num_children"]]
```
### Who in the data-frame is older than 40 and own pets

```Python
# people older than 40 who own pets
df[(df["age"] > 40) & (df["num_pets"] > 0)]
df[ (df["age"] > 40) | (df["num_pets"] > 0) ]
```
### Drop age and num_children columns
```Python
# df itself is not modified; a copy is returned instead
df.drop(["age","num_children"],axis=1)
```
### After dropping, the original data-frame is untouched

`df`
`df.describe()`

### What is the average for age, num_pets and num_children?
```Python
# Apply an aggregate function to every column
import numpy as np
df[["age","num_pets","num_children"]].mean()
df[["age","num_pets","num_children"]].apply(lambda col: np.mean(col),axis=0)
```
`df[["age","num_pets","num_children"]].apply(lambda col: np.sum(col),axis=0)`

`df['age'].sum()`

### Add numerical values of age, num_pets, num_children
```Python
df[["age","num_pets","num_children"]].apply(lambda row: np.sum(row),axis=1)
```
### Select data-frame based on column name
`df[['age']]`

`df['age']`

`df[["age"]].apply(lambda value: value*2)`

### Apply a function to specific column and apply the changes to original data-frame

`df['age'] = df['age'].apply(lambda x: x*2)`

### Sort data-frame based on a specific column in ascending order

```Python
# Sort DataFrame by column value
df.sort_values( "age", ascending= True)
```
### Select rows whose name begins with the letter 'j'

```Python
# select rows whose name begins with the letter 'j'
df[df.apply(lambda row: row['name'].startswith('j'),axis=1)]
```

### Pivot table from data-frame
```python
from collections import OrderedDict
from pandas import DataFrame
import pandas as pd
import numpy as np

table = OrderedDict((
    ("Item", ['Item0', 'Item0', 'Item1', 'Item1']),
    ('CType',['Gold', 'Bronze', 'Gold', 'Silver']),
    ('USD',  ['1$', '2$', '3$', '4$']),
    ('EU',   ['1€', '2€', '3€', '4€'])
))
d = DataFrame(table)
p = d.pivot(index='Item', columns='CType', values='USD')
```

### Check Your Understanding

Answers: [Solutions/SimpleDataManipulation.md](../Solutions/SimpleDataManipulation.md).

1. On the same DataFrame, `df.loc[:2]` and `df.iloc[:2]` return a different number of rows. Why, and how many rows does each return?
2. In `.apply(func, axis=0)` vs. `.apply(func, axis=1)`, which one applies `func` to each row, and which to each column?
3. Does `df.drop(["age"], axis=1)` change the original `df`? How would you make the change stick?

### Topics
- Creating a DataFrame from a dictionary
- Selecting rows/columns: `.loc`, `.iloc`, boolean filtering
- Aggregating with `.mean()`, `.sum()`, `.apply()`
- Sorting and pivoting

### Resources
- [pandas: Indexing and selecting data](https://pandas.pydata.org/docs/user_guide/indexing.html)
- Complete the [companion notebook](../Notebooks/Pandas_Intro.ipynb)

### Challenges

Deliverable: a notebook building the `people` DataFrame below and answering all 6 questions using the operations demonstrated above (no writing raw loops).

```python
people = pd.DataFrame({
    'name': ['john', 'mary', 'peter', 'jeff', 'bill', 'lisa'],
    'age': [23, 78, 22, 19, 45, 33],
    'state': ['iowa', 'dc', 'california', 'texas', 'washington', 'dc'],
    'num_children': [2, 2, 0, 1, 2, 1],
    'num_pets': [0, 4, 0, 5, 0, 0],
})
```

1. Who is older than 30?
2. Who has more pets than children?
3. What's the average age, and the average number of pets?
4. Sort the DataFrame by age, descending
5. Which rows have a name starting with a vowel?
6. Add a new column `pet_to_child_ratio` = `num_pets / (num_children + 1)` (the `+1` avoids dividing by zero)

### Self-Check
- [ ] Question 1 ("older than 30") returns exactly 3 people: mary, bill, lisa
- [ ] Question 2 ("more pets than children") returns exactly 2 people: mary, jeff
- [ ] Question 3's average age is `36.666...` and average pets is `1.5`
- [ ] Question 4 uses `.sort_values(..., ascending=False)`, not a manual loop
- [ ] Question 5 ("name starts with a vowel") returns an **empty** result — none of john/mary/peter/jeff/bill/lisa start with a/e/i/o/u. If you got rows back, check your condition
- [ ] Question 6's `pet_to_child_ratio` column is computed with vectorized pandas math (`df['num_pets'] / (df['num_children'] + 1)`), not a Python loop
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/SimpleDataManipulation.md))
