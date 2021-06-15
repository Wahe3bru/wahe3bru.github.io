---
title: Missing Data Series
last_modified_at: 2019-09-30T15:17:02-05:00
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
excerpt:
---

Data scientists spend a lot of their time cleaning data. After cleaning it, the next step would be
in detecting and dealing with missing values before they can do some feature engineering.
In this series I would like to summarize what I have learned in dealing with missing data.
I will update this list as write each post.

__Imputations - important to note__
Imputation should be done over the training set, and then propagated to the test set. This means that the mean / median to be used to fill missing values both in train and test set, should be extracted from the train set only. And this is to avoid overfitting.

- [Detecting missing data]()
- [Types of missing data](/_posts/2019-09-30-types-of-missing-data.md)
- [Missing data imputation: Complete Case Analysis - list-wise & pair-wise deletion](/_posts/2019-10-01-complete-case-analysis.md)
- [Missing data imputation: Mean, median imputation](/_posts/2019-10-02-mean,-median-and-mode-imputation.md)
- [Missing data imputation: Arbitrary value imputation](/_posts/2019-10-03-arbitrary-value-imputation.md)
- [Missing data imputation: End distribution imputation](/_posts/2019-10-05-end-distribution-imputation.md)
- [Missing data imputation: Frequent category imputation](/_posts/2019-10-08-frequent-category-imputation.md)
- [Missing data imputation: Missing category imputation](/_posts/2019-10-03-arbitrary-value-imputation.md)
- [Missing data imputation: Random sample imputation](/_posts/2019-10-11-random-sample-imputation.md)
- [Missing data imputation: Missing indicator](/_posts/2019-10-12-missing-indicator.md)
