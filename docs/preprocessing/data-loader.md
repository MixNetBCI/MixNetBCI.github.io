---
layout: default
title: Data Loader
parent: Preprocessing
nav_order: 5
---

# min2net.utils.DataLoader

[<img src="https://min2net.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/min2net/utils.py#L82){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## DataLoader class

Loading the preprocessed data of subject-dependent and subject-independent setting

```py
min2net.utils.DataLoader()
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
| dataset   | `str` dataset name ('OpenBMI', 'SMR_BCI', 'BCIC2a').|  |
| train_type    | `str` traing type ('subject_dependent', 'subject_independent'). | `None`  |
| data_type    | `str` traing type ('fbcsp', 'spectral_spatial', 'time_domain'). | `None`  |
|  num_class  | `int` number of classes | 2|
|  subject  | `int` subject ID. (start from 1) | `None` |
|  data_format  | `str` data format <br>`None` = not change,<br>'NCTD'=(#n_trial, #channels, #time, #depth), <br>'NTCD'=(#n_trial, #time, #channels, #depth), <br>'NSHWD'=(#n_trial, #n_subbands, #height, #width, #depth) | `None` |
| dataset_path | `str` path of the processed data | '/datasets' |
| **kwargs | | |

---

## load_train_set method

Loading the training set

```py
DataLoader.load_train_set(fold, **kwargs)
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  fold  | `int` fold number. (start from 1) |  |
| **kwargs | | |

**Returns:** X, y

---

## load_val_set method

Loading the validation set

```py
DataLoader.load_val_set(fold, **kwargs)
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  fold  | `int` fold number. (start from 1) |  |
| **kwargs | | |

**Returns:** X, y

---

## load_test_set method

Loading the test set

```py
DataLoader.load_test_set(fold, **kwargs)
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  fold  | `int` fold number. (start from 1) |  |
| **kwargs | | |

**Returns:** X, y

---

## Example

```py
from min2net.utils import DataLoader

loader = DataLoader(dataset='OpenBMI', 
                    train_type='subject_independent', 
                    subject=1, 
                    data_format='NTCD', 
                    data_type='time_domain', 
                    dataset_path='/datasets')

X_train, y_train = loader.load_train_set(fold=1)
X_val, y_val = loader.load_val_set(fold=1)
X_test, y_test = loader.load_test_set(fold=1)

```