---
title: See all the rows in Pandas
last_modified_at: 2019-08-16T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Jupyter
  - notes
  - Pandas
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
---

I always want to see all the columns.
so below the `imports`, I usually put
```python
# I can read the long column names
pd.set_option('max_colwidth', 180)
# Display all the columns
pd.set_option('display.max_columns', None)
```

Sometimes I would need to see all the rows and I came across a function:
```python
def print_full(df):
  pd.set_option('display.max_rows', len(df))
  print(df)
  pd.reset_option('displlay.max_rows')
```
It sets the options to display all the rows then resets it back to default.

I came across a better solution:

```python
# temporarily display 999 rows
with pd.option_context('display.max_rows', 999):
  print(df)
```
The option values are restored automatically when you exit the `with` block.
