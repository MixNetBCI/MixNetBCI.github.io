---
layout: default
title: Dowload Datasets
parent: Preprocessing
nav_order: 1
---

# mixnet.utils.load_raw

[<img src="https://mixnetbci.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet/blob/main/mixnet/utils.py#L27){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Download raw data

```py
mixnet.utils.load_raw(dataset)
```
Dowload raw dataset from 
1. BCIC2a: [BCI Competition IV 2a dataset- Four class motor imagery (001-2014)](http://bnci-horizon-2020.eu/database/data-sets),
2. BCIC2b: [BCI Competition IV 2b dataset-  Two class motor imagery (004-2014)](http://bnci-horizon-2020.eu/database/data-sets),
3. BNCI2015_001: [BNCI 2015-001 Motor Imagery dataset](https://moabb.neurotechx.com/docs/generated/moabb.datasets.BNCI2015_001.html#moabb.datasets.BNCI2015_001),
4. SMR_BCI: [SMR-BCI dataset- Two class motor imagery (002-2014)](http://bnci-horizon-2020.eu/database/data-sets), 
4. HighGamma: [High-gamma dataset described in Schirrmeister et al. 2017.](https://moabb.neurotechx.com/docs/generated/moabb.datasets.Schirrmeister2017.html#moabb.datasets.Schirrmeister2017), 
3. OpenBMI: [OpenBMI dataset](https://academic.oup.com/gigascience/article/8/5/giz002/5304369).


**Arguments:**

| Arguments | Description |
|:----------|:----------|
|dataset   | `str` Dataset name E.g. 'BCIC2a', 'BCIC2b', 'BNCI2015_001', 'SMR_BCI', 'HighGamma' and 'OpenBMI' |

**Example 1:**
```py
import mixnet

'''
download raw data
'''
mixnet.utils.load_raw('BCIC2a') 
mixnet.utils.load_raw('BCIC2b') 
mixnet.utils.load_raw('BNCI2015_001') 
mixnet.utils.load_raw('SMR_BCI') 
mixnet.utils.load_raw('HighGamma') 
mixnet.utils.load_raw('OpenBMI') 
```

**Example 2:** 
```py
import mixnet
import argparse

'''
download raw data 
1. In case of loading all datasets, please run the script as an example: 
    python download_datasets.py --dataset 'All'
2. In case of loading a particular dataset, please run the script as an example: 
    python download_datasets.py --dataset 'BCIC2a'
'''
parser = argparse.ArgumentParser()
parser.add_argument('--dataset', type=str, default='All', help='dataset name: ex. [BCIC2a/BCIC2b/BNCI2015_001/SMR_BCI/HighGamma/OpenBMI]')
args = parser.parse_args()

if args.dataset == 'All':
    print("============== All datasets are being downloaded ==========")
    mixnet.utils.load_raw('BCIC2a') 
    mixnet.utils.load_raw('BCIC2b') 
    mixnet.utils.load_raw('BNCI2015_001') 
    mixnet.utils.load_raw('SMR_BCI') 
    mixnet.utils.load_raw('HighGamma') 
    mixnet.utils.load_raw('OpenBMI') 
else: 
    print("============== The {} dataset is being downloaded ==========".format(args.dataset))
    mixnet.utils.load_raw(args.dataset)
```