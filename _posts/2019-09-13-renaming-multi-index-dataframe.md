---
title: renaming multi level DataFrame
last_modified_at: 2019-09-13T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Pandas
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt:
---
In my current project, I needed to extract data from a log table. After extracting the relavant rows and grouping by `colx`,
I needed to get the sum, count and mean from data2 column

The easiest solution would be:
```python
df_gr_agent.agg({'data2': {
    'comp_callr_sum': 'sum',
    'comp_callr_count': 'count',
    'comp_callr_mean': 'mean'
}})
```
which returns:
!["notice the 'data2' column name"](/assets/images/multi_idx_1.PNG)

But unfortunately that method of renaming columns is deprecated.
I found [Shane Lynn](https://www.shanelynn.ie/summarising-aggregation-and-grouping-data-in-python-pandas/) website quite educational and found their method of "using the ravel() method on the grouped columns."
> Ravel() turns a Pandas multi-index into a simpler array, which we can combine into sensible column names

```python
grouped = data.groupby('month').agg("duration": [min, max, mean])
# Using ravel, and a string join, we can create better names for the columns:
grouped.columns = ["_".join(x) for x in grouped.columns.ravel()]
```

For my solution renaming the multi-indexed column to something more informative required using [set_levels](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.MultiIndex.set_levels.html) with the final code:

```python
agent_COMPLETECALLER = df_gr_agent.agg({'data2': ['sum', 'count', 'mean']})
agent_COMPLETECALLER.columns.set_levels(['completeCaller'], level=0, inplace=True)
agent_COMPLETECALLER.columns = ["_".join(x) for x in agent_COMPLETECALLER.columns.ravel()]
```
Returning a much neater result (no multi-level columns)
![more informative column names, no multi-level columns too](/assets/images/multi_idx_2.PNG)
