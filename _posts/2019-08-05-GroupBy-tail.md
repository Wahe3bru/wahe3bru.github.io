---
title: "Viewing the last n rows of each group"
last_modified_at: 2019-08-05T10:20:02-05:00
categories:
  - blog
tags:
  - python
  - Pandas
classes: wide
---

In  a project I am working on, I was taking the logs of work done and predicting
 the expected date that purchased hours would be consumed.

The resulted dataframe had the necessary columns from the logs as well as others
 created by me including the predicted date.

To view the last entry of each contractID was as simple as grouping by ContractID and viewing the tail:
```python
new_table.groupby('contractID').tail(1)
```
According to [pandas documentation](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.core.groupby.GroupBy.tail.html) its
 > Essentially equivalent to .apply(lambda x: x.tail(n)), except ignores as_index flag.

similarly one can view the beginning by using - you guessed it - .head() - both default to 5 rows (n = 5)
