---
title: pandas count values
last_modified_at: 2019-08-19T15:17:02-05:00
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
Since I have been googling the correct name of the method so much,
that my autofill gets it right by the 3rd letter...<br>
So I thought I would make a note-to-self _(and you, if it's useful)_

I find making notes instead of relying on google makes me more efficient/productive
so that I don't break the flow. I don't suggest that anyone should memorize a library/api
especially one so big as Pandas! <br>
But if you find yourself making the same mistake or googling something simple quite often,
it's prolly best to make a note.

I use [anki](https://apps.ankiweb.net/) to help me memorize and will often include mistakes like above
so that I will stop doing it.<br>
For something as basic as `df['colA'].count_values()`, or `df['colA'].values_count()`,
move the 's' around and then _flow_ broken and I have to google "pandas v" and the solution pops up.

#### [pandas.Series.value_counts()](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.value_counts.html)
"The resulting object will be in descending order so that the first element is the most frequently-occurring element. Excludes NA values by default"
has five parameters:
- __normalize__: default False, but if True would return relative frequencies of the unique values.
- __sort__: default to True, sorts by frequencies (descending, see below).
-__ascending__: default False, sort in ascending order.
-__dropna__: default True, doesn't include counts of NaN.
-__bins__: optional, groups the numbers into half-open bins - number supplied by user. Only works for numerical Data.

returns a Series with the index as the value and the series value, the index.

The result is very similar to df.groupby('colA')['colA'].count() <br>
[so what's the difference?](https://stackoverflow.com/questions/47487753/when-is-it-appropriate-to-use-df-value-counts-vs-df-groupby-count)
Besides the obvious that `.groupby()` returns a groupby object that much more statistical functions can be performed, and
`.value_counts()` can only be performed on a Series, not a DataFrame.

The main difference will be that the result would be ordered by the __frequency__ with `value_counts`<br>
and the result of `groupby.count` will be ordered by index
