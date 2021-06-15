---
title: 100 pandas puzzles
last_modified_at: 2019-09-17T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Pandas
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "Revision is always good. Every now and then I like to review the basics and test myself at the intermediary level"
---
I am continuously learning new things, and relearning in some cases. There are alot of
tricks to solving a problem, especially a programming one. I like to learn the best practice version, as
well as the hack method. I prefer to understand processes and the reasoning behind it. That way
I don't need to remember every method but rather workout the solution logically, or at the very least be
able to google it quickly and efficiently.

Revision is always good. Every now and then I like to review the basics and test myself at the intermediary level. That's why I love helping others, sometimes they will ask interesting questions that really challenge my understanding. I am not to proud to tell them "I don't know" - but I always get back to them with either the solution or ways to go about finding it.

I found [100 pandas puzzles](https://github.com/ajcr/100-pandas-puzzles) and thought it would be a cool review, I may learn something I had forgotten :)

**1.** Import pandas under the name `pd`.
`import pandas as pd`


**2.** Print the version of pandas that has been imported.
`pd.__version__`

**3.** Print out all the version information of the libraries that are required by the pandas library.
`pd.show_versions()`

Consider the following Python dictionary `data` and Python list `labels`:

``` python
data = {'animal': ['cat', 'cat', 'snake', 'dog', 'dog', 'cat', 'snake', 'cat', 'dog', 'dog'],
        'age': [2.5, 3, 0.5, np.nan, 5, 2, 4.5, np.nan, 7, 3],
        'visits': [1, 3, 2, 3, 2, 3, 1, 1, 2, 1],
        'priority': ['yes', 'yes', 'no', 'yes', 'no', 'no', 'no', 'yes', 'no', 'no']}

labels = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j']
```
(This is just some meaningless data I made up with the theme of animals and trips to a vet.)

**4.** Create a DataFrame `df` from this dictionary `data` which has the index `labels`.
`df= pd.DataFrame(data=data, index=labels)`

**5.** Display a summary of the basic information about this DataFrame and its data.
`df.describe()`

**6.** Return the first 3 rows of the DataFrame `df`.
df.head(3)

**7.** Select just the 'animal' and 'age' columns from the DataFrame `df`.
df[['animal', 'age']]

**8.** Select the data in rows `[3, 4, 8]` *and* in columns `['animal', 'age']`.
`df.iloc[[3,4,6]][['animal', 'age']]`

**9.** Select only the rows where the number of visits is greater than 3.
`df[df.visits >= 3]`

**10.** Select the rows where the age is missing, i.e. is `NaN`.
`df[df.age.isna()]`

**11.** Select the rows where the animal is a cat *and* the age is less than 3.
`df.query('animal == "cat" and age < 3')`

**12.** Select the rows the age is between 2 and 4 (inclusive).
`df.query('2 <= age <=4')`
or
`df[(2 <= df.age) & (df.age<= 4)]`

**13.** Change the age in row 'f' to 1.5.
`df.loc['f']['age'] = 1.5`

**14.** Calculate the sum of all visits (the total number of visits).
`df.visits.sum()`

**15.** Calculate the mean age for each different animal in `df`.
`df.groupby('animal')['age'].mean()`

**16.** Append a new row 'k' to `df` with your choice of values for each column. Then delete that row to return the original DataFrame.

```Python
df.loc['k'] = ['mouse', 1, 3, 'no']
df.drop('k', inplace=True)
```
**17.** Count the number of each type of animal in `df`.
`df.groupby('animal')['age'].count()`

**18.** Sort `df` first by the values in the 'age' in *decending* order, then by the value in the 'visit' column in *ascending* order.

`df.sort_values(['age', 'visits'], ascending=[False, True])`
`na_position='first'` would sort with the `na`'s displayed on top.

**19.** The 'priority' column contains the values 'yes' and 'no'. Replace this column with a column of boolean values: 'yes' should be `True` and 'no' should be `False`.

`df['priority'] = df.priority.map({'yes': True, 'no': False})`
my favourite way, but I found this [awesome answer](https://stackoverflow.com/questions/40901770/is-there-a-simple-way-to-change-a-column-of-yes-no-to-1-0-in-a-pandas-dataframe) that not only shows multiple ways but also how long each method takes.

**20.** In the 'animal' column, change the 'snake' entries to 'python'.
df.animal = df.animal.str.replace('snake', 'python')

**21.** For each animal type and each number of visits, find the mean age. In other words, each row is an animal, each column is a number of visits and the values are the mean ages (hint: use a pivot table).
`df.pivot_table(index='animal', columns='visits', values='age')`
*This last one I had to google. I had the params correct but was using `.pivot` instead of `.pivot_table`

That was the basics done. Not much trouble, but the next set of questions look interesting and should provide more of a challenge.
