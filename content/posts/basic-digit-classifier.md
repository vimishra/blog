+++
title = "Basic Digit Classifier (for 2s and 9s) without tunable parameters"
date = "2021-09-26"
author = "Vikas Mishra"
categories = ["Deep Learning", "Fast.ai"]
tags = ["fastai", "deeplearning", "mnist"]
+++


## Motivation and approach

In this case we are trying to build a very basic Digit Classifier. This is strictly speaking not a Deep Learning or a Machine Learning classifier since there are no tunable parameters here. But the intent behind this approach is to understand the basics of how to do digit classification. The intent here is not to do something super hard or tricky but to understand the basics of how to use Fast.ai for doing something like this.

The approach we will be following will be something like this. 

1. Import the MNIST dataset.
2. Build the stacked tensor of 2s and 9s - both the training data as well as validation data.
3. Identify an idealized 2 and an idealized 9.
4. Figure out for each data element in the validation set, if it is closer to a 2 or closer to a 9 and based on that classify it. 
5. Publish the accuracy.

Let's start by importing the libraries we need for the exercise.


```python
from fastai.vision.all import *
from fastbook import *
```


```python

```
