---
layout: default
title: EEGNet
parent: Models
nav_order: 2
---

# min2net.model.EEGNet

[<img src="./assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/model/EEGNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## About EEGNet
Original authors have uploaded their code here https://github.com/vlawhern/arl-eegmodels

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
## EEGNet class

Configures the model for training. Based on [tf.keras.Model](https://www.tensorflow.org/api_docs/python/tf/keras/Model).

```py
min2net.model.EEGNet()
```


**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|input_shape   | `tuple` of integers. <br/> (1, *#channel*, *#time_point*) | (20,400,1)  |
| num_class    | `int` number of class.  | 2  |
| loss         | `str` (name of objective function), objective function or [tf.keras.losses.Loss](https://www.tensorflow.org/api_docs/python/tf/keras/losses) instance.  |  `'sparse_categorical_crossentropy'` |
|  epochs      | `int` number of epochs to train the model.  |  200 |
|  batch_size  | `int` or `None`. Number of samples per gradient update. | 100 |
| optimizer    | `str` (name of optimizer) or `optimizer instance`. See [tf.keras.optimizers](https://www.tensorflow.org/api_docs/python/tf/keras/optimizers).  | Adam(beta_1=0.9, beta_2=0.999, epsilon=1e-08) |
|  lr          | `float` the start learning rate | 0.01
|  min_lr      | `float` lower bound on the learning rate. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). | 0.01  |
|  factor      | `float` factor by which the learning rate will be reduced. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). |  0.25 |
|  patience    | `int` number of epochs with no improvement after which learning rate will be reduced. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). | 10 |
|  es_patience | `int` number of epochs with no improvement after which training will be stopped. See [tf.keras.callbacks.EarlyStopping](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/EarlyStopping). |  20 |
|  verbose     | `0` or `1`. Verbosity mode. 0 = silent, 1 = progress bar.  | 1 |
|  log_path    | `str` path to save model | 'logs' |
|  model_name  | `str` prefix to save model | 'EEGNet' |
|  **kwargs    | Keyword argument to pass into the function for replacing the variables of the model such as `kernLength`, `F1`, `D`, `F2`,  `norm_rate`, `dropout_rate`, `f1_average`, `data_format`, `shuffle`, `metrics`, `monitor`, `mode`, `save_best_only`, `save_weight_only`, `seed`, and `class_balancing`| -

---
## Build method

Build the model that group layers into an object with training and inference features.

```py
EEGNet.build()
```

**Returns:** Model (`tf.keras.Model`): Model object
  
---
## Fit method
Fit the model according to the given training and validation data. This method was implemented based on [tf.keras.Model.fit()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#fit). The model
`weights` and `logs` will save at `'log_path'`.

```py
EEGNet.fit(X_train, 
           y_train, 
           X_val, 
           y_val)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|X_train   | `ndarray` Training EEG signals. shape (*#trial*, *#channel*, *#time_point*, *#depth*) | 
|y_train   | `ndarray` Label of training set. shape (*#trial*) |
|X_val   | `ndarray` Validation EEG signals. shape (*#trial*, *#channel*, *#time_point*, *#depth*) |
|y_val   | `ndarray` Label of validation set. shape (*#trial*) |
  
---
## Predict method

Generates output predictions & the loss value & metrics values for the model in test mode for the input samples. This medthod was implemented based on [tf.keras.Model.predict()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#predict) and [tf.keras.Model.evaluate()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#evaluate).

```py
EEGNet.predict(X_test, 
               y_test)
```

| Arguments | Description |
|:---|:----|
|X_test   | `ndarray` Testing EEG signals. shape (*#trial*, *#channel*, *#time_point*, *#depth*) | 
|y_test   | `ndarray` Label of test set. shape (*#trial*) |

**Returns:**
  >- Y: dictionary of `{y_true, y_pred}`
  >- evaluation: dictionary of `{loss, accuracy, f1_score}`

---
## Example

```py
from min2net.model import EEGNet
import ndarray as np

model = EEGNet(input_shape=(20,400,1), num_class=2, dropout_rate=0.25, shuffle=True)
model.fit(X_train, y_train, X_val, y_val)

Y, evaluation = model.predict(X_test, y_test)
```