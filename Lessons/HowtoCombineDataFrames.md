## How to Combine DataFrames

### Learning Objectives
By the end of this lesson, students will be able to:
1. Merge two DataFrames with `pd.merge()` using left/right/inner/outer joins
2. Concatenate DataFrames row-wise and column-wise with `pd.concat()`
3. Reshape a DataFrame from wide to long format with `pd.melt()`

## Combine Dataset in Pandas

- Create two data-frames that have common columns

```Python
import pandas as pd

adf = pd.DataFrame(data={'x1': ['A', 'B', 'C'], 'x2' : [1, 2, 3]})

bdf = pd.DataFrame(data={'x1': ['A', 'B', 'D'], 'x3' : ['T', 'F', 'T']})

```
### Merge adf and bdf based on adf
```python
pd.merge(adf, bdf, how='left')
```

### Merge adf and bdf based on bdf
```Python
pd.merge(adf, bdf, how= 'right')
```
### Merge adf and bdf based on what they have in common
```Python
pd.merge(adf, bdf, how= 'inner')
# Another way to do the above Task
pd.merge(adf, bdf)
```

### Union of two DataFrames

```Python
pd.merge(adf, bdf, how= 'outer')
```

### Appending Pandas DataFrames

```Python
# Append bdf after bdf (row-wise concatenation)
pd.concat([adf, bdf], sort=True)

# Column-wise concatination
pd.concat([adf, bdf], axis=1)

```
```Python
cdf = pd.DataFrame(data={'x1': ['A', 'B', 'C'], 'x3' : ['T', 'F', 'T']})
# cdf
pd.concat([adf, cdf], axis=1)

pd.concat([adf, cdf], sort=False)

# Correct the indexing after concatination
df = pd.concat([adf, cdf], ignore_index=True)
df

pd.merge(adf, cdf, how='left')
```

## When two data-frames have exactly the same columns

```Python
df = pd.DataFrame([[1, 2], [3, 4]], columns = ['a','b'])
df2 = pd.DataFrame([[5, 6], [7, 8]], columns = ['a','b'])

# DataFrame.append() was removed in pandas 2.0 — use pd.concat instead
df = pd.concat([df, df2], ignore_index=True)
```

### Slicing data-frame based on largest value for an specific column

```Python
import numpy as np

df = pd.DataFrame({'a': [1, 10, 8, 11, -1],'b': list('abdce'), 'c': [1.0, 2.0, np.nan, 3.0, 4.0]})
df.nlargest(3, 'a')

df

df['c'].isnull().sum()

df.isnull().sum()
```

### Reshape Pandas data-frame with Melt
```python
data = {'weekday': ["Monday", "Tuesday", "Wednesday",
         "Thursday", "Friday", "Saturday", "Sunday"],
        'Person 1': [12, 6, 5, 8, 11, 6, 4],
        'Person 2': [10, 6, 11, 5, 8, 9, 12],
        'Person 3': [8, 5, 7, 3, 7, 11, 15]}
df = pd.DataFrame(data, columns=['weekday',
        'Person 1', 'Person 2', 'Person 3'])

# Reshape Pandas Data With Melt
melted = pd.melt(df, id_vars=["weekday"],
                 var_name="Person", value_name="Score")

melted                         
```

### Topics
- `pd.merge()`: left, right, inner, outer joins
- `pd.concat()`: row-wise and column-wise
- `pd.melt()`: wide-to-long reshaping

### Resources
- [Pandas Merge, Join, and Concatenate](https://martin-thoma.com/pandas-merge-join-concatenate/)
- [Pandas melt tutorial notebook](https://github.com/codebasics/py/blob/master/pandas/11_melt/pandas_melt_tutorial.ipynb)
- [Reshape Pandas Data with Melt](https://deparkes.co.uk/2016/10/28/reshape-pandas-data-with-melt/)
- Complete the [companion notebook](../Notebooks/Pandas_Merge_Concatenate.ipynb)

### Challenges

Deliverable: a notebook with the two DataFrames below, all 4 join types performed and their row counts compared, plus one melt exercise.

```python
students = pd.DataFrame({'student_id': [1, 2, 3, 4], 'name': ['Ana', 'Ben', 'Cy', 'Deb']})
grades = pd.DataFrame({'student_id': [1, 2, 2, 5], 'course': ['Math', 'Math', 'Art', 'Art'], 'grade': ['A', 'B', 'A', 'C']})
```

1. Perform a left, right, inner, and outer join of `students` and `grades` on `student_id`. For each, state in a markdown cell why the row count differs (which student/grade rows appear or vanish, and why)
2. Concatenate two copies of `students` row-wise with `pd.concat`, using `ignore_index=True` so indices don't collide
3. Using the `weekday`/`Person 1-3` melt example from this lesson, melt it and then answer: which person had the highest single-day score, and on which day?

### Rubric
| Criteria | Meets expectations |
|---|---|
| Joins | All 4 join types performed correctly with correct resulting row counts |
| Explanation | Row-count differences explained correctly for each join type |
| Melt | Melted DataFrame correctly answers the highest-score question |
