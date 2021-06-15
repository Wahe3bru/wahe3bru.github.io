---
title: Complete Case Analysis
last_modified_at: 2019-10-01T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - missing data
  - notes
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "Pair-wise and list-wise deletion are methods used only if the variables missing are known to be Missing Completely At Random (MCAR). The assumption being that that the missing data is the same as randomly excluding some observations from the dataset"
---
Pair-wise and list-wise deletion are methods used only if the variables missing are known to be Missing Completely At Random (MCAR). The assumption being that that the missing data is the same as randomly excluding some observations from the dataset.

## Pair-wise deletion
This method excludes the observation from analysis using a subset of data, where the variable is missing but can still use the observation where the variables are not missing.
An example of that would be using Pandas mean, `pd.mean()` has by default `skipna=True` so automatically excludes na's from the mean calculation.

## Complete-case analysis (CCA) or "list-wise deletion"
List-wise deletion removes the observation from the dataset so only complete observations are used (the complete case) for analysis.

#### Advantages
- It is easier to implement
- No manipulation of the data
- Variable distribution remains unchanged (if data is MCAR)

#### Disadvantages
- Can exclude are large fraction of the original dataset
- In production, the model won't know how to handle missing data
- if the data is not MCAR:
- - it will create a biased dataset
- - information useful for analysis will be lost

CCA should only be used if the data is MCAR. Due the loss of information, the rule of thumb is to only delete observations if the total amount of missing data ~5% of the original dataset.

Note that in production, when the model encounters an observation with missing data it can not score that observation or impute the missing variable. In reality there are more often than not data missing and therefore it is best to know the various imputation techniques and their limitations.
