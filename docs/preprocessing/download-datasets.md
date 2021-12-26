---
layout: default
title: Dowload Datasets
parent: Preprocessing
nav_order: 1
---

# min2net.utils.load_raw

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/utils.py#L17){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Download raw data

```py
min2net.utils.load_raw(dataset_name)
```
Dowload raw dataset from 
1.  SMR_BCI: [SMR-BCI dataset- Two class motor imagery (002-2014)](http://bnci-horizon-2020.eu/database/data-sets), 
2. BCIC2a: [BCI Competition IV 2a dataset- Four class motor imagery (001-2014)](http://bnci-horizon-2020.eu/database/data-sets),
3. OpenBMI: [OpenBMI dataset](https://academic.oup.com/gigascience/article/8/5/giz002/5304369).


**Arguments:**

| Arguments | Description |
|:----------|:----------|
|dataset_name   | `str` Dataset name E.g. 'SMR_BCI', 'BCIC2a' and 'OpenBMI' |

**Example**
```py
import min2net

'''
download raw data
'''
min2net.utils.load_raw('SMR_BCI')
min2net.utils.load_raw('BCIC2a')
min2net.utils.load_raw('OpenBMI')

```