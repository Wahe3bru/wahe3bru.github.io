---
title: Selecting dtypes from Pandas DataFrame
last_modified_at: 2019-10-17T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Pandas
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt:
---
While doing an exercise in DataCamp that involved mean imputation, I came across a handy method to
select specific data types called `pd.select_dtypes()` - such an intuitive name, how come it took so long for me to come across it?
```Python
# Import imputer module
from sklearn.impute import SimpleImputer

# Subset numeric features: numeric_cols
numeric_cols = loan_data.select_dtypes(include=[np.number])

# Impute with mean
imp_mean = SimpleImputer(strategy='mean')
loans_imp_mean = imp_mean.fit_transform(numeric_cols)

# Convert returned array to DataFrame
loans_imp_meanDF = pd.DataFrame(loans_imp_mean, columns=numeric_cols.columns)

# Check for missing values
print(loans_imp_meanDF.info())
```
In the example above, numeric columns containing both float and integer types are selected using `.select_dtypes(include=[np.number])` alternatively `.select_dtypes(include='number')`

The select_dtypes method also has an `exclude` parameter which would be the inverse of `include`.

as per the Pandas [documentaion](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.select_dtypes.html)
- To select all numeric types, use np.number or 'number'
- To select strings you must use the object dtype, but note that this will return all object dtype columns
- To select datetimes, use np.datetime64, 'datetime' or 'datetime64'
- To select timedeltas, use np.timedelta64, 'timedelta' or 'timedelta64'
- To select Pandas categorical dtypes, use 'category'
