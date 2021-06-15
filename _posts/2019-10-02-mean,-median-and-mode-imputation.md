---
title: Mean, Median and Mode Imputation
last_modified_at: 2019-10-01T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - missing data
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "If a variable is normally distributed, the mean, median and mode, are approximately the same. Therefore, replacing missing values by the mean or the median are equivalent."
---
This method of imputation replaces the missing values with either the _mean_ (if the variable has a normal distribution) or _median_ (if the variable distribution is skewed). The mode is rarely used, and would be project specific. It can only be used on numerical variables, both continuous and discrete.

This method is used when the data is MCAR, therefore assumes that the missing observations would probably look like the majority of the observations.

#### Advantages
- easy to implement
- a fast way of getting a complete dataset
- can be used in production

#### Disadvantages
- Distortion of the original variable distribution
- Distortion of the original variance
- Distortion of the covariance with the remaining variables of the dataset

If the total missing variables is large, then replacing them with the mean/median will distort the variance, leading to a possible underestimation of the variance. It might also affect the correlation and covariances with other variables in the dataset. Concentrating all missing values at the mean/median value might lead to common observations in the distribution being picked up as outliers.

Therefore this method should be used with missing data ~5% of the variable.

Note that because of the simplicity of this technique it is very commonly used, even if the data is not MCAR or there is alot of data. Adding a "missing indicator" column is usually combined to capture those observations whose data was missing. This helps in two ways; if the data is MCAR then the mean/median imputation would capture it, if it wasn't  - the missing indicator does.
