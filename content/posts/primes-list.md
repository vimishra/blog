---
categories: ["maths", "algorithms"]
date: "2021-07-16T08:36:25+05:30"
draft: false
tags: ["maths", "python", "algorithms"]
title: "Primes List"
math: true

---

## Extract all the prime number from a composite number with python

This is a quick article to show you how to create an algorithm to extract all the prime numbers from a composite number in Python.

### Algorithm
``` python
def primes_list(N):
    """
    Extract all the prime numbers
    from a composite number

    Keyword arguments:
    N -- an integer
    Return: a list of prime numbers
    """
    for i in range(N-1, 0, -1):
        if i == 1:
            return [N]
        elif N % i == 0:
            return [int(N/i)] + primes_list(int(i))
```

### Usage
``` python
print(primes_lists(12))
> [2,2,3]
```

### Fundamental property of Primes

Composite numbers can be arranged into rectangles but prime numbers cannot

![Primes vs Composites](/primes-vs-composites.png)

In hindsight this is obvious.

### Mathematics

Here's sum inline math: $ \sum_{n=1}^{\infty} 2^{-n} = 1 $

Display mode math looks like
$$
\int \frac{1}{x} dx = \ln |x|
$$
