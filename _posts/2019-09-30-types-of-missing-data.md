---
title: Types of Missing Data
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
  overlay_image: https://source.unsplash.com/AOHEF53lTGk/1024x720
excerpt: "Understanding the reason for which data is missing is important in deciding which methods to impute "
---
Missing data occurs when there is no value stored for certain variable in an observation.
Data can be missing for a multitude of reasons.
- the value was forgotten/lost/not stored properly
- in a survey the question might not have been asked
- for a specific observation, the value might not exist
- the value is unknown

### Missing Data Mechanisms
There are 3 mechanisms that lead to missing data, 2 of them involve missing data randomly or almost-randomly, and the third one involves a systematic loss of data.

#### Missing At Random
When there is a relationship between the observed data and the propensity of missing data. The probability of data missing is dependent on other variables.
eg. Fitter people are more likely to disclose their weight than unfit people. Therefore there will be weight information missing at random for individuals who do not disclose their weight, but because the unfit are less likely to disclose their weight, there will be more missing weight information than the fit individuals. If the weight information is to be used, we can control for the bias by adding a fitness indicator.

#### Missing Not At Random
There is a mechanism or reason why missing values are introduced in the dataset. For example a study that advertises at a university campus will have many missing age groups as the volunteers would be of very similar ages.

#### Missing Completely At Random
The probability of a variable missing is the same for all the observations. There is no relationship between the data missing and other values, observed or missing, within the dataset. There is nothing systematic going on that makes it more likely that some data to be missing more than other data. Therefore if we disregard the observations where data is missing completely at random, we __do not bias the inferences__ made.

Understanding the reason for which data is missing is important in deciding which methods to impute (or disregard) the missing values.
