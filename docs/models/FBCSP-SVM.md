---
layout: default
title: FBCSP-SVM
parent: Models
nav_order: 3
---

# FBCSP-SVM Usage

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_FBCSP_SVM.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Preparation for FBCSP_SVM's input

An example of FBCSP_SVM's input on the BCIC IV 2a dataset (All settings are set up as optimal settings in the original paper).

### Downloading a particular dataset
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/download_datasets.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python download_datasets.py --dataset 'BCIC2a'
```
---
### Preprocessing based on Filter Bank Common Spatial Pattern (FBCSP). over the considered dataset 
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/prep_FBCSP.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python prep_FBCSP.py --dataset 'BCIC2a'
```
---
### Build, fit, and evaluate FBCSP_SVM
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_FBCSP_SVM.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
# Subject-dependent MI classification
python run_FBCSP_SVM.py --model_name 'FBCSP_SVM' --dataset 'BCIC2a' --train_type 'subject_dependent' --data_type 'fbcsp' --num_class 2  --num_chs 20 

# Subject-independent MI classification
python run_FBCSP_SVM.py --model_name 'FBCSP_SVM' --dataset 'BCIC2a' --train_type 'subject_independent' --data_type 'fbcsp' --num_class 2  --num_chs 20 
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  model_name  | `str` prefix to save model | 'FBCSP_SVM' |
|  dataset     | `str` prefix to pick up a particular dataset and save model | 'BCIC2a'|
|  train_type  | `str` prefix to pick up a particular traning manner and save model | 'subject_dependent'|
|  data_type   | `str` prefix to select data type of input | 'time_domain' |
| num_class    | `int` number of classes  | 2  |
| num_chs      | `int` number of classes  | 20 |
| log_dir      | `str` path to save model | 'logs' |
|  subjects    | `int` or `list of int` or `None` list of range test subject, if `None`, use all subjects | `None` | -
