---
layout: default
title: MixNet
parent: Models
nav_order: 1
---

# MixNet Usage

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_MixNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 



{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## Preparation for MixNet's input

An example of MixNet's input on the BCIC IV 2a dataset (All settings are set up as optimal settings in the original paper).

### Downloading a particular dataset
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/download_datasets.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python download_datasets.py --dataset 'BCIC2a'
```
---
### Preprocessing based on Spectral Spatial Signals generation over the considered dataset 
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/prep_spectral_spatial_signals.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python prep_spectral_spatial_signals.py --dataset 'BCIC2a'
```
---
### Build, fit, and evaluate MixNet
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_MixNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
# Subject-dependent MI classification
python run_MixNet.py --model_name 'MixNet' --dataset 'BCIC2a' --train_type 'subject_dependent' --data_type 'spectral_spatial_signals' --adaptive_gradient True --policy 'HistoricalTangentSlope' --log_dir 'logs' --num_class 2 --GPU 0 --margin 1.0 --n_component 2 --warmup 7

# Subject-independent MI classification
python run_MixNet.py --model_name 'MixNet' --dataset 'BCIC2a' --train_type 'subject_independent' --data_type 'spectral_spatial_signals' --adaptive_gradient True --policy 'HistoricalTangentSlope' --log_dir 'logs' --num_class 2 --GPU 0 --margin 0.1 --n_component 4 --latent_dim 128 --warmup 5
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  model_name  | `str` prefix to save model | 'MixNet' |
|  dataset     | `str` prefix to pick up a particular dataset and save model | 'BCIC2a'|
|  train_type  | `str` prefix to pick up a particular traning manner and save model | 'subject_dependent'|
|  data_type   | `str` prefix to select data type of input | 'spectral_spatial_signals' |
| num_class    | `int` number of classes  | 2  |
| latent_dim   |`int` or `None`. If `None`, latent_dim is equal to number of CSP components multiply by nunber of frequency bands `U x Nb` |`None`|
| adaptive_gradient | `str2bool` to use adaptive loss weights  | `True` |
|  policy      | `str` adaptive gradient policy for MixNet | 'HistoricalTangentSlope' |
| log_dir      | `str` path to save model | 'logs' |
|  subjects    | `int` or `list of int` or `None` list of range test subject, if `None`, use all subjects | `None` |
|  margin      | `float` margin (alpha) of Triplet loss| 1.0 |
|  n_component | `int` number of CSP components used | `None` |
|  warmup      | `int` warm-up period of adaptive gradient bleding |  5 |
|  GPU         |  `str` select GPU ID | 0 | -
