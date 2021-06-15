---
title: Random Sample Imputation
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

Random Sample imputation method is similar to [mean/median imputation](/_posts/2019-10-02-mean,-median-and-mode-imputation.md) in that it preserves the statistical parameters of the variable.
In this method one replaces a missing value from a pool of available values randomly. Thereby preserving the mean and standard deviation of numerical variables. When using this method on categorical variables, we maintain the frequency of the different labels present in the variable.

This technique is used when the data is assumed to be MCAR. Therefore substituting missing values from the variable distribution won't affect the overall distribution.

#### Advantages
- easy to implement
- fast way to complete datasets
- preserves the variance of the variable

#### Disadvantages
- randomness
- the relationship between imputed variables with other variables might be distorted if there are alot of missing values
- if used in production it can be memmory heavy as the original training set needs to be stored to extract replacement values for future observations.

Random Sample imputation is well suited for linear models as it does not distort the distribution, regardless of the amount of missing values. It should however be used when the missing data is MCAR and not more than 5% of the variable.

__note:__ Randomness can be an issue, especially in model training and selection. It can also be an issue for testing. Therefore a randomness needs to be controlled by setting the seed.
