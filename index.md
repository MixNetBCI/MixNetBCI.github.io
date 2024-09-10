---
layout: default
title: Home
nav_order: 1
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
permalink: /
---

# MixNet
{: .fs-9 }

Joining Force of Classical and Modern Approaches Toward the Comprehensive Pipeline in Motor Imagery EEG Classification

[![Pypi Downloads](https://img.shields.io/pypi/v/mixnet-bci?color=green&logo=pypi&logoColor=white)](https://pypi.org/project/mixnet-bci)
[![DOI](https://img.shields.io/badge/DOI-10.1109%2FJIOT.2024.3402254-blue)](https://ieeexplore.ieee.org/document/10533256)
<!-- [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1IE5J0Yn10ZIhWjSatQn_QWJWZblr6tZy?usp=sharing)
[![Pypi Downloads](https://img.shields.io/pypi/v/min2net?color=green&logo=pypi&logoColor=white)](https://pypi.org/project/min2net)
[![DOI](https://img.shields.io/badge/DOI-10.1109%2FTBME.2021.3137184-blue)](https://ieeexplore.ieee.org/document/9658165) -->

Python API and the novel algorithm for motor imagery EEG classification named MixNet. The API benefits BCI researchers ranging from beginners to experts. We demonstrate examples of using the API for loading six benchmark datasets, preprocessing, training, and validating SOTA models, including MixNet. In summary, the API allows the researchers to construct the pipeline to benchmark the newly proposed and recently developed SOTA models.

- **Website:** [https://mixnetbci.github.io/](https://mixnetbci.github.io/)
- **Documentation:** [https://https://mixnetbci.github.io/](https://mixnetbci.github.io/)
- **Source code:** [https://github.com/Max-Phairot-A/MixNet](https://github.com/Max-Phairot-A/MixNet)
- **Bug reports:** [https://github.com/Max-Phairot-A/MixNet/issues](https://github.com/Max-Phairot-A/MixNet/issues)
  
<!-- <div class="code-example" markdown="1">
Stable
{: .label .label-green }

New release
{: .label .label-green }

DOI: 10.1109%2FTBME.2021.3137184
{: .label .label-blue .text-grey-lt-000}

</div> -->

{: .fs-6 .fw-300 }

<!-- [Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View it on GitHub](https://github.com/IoBT-VISTEC//MIN2Net){: .btn .fs-5 .mb-4 .mb-md-0 } -->

---


## Getting started

### Dependencies

- Python==3.8.10
- tensorflow-gpu==2.7.0
- tensorflow-addons==0.16.1
- scikit-learn>=1.2.2
- wget>=3.2
- h5py==3.5.0
- pandas>=2.0

1. Create `docker container` with dependencies
```bash
docker pull tensorflow/tensorflow:2.7.0-gpu
docker run -ti --name mixnet_container docker.io/tensorflow/tensorflow:2.7.0-gpu bash
wget https://github.com/Max-Phairot-A/MixNet/blob/main/requirement.txt
pip install -r requirements.txt
```

### Installation:

1. Using pip

  ```bash
  pip install mixnet-bci
  ```
2. Using the released python wheel

  ```bash
  wget https://github.com/Max-Phairot-A/MixNet/releases/tag/v1.0.0/mixnet_bci-1.0.0-py3-none-any.whl
  pip install mixnet_bci-1.0.0-py3-none-any.whl
  ```

### Usage 

**Tutorial:** [https://mixnetbci.github.io/](https://mixnetbci.github.io)

<!-- ### Tutorial

[<img src="./assets/images/colab_favicon.ico" width="30" height="30"> Open in Colab](https://colab.research.google.com/drive/1IE5J0Yn10ZIhWjSatQn_QWJWZblr6tZy?usp=sharing){: .btn .fs-5 .mb-4 .mb-md-0 } -->

### Citation

To read & cite our paper, please go to [our preprint](https://arxiv.org/abs/2409.04104v1) and [our paper](https://ieeexplore.ieee.org/document/10533256).

P. Autthasan, R. Chaisaen, H. Phan, M. D. Vos and T. Wilaiprasitporn, "MixNet: Joining Force of Classical and Modern Approaches Toward the Comprehensive Pipeline in Motor Imagery EEG Classification," in IEEE Internet of Things Journal, vol. 11, no. 17, pp. 28539-28554, 1 Sept.1, 2024, doi: 10.1109/JIOT.2024.3402254. 

```
@ARTICLE{10533256,
  author={Autthasan, Phairot and Chaisaen, Rattanaphon and Phan, Huy and Vos, Maarten De and Wilaiprasitporn, Theerawit},
  journal={IEEE Internet of Things Journal}, 
  title={MixNet: Joining Force of Classical and Modern Approaches Toward the Comprehensive Pipeline in Motor Imagery EEG Classification}, 
  year={2024},
  volume={11},
  number={17},
  pages={28539-28554},
  keywords={Electroencephalography;Task analysis;Feature extraction;Measurement;Internet of Things;Multitasking;Motors;Adaptive gradient blending;brain-computer interface (BCI);deep learning (DL);motor imagery (MI);multitask learning},
  doi={10.1109/JIOT.2024.3402254}}
```


### Source Code 

<!-- View our Code on [<img src="./assets/images/github.png" width="20" height="20">](https://github.com/IoBT-VISTEC/MIN2Net) -->

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/Max-Phairot-A/MixNet){: .btn .fs-5 .mb-4 .mb-md-0 } 

### License
Copyright &copy; 2021-All rights reserved by [INTERFACES (BRAIN lab @ IST, VISTEC, Thailand)](https://www.facebook.com/interfaces.brainvistec).
Distributed by an [Apache License 2.0](https://github.com/Max-Phairot-A/MixNet/blob/main/LICENSE).