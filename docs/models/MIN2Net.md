---
layout: default
title: MIN2Net
parent: Models
nav_order: 2
---

# MIN2Net Usage

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_MIN2Net.py){: .btn .fs-5 .mb-4 .mb-md-0 } 


{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## About MIN2Net
Original authors have uploaded their code here [https://github.com/IoBT-VISTEC/MIN2Net](https://github.com/IoBT-VISTEC/MIN2Net)

If you use the MIN2Net model in your research, please cite the following paper:

```
@ARTICLE{9658165,
  author={Autthasan, Phairot and Chaisaen, Rattanaphon and Sudhawiyangkul, Thapanun and Rangpong, Phurin and Kiatthaveephong, Suktipol and Dilokthanakul, Nat and Bhakdisongkhram, Gun and Phan, Huy and Guan, Cuntai and Wilaiprasitporn, Theerawit},
  journal={IEEE Transactions on Biomedical Engineering}, 
  title={MIN2Net: End-to-End Multi-Task Learning for Subject-Independent Motor Imagery EEG Classification}, 
  year={2022},
  volume={69},
  number={6},
  pages={2105-2118},
  doi={10.1109/TBME.2021.3137184}}
```
---

## Preparation for MIN2Net's input

An example of MIN2Net's input on the BCIC IV 2a dataset (All settings are set up as optimal settings in the original paper).

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
### Build, fit, and evaluate MIN2Net
[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/experiments/run_MIN2Net.py){: .btn .fs-5 .mb-4 .mb-md-0 } 
```py
# Subject-dependent MI classification
python run_MIN2Net.py --model_name 'MIN2Net_original' --dataset 'BCIC2a' --train_type 'subject_dependent' --data_type 'time_domain' --log_dir 'logs' --num_class 2  --num_chs 20 --GPU 0 --loss_weights 1.0 0.1 1.0 --margin 100.0

# Subject-independent MI classification
python run_MIN2Net.py --model_name 'MIN2Net_original' --dataset 'BCIC2a' --train_type 'subject_independent' --data_type 'time_domain' --log_dir 'logs' --num_class 2  --num_chs 20 --GPU 0 --loss_weights 0.5 0.1 1.0 --margin 1.0
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|  model_name  | `str` prefix to save model | 'MIN2Net_original' |
|  dataset     | `str` prefix to pick up a particular dataset and save model | 'BCIC2a'|
|  train_type  | `str` prefix to pick up a particular traning manner and save model | 'subject_dependent'|
|  data_type   | `str` prefix to select data type of input | 'time_domain' |
| num_class    | `int` number of classes  | 2  |
| num_chs      | `int` number of classes  | 20 |
| latent_dim   |`int` or `None`. If `None`, latent_dim is equal to number of channels `C` or 64 for 2- or 3-class classification, respectively. |`None`|
| log_dir      | `str` path to save model | 'logs' |
|  subjects    | `int` or `list of int` or `None` list of range test subject, if `None`, use all subjects | `None` |
|  margin      | `float` margin (alpha) of Triplet loss| 1.0 |
|  GPU         |  `str` select GPU ID | 0 | -