---
layout: default
title: DeepConvNet
parent: Models
nav_order: 2
---

# min2net.model.DeepConvNet

[<img src="https://min2net.github.io/assets/images/github.png" width="30" height="30"> View source on GitHub](https://github.com/IoBT-VISTEC/MIN2Net/blob/main/min2net/model/DeepConvNet.py){: .btn .fs-5 .mb-4 .mb-md-0 } 

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
## DeepConvNet class
Configures the model for training. Based on [tf.keras.Model](https://www.tensorflow.org/api_docs/python/tf/keras/Model).

```py
min2net.model.DeepConvNet()
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
|  model_name  | `str` prefix to save model | 'DeepConvNet' |
|  **kwargs    | Keyword argument to pass into the function for replacing the variables of the model such as `kernLength`, `F1`, `D`, `F2`,  `norm_rate`, `dropout_rate`, `f1_average`, `data_format`, `shuffle`, `metrics`, `monitor`, `mode`, `save_best_only`, `save_weight_only`, `seed`, and `class_balancing`| -

---
## Build method

Build the model that group layers into an object with training and inference features.

```py
DeepConvNet.build()
```
       
        Keras implementation of the Deep Convolutional Network as described in
        Schirrmeister et. al. (2017), Human Brain Mapping.

        This implementation assumes the input is a 2-second EEG signal sampled at
        128Hz, as opposed to signals sampled at 250Hz as described in the original
        paper. We also perform temporal convolutions of length (1, 5) as opposed
        to (1, 10) due to this sampling rate difference.

        Note that we use the max_norm constraint on all convolutional layers, as
        well as the classification layer. We also change the defaults for the
        BatchNormalization layer. We used this based on a personal communication
        with the original authors.

                          ours        original paper
        pool_size        1, 2        1, 3
        strides          1, 2        1, 3
        conv filters     1, 5        1, 10



**Returns:** Model (`tf.keras.Model`): Model object
  
---
## Fit method
Fit the model according to the given training and validation data. This method was implemented based on [tf.keras.Model.fit()](https://www.tensorflow.org/api_docs/python/tf/keras/Model#fit). The model
`weights` and `logs` will save at `'log_path'`.

```py
DeepConvNet.fit(X_train, 
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
DeepConvNet.predict(X_test, 
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
from min2net.model import DeepConvNet
import ndarray as np

model = DeepConvNet(input_shape=(20,400,1), num_class=2, dropout_rate=0.25, shuffle=True)
model.fit(X_train, y_train, X_val, y_val)

Y, evaluation = model.predict(X_test, y_test)
```