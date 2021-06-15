---
title: model persistance
last_modified_at: 2019-08-26T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
---
## AKA I have a model... now what?

After having developed a model and would like to save it for future predictions one would save via serialization.
There are two methods:
1) Pickle
2) Joblib

The [scikit learn docs](https://scikit-learn.org/stable/modules/model_persistence.html) have a good example but to simplify.

After having the model trained on your data aka `clf.fit(X, y)`<br>
saving it via __Pickle__:
```python
import pickle
# saving model to a file
with open('model.pkl', 'wb') as f:
    pickle.dump(clf, f)
```

saving via __Joblib__:
```python
from sklearn.externals import joblib
# saving model to a file
joblib.dump(clf, 'model.pkl')
```

The file is saved in the current working directory.<br>
Similarly to load the model

loading via __Pickle__:
```python
import pickle
# loading from file
with open('model.pkl', 'rb') as f:
    trained_clf = pickle.load(f)
```

loading via __Joblib__:
```python
from sklearn.externals import joblib
# loading from file
trained_clf = joblib.load('model.pkl')
```

#### Warning
Note that best practice is to save the model along with additional metadata. such as:
- The training data (or an immutable snapshot)
- the source code used to generate the model
- the version of scikit-learn and its dependencies
- the cross validation score obtained on the training data

Failure to do so might lock one in to using an old version of scikit-learn as per the documentation

>While models saved using one version of scikit-learn might load in other versions, this is entirely unsupported and inadvisable. It should also be kept in mind that operations performed on such data could give different and unexpected results.
