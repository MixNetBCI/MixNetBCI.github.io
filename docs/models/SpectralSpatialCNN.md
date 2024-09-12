---
layout: default
title: SpectralSpatialCNN
parent: Models
nav_order: 6
---

# SpectralSpatialCNN Usage

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_SpectralSpatialCNN.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## About SpectralSpatialCNN

If you use the SpectralSpatialCNN model in your research, please cite the following paper:

```
@ARTICLE{8897723,
  author={Kwon, O-Yeon and Lee, Min-Ho and Guan, Cuntai and Lee, Seong-Whan},
  journal={IEEE Transactions on Neural Networks and Learning Systems}, 
  title={Subject-Independent Brain–Computer Interfaces Based on Deep Convolutional Neural Networks}, 
  year={2020},
  volume={31},
  number={10},
  pages={3839-3852},
  doi={10.1109/TNNLS.2019.2946869}}
```

---

## Preparation for SpectralSpatialCNN's input

An example of SpectralSpatialCNN's input on the BCIC IV 2a dataset (All settings are set up as optimal settings in the original paper).

### Downloading a particular dataset
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/download_datasets.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python download_datasets.py --dataset 'BCIC2a'
```
---
### Preprocessing based on Spectral Spatial mapping over the considered dataset 
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/prep_spectral_spatial.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
python prep_spectral_spatial.py --dataset 'BCIC2a'
```
---
### Build, fit, and evaluate SpectralSpatialCNN
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_SpectralSpatialCNN.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
# Subject-dependent MI classification
python run_SpectralSpatialCNN.py --model_name 'SpectralSpatialCNN' --dataset 'BCIC2a' --train_type 'subject_dependent' --data_type 'spectral_spatial' --num_class 2  --num_chs 20 --GPU 0

# Subject-independent MI classification
python run_SpectralSpatialCNN.py --model_name 'SpectralSpatialCNN' --dataset 'BCIC2a' --train_type 'subject_independent' --data_type 'spectral_spatial' --num_class 2  --num_chs 20 --GPU 0
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  model_name  | `str` prefix to save model | 'SpectralSpatialCNN' |
|  dataset     | `str` prefix to pick up a particular dataset and save model | 'BCIC2a'|
|  train_type  | `str` prefix to pick up a particular traning manner and save model | 'subject_dependent'|
|  data_type   | `str` prefix to select data type of input | 'spectral_spatial' |
| num_class    | `int` number of classes  | 2  |
| num_chs      | `int` number of classes  | 20 |
| log_dir      | `str` path to save model | 'logs' |
|  subjects    | `int` or `list of int` or `None` list of range test subject, if `None`, use all subjects | `None` |
|  GPU         |  `str` select GPU ID | 0 | -