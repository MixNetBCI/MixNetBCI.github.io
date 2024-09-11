---
layout: default
title: Data Loader
parent: Preprocessing
nav_order: 5
---

# mixnet.utils.DataLoader

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/mixnet/utils.py#L175){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## DataLoader class

Loading the preprocessed data of subject-dependent and subject-independent setting

```py
mixnet.utils.DataLoader()
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
| dataset   | `str` dataset name (‘BCIC2a’, ‘BCIC2b’, ‘BNCI2015_001’, ‘SMR_BCI’, ‘HighGamma’,  ‘OpenBMI’).|  |
| train_type    | `str` traing type ('subject_dependent', 'subject_independent'). | `None`  |
| data_type    | `str` traing type ('fbcsp', 'spectral_spatial', 'time_domain', 'spectral_spatial_signals'). | `None`  |
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

## Example 1: DataLoader for MIN2Net

```py
from mixnet.utils import DataLoader

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

## Example 2: DataLoader for MixNet

```py
from mixnet.utils import DataLoader

loader = DataLoader(dataset='OpenBMI', 
                    train_type='subject_independent', 
                    subject=1, 
                    data_format='NTCD', 
                    data_type='spectral_spatial_signals', 
                    dataset_path='/datasets')

X_train, y_train = loader.load_train_set(fold=1)
X_val, y_val = loader.load_val_set(fold=1)
X_test, y_test = loader.load_test_set(fold=1)

```

## Example 3: DataLoader for EEGNet and DeepConvNet

```py
from mixnet.utils import DataLoader

loader = DataLoader(dataset='OpenBMI', 
                    train_type='subject_independent', 
                    subject=1, 
                    data_format='NDCT', 
                    data_type='time_domain', 
                    dataset_path='/datasets')

X_train, y_train = loader.load_train_set(fold=1)
X_val, y_val = loader.load_val_set(fold=1)
X_test, y_test = loader.load_test_set(fold=1)

```