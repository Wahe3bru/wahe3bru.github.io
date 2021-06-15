---
title: Frequent category imputation
last_modified_at: 2019-08-10T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - missing data
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "Frequent category imputation replaces all missing values within a variable
with the most frequent value/category"
---
Frequent category imputation also known as mode imputation replaces all missing values within a variable
with the most frequent value/category.
It is mostly used for categorical variables, but can be used for numerical.
This method is used on the assumption that data is MCAR, and therefore the missing data is most likely similar to the
most frequent value of the varirable.

#### Advantages
- easy to implement
- fast way to complete datasets
- can be used in production

#### Disadvantages
- It distorts the relation between the most frequent value with other variables in the dataset
- if there's a lot of missing values, it can result in an overrepresentation of the most frequent value.

Therefore this method should only be used when the missing data is no more than 5% of the variable.
