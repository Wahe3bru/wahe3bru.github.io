---
title: Missing Indicator
last_modified_at: 2019-10-11T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - missing data
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt:
---
This Technique adds an additional binary variable indicating if the observation was missing or not. It's used in combination with other imputation techniques that are used when the data is MCAR.

It is commonly used together:

- Mean / median imputation + missing indicator (Numerical variables)
- Frequent category imputation + missing indicator (Categorical variables)
- Random sample Imputation + missing indicator (Numerical and categorical)

#### Advantages
- easy to implement
- captures the importance of missing data

#### Disadvantages
- expands the feature space
- the original variable still needs to imputed

For each missing variable, an additional variable is created. This increases the feature space. Additionally, missing data tends to be the same for observations across multiple variables leading to the missing indicator variables being very similar or identical to each other.

For example: data that is not MCAR, the imputation techniques to be used like example arbitrary value imputation or end of distribution imputation, would affect the variable distribution dramatically, making it not suitable for training a linear model on.
Alternatively one can use the mean/median imputation combined with the missing indicator to flag those missing observations.
This covers two angles; if data is MCAR - mean imputation, if data is not - it would be captured by the missing indicator.
