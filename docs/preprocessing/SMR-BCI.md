---
layout: default
title: SMR_BCI dataset
parent: Preprocessing
nav_order: 3
---

# min2net.preprocessing.SMR_BCI

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/tree/main/preprocessing/SMR_BCI){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .fs-6 .fw-300 }

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Time domain

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/preprocessing/SMR_BCI/time_domain.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

### Subject-dependent setting

Preprocess raw time-series EEG in subject-dependent setting using butter bandpass filter and resampling. Split data into train, validation and test sets using stratified k-fold cross-validation.

```py
time_domain.subject_dependent(k_folds, 
                              pick_smp_freq,
                              bands, 
                              order, 
                              save_path,
                              num_class,
                              sel_chs)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|k_folds           | `int` number of k-fold cross-validation. |
| pick_smp_freq    | `int` pick sample frequency (downsampling EEG to to `pick_smp_freq`) |
| bands            | `list`  list of low cut and high cut frequency bands e.g. `[8, 30]` |
| order            | `int` number of order of butter bandpass filter  |
| save_path        | `str` path to save processed EEG  |
| num_class        | `int` number of classes. Default 2|
| sel_chs          | `list` or `None`. list if EEG channels. Default `None` |

**Example**
```py
import min2net.preprocessing as prep

prep.SMR_BCI.time_domain.subject_dependent_setting(k_folds=5,
                                                 pick_smp_freq=100, 
                                                 bands=[8, 30], 
                                                 order=5, 
                                                 save_path='datasets')
```

### Subject-independent setting

Preprocess raw time-series EEG in subject-independent setting using butter bandpass filter and resampling. Split data into train, validation and test sets using stratified k-fold cross-validation.

```py
time_domain.subject_independent(k_folds, 
                                pick_smp_freq,
                                bands, 
                                order, 
                                save_path,
                                num_class,
                                sel_chs)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|k_folds           | `int` number of k-fold cross-validation. |
| pick_smp_freq    | `int` pick sample frequency (downsampling EEG to to `pick_smp_freq`) |
| bands            | `list`  list of low cut and high cut frequency bands e.g. `[8, 30]` |
| order            | `int` number of order of butter bandpass filter  |
| save_path        | `str` path to save processed EEG  |
| num_class        | `int` number of classes. Default 2|
| sel_chs          | `list` or `None`. list if EEG channels. Default `None` |

**Example**
```py
import min2net.preprocessing as prep

prep.SMR_BCI.time_domain.subject_independent_setting(k_folds=5,
                                                    pick_smp_freq=100, 
                                                    bands=[8, 30], 
                                                    order=5, 
                                                    save_path='datasets')
```
---

## Filter Bank Common Spatial Pattern (FBCSP)

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/preprocessing/SMR_BCI/fbcsp.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

### Subject-dependent setting

Preprocess raw time-series EEG in subject-dependent setting using Filter Bank Common Spatial Pattern (FBCSP). Split data into train, validation and test sets using stratified k-fold cross-validation.

```py
fbcsp.subject_dependent(k_folds, 
                        pick_smp_freq, 
                        n_components, 
                        bands, 
                        n_features, 
                        order, 
                        save_path,
                        num_class,
                        sel_chs)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|k_folds           | `int` number of k-fold cross-validation. |
| pick_smp_freq    | `int` pick sample frequency (downsampling EEG to to `pick_smp_freq`) |
 | n_components            | `int` number of components of CSP|
| bands            | `list`  list of low cut and high cut frequency bands of filter bank e.g. `[[4, 8], [8, 12], ...]` |
| n_features | `int` number of features for mutual_info_classif |
| order            | `int` number of order of butter bandpass filter  |
| save_path        | `str` path to save processed EEG  |
| num_class        | `int` number of classes. Default 2|
| sel_chs          | `list` or `None`. list if EEG channels. Default `None` |

**Example**
```py
import min2net.preprocessing as prep

bands = [[4, 8], [8, 12], [12, 16], 
         [16, 20], [20, 24], [24, 28], 
         [28, 32], [32, 36], [36, 40]]

prep.SMR_BCI.fbcsp.subject_dependent_setting(k_folds=5, 
                                            pick_smp_freq=100, 
                                            n_components=4, 
                                            bands=bands, 
                                            n_features=8, 
                                            order=5, 
                                            save_path='datasets')
```

### Subject-independent setting

Preprocess raw time-series EEG in subject-independent setting using Filter Bank Common Spatial Pattern (FBCSP). Split data into train, validation and test sets using stratified k-fold cross-validation.

```py
fbcsp.subject_independent(k_folds, 
                          pick_smp_freq, 
                          n_components, 
                          bands, 
                          n_features, 
                          order, 
                          save_path,
                          num_class,
                          sel_chs)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|k_folds           | `int` number of k-fold cross-validation. |
| pick_smp_freq    | `int` pick sample frequency (downsampling EEG to to `pick_smp_freq`) |
 | n_components            | `int` number of components of CSP|
| bands            | `list`  list of low cut and high cut frequency bands of filter bank e.g. `[[4, 8], [8, 12], ...]` |
| n_features | `int` number of features for mutual_info_classif |
| order            | `int` number of order of butter bandpass filter  |
| save_path        | `str` path to save processed EEG  |
| num_class        | `int` number of classes. Default 2|
| sel_chs          | `list` or `None`. list if EEG channels. Default `None` |

**Example**
```py
import min2net.preprocessing as prep

bands = [[4, 8], [8, 12], [12, 16], 
         [16, 20], [20, 24], [24, 28], 
         [28, 32], [32, 36], [36, 40]]

prep.SMR_BCI.fbcsp.subject_independent_setting(k_folds=5, 
                                              pick_smp_freq=100, 
                                              n_components=4, 
                                              bands=bands, 
                                              n_features=8, 
                                              order=5, 
                                              save_path='datasets')
```

---
## Spectral Spatial mapping

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/preprocessing/SMR_BCI/spectral_spatial.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

### Subject-dependent setting
 Preprocess raw time-series EEG in subject-dependent setting using Spectral Spatial mapping. Split data into train, validation and test sets using stratified k-fold cross-validation.

```py
spectral_spatial.subject_dependent(k_folds, 
                                   pick_smp_freq, 
                                   n_components, 
                                   bands, 
                                   n_features, 
                                   order, 
                                   save_path,
                                   num_class,
                                   sel_chs)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|k_folds           | `int` number of k-fold cross-validation. |
| pick_smp_freq    | `int` pick sample frequency (downsampling EEG to to `pick_smp_freq`) |
 | n_components            | `int` number of components of CSP|
| bands            | `list`  list of low cut and high cut frequency bands of filter bank e.g. `[[4, 8], [8, 12], ...]` |
| n_pick_bands | `int` number of filter bands|
| n_features | `int` number of features for mutual_info_classif |
| order            | `int` number of order of butter bandpass filter  |
| save_path        | `str` path to save processed EEG  |
| num_class        | `int` number of classes. Default 2|
| sel_chs          | `list` or `None`. list if EEG channels. Default `None` |

**Example**
```py
import min2net.preprocessing as prep

bands = [[7.5,14],[11,13],[10,14],[9,12],[19,22],
         [16,22],[26,34],[17.5,20.5],[7,30],[5,14],
         [11,31],[12,18],[7,9],[15,17],[25,30],
         [20,25],[5,10],[10,25],[15,30],[10,12],
         [23,27],[28,32],[12,33],[11,22],[5,8],
         [7.5,17.5],[23,26],[5,20],[5,25],[10,20]]

prep.SMR_BCI.spectral_spatial.subject_dependent_setting(k_folds=5, 
                                                       pick_smp_freq=100, 
                                                       n_components=10, 
                                                       bands=bands, 
                                                       n_pick_bands=20, 
                                                       order=5, 
                                                       save_path='datasets')
```

### Subject-independent setting

Preprocess raw time-series EEG in subject-independent setting using Spectral Spatial mapping. Split data into train, validation and test sets using stratified k-fold cross-validation.

```py
spectral_spatial.subject_independent(k_folds, 
                                     pick_smp_freq, 
                                     n_components, 
                                     bands, 
                                     n_features, 
                                     order, 
                                     save_path,
                                     num_class,
                                     sel_chs)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|k_folds           | `int` number of k-fold cross-validation. |
| pick_smp_freq    | `int` pick sample frequency (downsampling EEG to to `pick_smp_freq`) |
 | n_components            | `int` number of components of CSP|
| bands            | `list`  list of low cut and high cut frequency bands of filter bank e.g. `[[4, 8], [8, 12], ...]` |
| n_pick_bands | `int` number of filter bands|
| n_features | `int` number of features for mutual_info_classif |
| order            | `int` number of order of butter bandpass filter  |
| save_path        | `str` path to save processed EEG  |
| num_class        | `int` number of classes. Default 2|
| sel_chs          | `list` or `None`. list if EEG channels. Default `None` |

**Example**
```py
import min2net.preprocessing as prep

bands = [[7.5,14],[11,13],[10,14],[9,12],[19,22],
         [16,22],[26,34],[17.5,20.5],[7,30],[5,14],
         [11,31],[12,18],[7,9],[15,17],[25,30],
         [20,25],[5,10],[10,25],[15,30],[10,12],
         [23,27],[28,32],[12,33],[11,22],[5,8],
         [7.5,17.5],[23,26],[5,20],[5,25],[10,20]]

prep.SMR_BCI.spectral_spatial.subject_independent_setting(k_folds=5, 
                                                         pick_smp_freq=100, 
                                                         n_components=10, 
                                                         bands=bands, 
                                                         n_pick_bands=20, 
                                                         order=5, 
                                                         save_path='datasets')
```