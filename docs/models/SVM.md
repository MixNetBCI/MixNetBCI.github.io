---
layout: default
title: SVM
parent: Models
nav_order: 1
---

# min2net.model.SVM

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/model/SVM.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## SVM class
Configures the model for training. This method was implemented based on [sklearn.svm.SVC](https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html) using [PredefinedSplit](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.PredefinedSplit.html) to predefined split cross-validation and [GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html) to tune the model.

```py
min2net.model.SVM()
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  tuned_parameters   | `list` of `dictionaries` with parameters names (`str`) as keys and lists of parameter settings for [GridSearchCV](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GridSearchCV.html) |  [\{'kernel': ['rbf'], <br>'gamma': [1e-2, 1e-3],<br>'C': [0.001, 0.01, 0.1, 1, 10, 100, 1000]\},<br>\{'kernel': ['sigmoid'],<br>'gamma': [1e-2, 1e-3],<br>'C': [0.001, 0.01, 0.1, 1, 10, 100, 1000]\},<br>\{'kernel': ['linear'],<br>'gamma': [1e-2, 1e-3],<br>'C':[0.001, 0.01, 0.1, 1, 10, 100, 1000]\}]
|  log_path    | `str` path to save model | 'logs' |
|  model_name  | `str` prefix to save model | 'SVM' |
|  **kwargs    | Keyword argument to pass into the function for replacing the variables of the model such as `seed` and `f1_average` | -
  
---
## Fit method

Fit the SVM model according to the given training and validation data. The model with an optimal parameter set will save at `'log_path'`.

```py
SVM.fit(X_train, 
        y_train, 
        X_val, 
        y_val)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|X_train   | `ndarray` Training EEG signals. shape (*#trial*, *#features*) | 
|y_train   | `ndarray` Label of training set. shape (*#trial*) |
|X_val   | `ndarray` Validation EEG signals. shape (*#trial*, *#features*) |
|y_val   | `ndarray` Label of validation set. shape (*#trial*) |
  
---
## Predict method
Generates output predictions and classification report on samples in X_test.

```py
SVM.predict(X_test, 
            y_test)
```

| Arguments | Description |
|:---|:----|
|X_test   | `ndarray` Testing EEG signals. shape (*#trial*, *#features*) | 
|y_test   | `ndarray` Label of test set. shape (*#trial*) |

**Returns:**
  >- Y: dictionary of `{y_true, y_pred}`
  >- evaluation: dictionary of `{accuracy, f1_score}`

---
## Example

```py
from min2net.model import SVM
import numpy as np

model = SVM()
model.fit(X_train, y_train, X_val, y_val)

Y, evaluation = model.predict(X_test, y_test)
```