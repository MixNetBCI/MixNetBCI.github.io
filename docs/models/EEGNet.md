---
layout: default
title: EEGNet
parent: Models
nav_order: 4
---

# EEGNet Usage

[<img src="https://min2net.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/min2net/model/EEGNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## About EEGNet
Original authors have uploaded their code here [https://github.com/vlawhern/arl-eegmodels](https://github.com/vlawhern/arl-eegmodels)

If you use the EEGNet model in your research, please cite the following paper:

```
@article{Lawhern2018,
  author={Vernon J Lawhern and Amelia J Solon and Nicholas R Waytowich and Stephen M Gordon and Chou P Hung and Brent J Lance},
  title={EEGNet: a compact convolutional neural network for EEG-based brain–computer interfaces},
  journal={Journal of Neural Engineering},
  volume={15},
  number={5},
  pages={056013},
  url={http://stacks.iop.org/1741-2552/15/i=5/a=056013},
  year={2018}
}
```
---

## Preparation for EEGNet's input

An example of EEGNet's input on the BCIC IV 2a dataset (All settings are set up as optimal settings in the original paper).

### Downloading a particular dataset
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/download_datasets.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python download_datasets.py --dataset 'BCIC2a'
```
---
### Preprocessing based on time domain EEG over the considered dataset 
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/prep_time_domain.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python prep_time_domain.py --dataset 'BCIC2a'
```
---
### Build, fit, and evaluate EEGNet
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_EEGNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
# Subject-dependent MI classification
python run_EEGNet.py --model_name 'EEGNet' --dataset 'BCIC2a' --train_type 'subject_dependent' --data_type 'time_domain' --num_class 2  --num_chs 20 --GPU 0

# Subject-independent MI classification
python run_EEGNet.py --model_name 'EEGNet' --dataset 'BCIC2a' --train_type 'subject_independent' --data_type 'time_domain' --num_class 2  --num_chs 20 --GPU 0
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  model_name  | `str` prefix to save model | 'EEGNet' |
|  dataset     | `str` prefix to pick up a particular dataset and save model | 'BCIC2a'|
|  train_type  | `str` prefix to pick up a particular traning manner and save model | 'subject_dependent'|
|  data_type   | `str` prefix to select data type of input | 'time_domain' |
| num_class    | `int` number of classes  | 2  |
| num_chs      | `int` number of classes  | 20 |
| log_dir      | `str` path to save model | 'logs' |
|  subjects    | `int` or `list of int` or `None` list of range test subject, if `None`, use all subjects | `None` |
|  GPU         |  `str` select GPU ID | 0 | -