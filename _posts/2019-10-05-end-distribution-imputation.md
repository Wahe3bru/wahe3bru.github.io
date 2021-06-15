---
title: End distribution imputation
last_modified_at: 2019-10-10T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - missing data
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "in order not to assume that missing is at random, the missing data are replaced by a value at the end of the distribution"
---
This method is an extension of "arbitrary value imputation", but the values chosen are at the end of the variable distribution.
Depending on the distribution of the variable, the value is chosen.
- if the variable is normally distributed, then we use the mean plus 3 times the standard deviation.
- if the variable is skewed, we use the IQR proximity rule
- an alternative, is selecting the min/max value and multiply it by a certain multiple like 2 or 3.
Therefore this method is suitable for numerical variables.

#### Advantages
- easy to implement
- a fast way of obtaining a complete dataset
- can be used in production
- it captures the importance of "nothingness"

#### Disadvantages
- Distortion of the original variable distribution
- Distortion of the original variance
- Distortion of the covariance with the remaining variables of the dataset
- This technique may mask true outliers in the distribution

This technique is a particular version of arbitrary value imputation and has therefore similar advantages and disadvantages. It is used when data is assumed MNAR and therefore want to flag the observation as different.
This method is rarely used in data competitions, however, this method is used in finance companies. When capturing the financial history of customers, in order not to assume that missing is at random, the missing data are replaced by a value at the end of the distribution.
