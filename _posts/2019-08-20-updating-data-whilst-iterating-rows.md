---
title: Updating data whilst iterating rows
last_modified_at: 2019-08-20T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Pandas
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
---
On a current project I am working on, I imported the first 6 months of this year
to develop a model for ~~redacted~~ work.
After initial development I used the 7th month as a validation set.

The problem I came across was that the `DueDate` column was not datetime type.
hmmm... <br>
the same SQL query with the dates changed read the 3 date columns as datetimes.
luckily I used the [view all rows trick](https://wahe3bru.github.io/blog/see-all-the-rows-in-pandas/) to look for non-date type strings (as the column type was 'Object')

!['found the culprit'](/assets/images/datecolzeros.PNG)

Turns out between rows 908 and 986 the datetime was set to zeros - must have been a problem with the system they used.

So how to go about fixing it?

In searching for a solution I came across this [stackoverflow post](https://stackoverflow.com/a/48951427) <br>
_piRSquared_ (the answerer) was quite thorough in their answer but the takeaways were:
These were deprecated:
- `pd.DateFrame.set_value`
- `pd.DateFrame.ix`
These are possibe methods
- `pd.DataFrame.loc`
but the _recommendation_ was to use `pd.DataFrame.at`

Using this knowledge, this is how I solved my problem:
```python
from pandas.api.types import is_datetime64_any_dtype as is_datetime

# within a preprocessing function
old_date = datetime.strptime("2018-01-01 12:00:00", "%Y-%m-%d %H:%M:%S")

if not is_datetime(df['DueDateTime']):
        for i in df.index:
            if type(df.at[i, 'DueDateTime']) == str:
                df.at[i, 'DueDateTime'] = old_date

        df['DueDate'] = df['DueDate'].astype('datetime64[ns]')
```
explanation:
I created an `old_date` datetime object. <br>
after checking if the column is __not__ a datetime using [`is_datetime`](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.api.types.is_datetime64_any_dtype.html)

- loop over the index of the dataframe checking if the element type in `DueDate` is a string
- replace the string (which would be all zeros) with `old_date`
- finally convert `DueDate` column to a datetime type

I used the DueDate column to calculate:
```python
df['Due_in_hours'] = (df.DueDate - df.CreateDate).astype('timedelta64[h]')
```
To avoid negative hours I apply the below function the `Due_in_hours`
```python
def no_negative_hours_due(hours):
    '''replace negative hours with zero'''

    if hours < 0 :
        return 0
    return hours
```
It could probably be done in a lambda but I am writing functions for documentation - to help others who have to look at the code
as well as to assist in practicing unit tests using `pytest`.
