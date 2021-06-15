---
title: is it datetime yet
last_modified_at: 2019-08-29T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "It took me an embarrassingly long time to figure that out"
---

In my current project I import data from open tickets and give an estimated time to completion.
What I realised after the fourth iteration was that sometimes a column is not always imported as a datetime object and
rather as string.<br>
It's easy to convert to a datetime object as the format is always the same `%Y-%m-%d` eg 2019-08-24

#### How do I know if the element in the column is different?
So it turns out that sometimes a due date is not entered and defaults to all zeros. <br>
It took me an embarrassingly long time to figure that out.<br>
luckily, once again the [view more lines in the dataframe](https://wahe3bru.github.io/blog/see-all-the-rows-in-pandas/) technique was
used to help me view the data until I discovered the all zeros thing.<br>
anyhoo, I knew there had to be datetime check similar to `isdigit()` or `isinstance()` and [there is](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.api.types.is_datetime64_any_dtype.html)!

This is how I used it:
So a lil background. I wanted to create a feature which was the number of hours the ticket was due.
Easy calculation (in pandas), basicaly the `DueDateTime - CreateDateTime` and extract the hours with `.astype('timedelta64[h]')`
So if there's no DueDateTime I would use an old date so the hours would be negative - which can easily be filtered and dealt with.

```python
from pandas.api.types import is_datetime64_any_dtype as is_datetime


if not is_datetime(df['DueDateTime']):
        old_date = datetime.strptime("2018-01-01 12:00:00", "%Y-%m-%d %H:%M:%S")

        for i in df.index:
            if type(df.at[i, 'DueDateTime']) == str:
                df.at[i, 'DueDateTime'] = old_date

        df['DueDateTime'] = df['DueDateTime'].astype('datetime64[ns]')
```

There is code can definitely be refactored but after meeting with the dba, he suggested
that I don't use the DueDateTime column as it is not reliable and is not used by anyone and will prolly be removed soon.

Atleast I learned something new and have a feeling it will come in handy one day.
