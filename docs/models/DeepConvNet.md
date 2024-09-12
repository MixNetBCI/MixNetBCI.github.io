---
layout: default
title: DeepConvNet
parent: Models
nav_order: 5
---

# DeepConvNet Usage

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_DeepConvNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## About DeepConvNet

If you use the DeepConvNet model in your research, please cite the following paper:

```
@article{hbm23730,
  author = {Schirrmeister Robin Tibor and 
            Springenberg Jost Tobias and 
            Fiederer Lukas Dominique Josef and 
            Glasstetter Martin and 
            Eggensperger Katharina and 
            Tangermann Michael and 
            Hutter Frank and 
            Burgard Wolfram and 
            Ball Tonio},
  title = {Deep learning with convolutional neural networks for EEG decoding and visualization},
  journal = {Human Brain Mapping},
  volume = {38},
  number = {11},
  pages = {5391-5420},
  keywords = {electroencephalography, EEG analysis, machine learning, end‐to‐end learning, brain–machine interface, brain–computer interface, model interpretability, brain mapping},
  doi = {10.1002/hbm.23730},
  url = {https://onlinelibrary.wiley.com/doi/abs/10.1002/hbm.23730}
}
```

---
## Preparation for DeepConvNet's input

An example of DeepConvNet's input on the BCIC IV 2a dataset (All settings are set up as optimal settings in the original paper).

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
### Build, fit, and evaluate DeepConvNet
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_DeepConvNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
# Subject-dependent MI classification
python run_DeepConvNet.py --model_name 'DeepConvNet' --dataset 'BCIC2a' --train_type 'subject_dependent' --data_type 'time_domain' --num_class 2  --num_chs 20 --GPU 0

# Subject-independent MI classification
python run_DeepConvNet.py --model_name 'DeepConvNet' --dataset 'BCIC2a' --train_type 'subject_independent' --data_type 'time_domain' --num_class 2  --num_chs 20 --GPU 0
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  model_name  | `str` prefix to save model | 'DeepConvNet' |
|  dataset     | `str` prefix to pick up a particular dataset and save model | 'BCIC2a'|
|  train_type  | `str` prefix to pick up a particular traning manner and save model | 'subject_dependent'|
|  data_type   | `str` prefix to select data type of input | 'time_domain' |
| num_class    | `int` number of classes  | 2  |
| num_chs      | `int` number of classes  | 20 |
| log_dir      | `str` path to save model | 'logs' |
|  subjects    | `int` or `list of int` or `None` list of range test subject, if `None`, use all subjects | `None` |
|  GPU         |  `str` select GPU ID | 0 | -