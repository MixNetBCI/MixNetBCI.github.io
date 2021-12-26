---
layout: default
title: SpectralSpatialCNN
parent: Models
nav_order: 2
---

# min2net.model.SpectralSpatialCNN

[<img src="https://min2net.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/min2net/model/SpectralSpatialCNN.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

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
## SpectralSpatialCNN class
Configures the model for training. Based on [tf.keras.Model](https://www.tensorflow.org/api_docs/python/tf/keras/Model).

```py
min2net.model.SpectralSpatialCNN()
```


**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|input_shape   | `tuple` of integers. <br/> (1, *#time_point*, *#channel*) | (28,28,1)  |
| num_class    | `int` number of class.  | 2  |
| loss         | `str` (name of objective function), objective function or [tf.keras.losses.Loss](https://www.tensorflow.org/api_docs/python/tf/keras/losses) instance.  |  `'sparse_categorical_crossentropy'` |
|  epochs      | `int` number of epochs to train the model.  |  200 |
|  batch_size  | `int` or `None`. Number of samples per gradient update. | 100 |
| optimizer    | `str` (name of optimizer) or `optimizer instance`. See [tf.keras.optimizers](https://www.tensorflow.org/api_docs/python/tf/keras/optimizers).  | Adam(beta_1=0.9, beta_2=0.999, epsilon=1e-08) |
|  lr          | `float` the start learning rate | 1e-5
|  min_lr      | `float` lower bound on the learning rate. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). | 1e-6 |
|  factor      | `float` factor by which the learning rate will be reduced. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). |  0.25 |
|  patience    | `int` number of epochs with no improvement after which learning rate will be reduced. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). | 10 |
|  es_patience | `int` number of epochs with no improvement after which training will be stopped. See [tf.keras.callbacks.EarlyStopping](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/EarlyStopping). |  20 |
|  verbose     | `0` or `1`. Verbosity mode. 0 = silent, 1 = progress bar.  | 1 |
|  log_path    | `str` path to save model | 'logs' |
|  model_name  | `str` prefix to save model | 'SpectralSpatialCNN' |
|  **kwargs    | Keyword argument to pass into the function for replacing the variables of the model such as `n_subbands`, `dropout_rate`, `f1_average`, `data_format`, `shuffle`, `metrics`, `monitor`, `mode`, `save_best_only`, `save_weight_only`, `seed`, and `class_balancing` | -

---
## Build method

Build the model that group layers into an object with training and inference features.

```py
SpectralSpatialCNN.build()
```

**Returns:** Model (`tf.keras.Model`): Model object
  
---
## Fit method
Fit the model according to the given training and validation data. This method was implemented based on [tf.keras.Model.fit()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#fit). The model
`weights` and `logs` will save at `'log_path'`.

```py
SpectralSpatialCNN.fit(X_train, 
                       y_train, 
                       X_val, 
                       y_val)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|X_train   | `ndarray` Training EEG signals. shape (*#trial*, #n_subbands, *#height*, *#width*, *#depth*) |
|y_train   | `ndarray` Label of training set. shape (*#trial*) |
|X_val   | `ndarray` Validation EEG signals. shape (*#trial*, #n_subbands, *#height*, *#width*, *#depth*) |
|y_val   | `ndarray` Label of validation set. shape (*#trial*) |
  
---
## Predict method

Generates output predictions & the loss value & metrics values for the model in test mode for the input samples. This medthod was implemented based on [tf.keras.Model.predict()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#predict) and [tf.keras.Model.evaluate()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#evaluate).

```py
SpectralSpatialCNN.predict(X_test, 
               y_test)
```

| Arguments | Description |
|:---|:----|
|X_test   | `ndarray` Testing EEG signals. shape (*#trial*, #n_subbands, *#height*, *#width*, *#depth*) |
|y_test   | `ndarray` Label of test set. shape (*#trial*) |

**Returns:**
  >- Y: dictionary of `{y_true, y_pred}`
  >- evaluation: dictionary of `{loss, accuracy, f1_score}`

---
## Example

```py
from min2net.model import SpectralSpatialCNN
import numpy as np

model = SpectralSpatialCNN(input_shape=(28, 28, 1), num_class=2, dropout_rate=0.25, shuffle=True)
model.fit(X_train, y_train, X_val, y_val)

Y, evaluation = model.predict(X_test, y_test)
```