---
title: Arbitrary Value Imputation
last_modified_at: 2019-10-02T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - missing data
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "The reasoning behind arbitrary value imputation is to flag the missing value with a completely different value (like -1, if the distribution is positive)"
---

This method replaces all missing values within a variable by, you guessed it, an arbitrary value.\
Typically used values are 0, 999, -999 or -1.
Categorical and numerical variables can be imputed by this method.
The reasoning behind arbitrary value imputation is to flag the missing value with a completely different value (like -1, if the distribution is positive). We obviously assume that data is not missing at random.
This method is common practice in real life data collections whereby they use an arbitrary value to signal a missing value (instead of leaving it blank which can lead to errors in their processes)

#### Advantages
- easy to implement
- a fast way of achieving complete datasets
- can be used in production
- captures the importance of "missingness"

#### Disadvantages
- Distortion of the original variable distribution
- Distortion of the original variance
- Distortion of the covariance with the remaining variables of the dataset
- it can mask or create outliers if the arbitrary value is at the end of a distribution
- careful not to have arbitrary value not too similar to any value in the variable distribution

Careful thought has to be placed in deciding the arbitrary value, as it may bias the dataset if the value is similar to the mean/mode or other value in the variable distribution and we lose the "missingness" signifier.
We can also introduce or mask outliers if the value chosen is at the extreme tail of the distribution - like choosing -999 for a variable with a positive distribution.

__Arbitrary value imputation for categorical variables__
For Categorical variables this method is widely used. This method treats the missing data as an additional label/category, by grouping all missing observations into the label "Missing".<br>
This method does not assume anything about the missing data and is well suited if the amount of missing values are high.

__additional advantage__
- it makes no assumptions on the data

__disadvantage__
- if the number of missing data is small, the "Missing" category would be a _rare_ category and may cause tree algorithms to over-fit.

For categorical variables this method of imputation is the most popular and is widely used.
