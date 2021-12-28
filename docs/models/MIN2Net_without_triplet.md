---
layout: default
title: MIN2Net without triplet
parent: Models
nav_order: 7
---

# min2net.model.MIN2Net_without_triplet

[<img src="https://min2net.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/min2net/model/MIN2Net_without_triplet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 


{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
## MIN2Net_without_triplet class

Configures the model for training. Based on [tf.keras.Model](https://www.tensorflow.org/api_docs/python/tf/keras/Model).

```py
min2net.model.MIN2Net_without_triplet()
```

**Arguments:**

| Arguments | Description | Default |
|:---|:----|:---|
|input_shape   | `tuple` of integers. <br/> (1, *#time_point*, *#channel*) | (1,400,20)  |
| num_class    | `int` number of class.  | 2  |
| loss         | `list` of `str` (name of objective function), objective function or [tf.keras.losses.Loss](https://www.tensorflow.org/api_docs/python/tf/keras/losses) instance.  | [[`mean_squared_error`](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/min2net/loss.py#L6), <br/> `'sparse_categorical_crossentropy'`]  |
| loss_weights | `list` of `float` [β1,β2] to weight the loss contributions of different model outputs. | [1., 1.] |
|latent_dim|`int` or `None`. If `None`, latent_dim is equal to number of channels `C` or 64 for 2- or 3-class classification, respectively.|`None`|
|  epochs      | `int` number of epochs to train the model.  |  200 |
|  batch_size  | `int` or `None`. Number of samples per gradient update. | 100 |
| optimizer    | `str` (name of optimizer) or `optimizer instance`. See [tf.keras.optimizers](https://www.tensorflow.org/api_docs/python/tf/keras/optimizers).  | Adam(beta_1=0.9, beta_2=0.999, epsilon=1e-08) |
|  lr          | `float` the start learning rate | 1e-2
|  min_lr      | `float` lower bound on the learning rate. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). | 1e-3  |
|  factor      | `float` factor by which the learning rate will be reduced. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). |  0.25 |
|  patience    | `int` number of epochs with no improvement after which learning rate will be reduced. See [tf.keras.callbacks.ReduceLROnPlateau](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/ReduceLROnPlateau). | 20 |
|  es_patience | `int` number of epochs with no improvement after which training will be stopped. See [tf.keras.callbacks.EarlyStopping](https://www.tensorflow.org/api_docs/python/tf/keras/callbacks/EarlyStopping). |  50 |
|  verbose     | `0` or `1`. Verbosity mode. 0 = silent, 1 = progress bar.  | 1 |
|  log_path    | `str` path to save model | 'logs' |
|  model_name  | `str` prefix to save model | 'MIN2Net_without_triplet' |
|  **kwargs    | Keyword argument to pass into the function for replacing the variables of the model such as `data_format`, `shuffle`, `metrics`, `monitor`, `mode`, `save_best_only`, `save_weight_only`, `seed`, and `class_balancing`| -

---
## Build method
Build the model that group layers into an object with training and inference features.
```py
MIN2Net_without_triplet.build()
```

**Returns:** Model (`tf.keras.Model`): Model object

---
## Fit method
Fit the model according to the given training and validation data. This method was implemented based on [tf.keras.Model.fit()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#fit). The model
`weights` and `logs` will save at `'log_path'`.

```py
MIN2Net_without_triplet.fit(X_train, 
                            y_train, 
                            X_val, 
                            y_val)
```

**Arguments:**

| Arguments | Description |
|:---|:----|
|X_train   | `ndarray` Training EEG signals. shape (*#trial*, *#depth*, *#time_point*, *#channel*) | 
|y_train   | `ndarray` Label of training set. shape (*#trial*) |
|X_val   | `ndarray` Validation EEG signals. shape (*#trial*, *#depth*, *#time_point*, *#channel*) |
|y_val   | `ndarray` Label of validation set. shape (*#trial*) |

---
## Predict method
Generates output predictions & the loss value & metrics values for the model in test mode for the input samples. This method was implemented based on [tf.keras.Model.predict()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#predict) and [tf.keras.Model.evaluate()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#evaluate).

```py
MIN2Net_without_triplet.predict(X_test, 
                                y_test)
```

| Arguments | Description |
|:---|:----|
|X_test   | `ndarray` Testing EEG signals. shape (*#trial*, *#depth*, *#time_point*, *#channel*) | 
|y_test   | `ndarray` Label of test set. shape (*#trial*) |

**Returns:**
  >- Y: dictionary of `{y_true, y_pred, y_pred_decoder}`
  >- evaluation: dictionary of `{loss, decoder_loss, classifier_loss, accuracy, f1_score}`

---
## Example

```py
from min2net.model import MIN2Net_without_triplet
import numpy as np

model = MIN2Net_without_triplet(input_shape=(1, 400, 20), num_class=2, monitor='val_loss', shuffle=True)
model.fit(X_train, y_train, X_val, y_val)

Y, evaluation = model.predict(X_test, y_test)
```