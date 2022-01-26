---
title: "Check if PyTorch is using the GPU"
date: 2021-09-04T22:29:14+05:30
draft: false
---

This is one of the first things we need to check whenever we are setting up a new system.
The easiest way to check this is to use the below commands.

```python
# First let's import pytorch
import pytorch
```

Now let's check if there are multiple devices.
```python
# How many GPUs are there?
print(torch.cuda.device_count())
```

Check which GPU is the current one.
```python
# Which GPU Is The Current GPU?
print(torch.cuda.current_device())
```

What is the name of the current GPU?
```python
# Get the name of the current GPU
print(torch.cuda.get_device_name(torch.cuda.current_device()))
```

Finally check to see if PyTorch is using the GPU.

```python
# Is PyTorch using a GPU?
print(torch.cuda.is_available())
```
