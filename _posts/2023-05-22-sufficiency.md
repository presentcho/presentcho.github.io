---
title: '[Inference] 01. Sufficiency'
date: 2023-05-22 17:33:00 +0000
categories: [Inference, Sufficiency]
tags: [sufficiency]
math: true
---

## Sufficiency

A statistic $T$ is sufficient for $\theta$ if the conditional distribution $x\|T$ does not involve $\theta$

### How to find sufficient statistic? 
#### 1. Factorization Theorem

A statistic $T(X)$ is a sufficienct statistic for $\theta$ if and only if the likelihood can be written as:
$$L(\theta|x) = f(x;\theta) = g(T(x);\theta)h(x)$$


**Example 1: Normal Distribution**

What is the sufficient statistic for unknown parameter $(\mu, \sigma^2)$ when the random variables $X_1, ..., X_n$ i.i.d $N(\mu, \sigma^2)$?

$L_X(\mu, \sigma^2) = f(x_1,..,x_n; \mu, \sigma^2) \approx (\sigma^2)^{-n/2}exp[-\sum_{i=1}^{n}(x_i -\mu)^{2}/2\sigma^2]$

$(\sigma^2)^{-n/2}exp(-\frac{\sum_{i=1}^{n}(x_i-\bar{x})^{2} + n(\bar{x}-\mu)^{2}}{2\sigma^2})$

The sample mean and sample variance $(\bar{X}, \sum_{i=1}^{n}(X_i-\bar{X})^{2}/(n-1))$ is the sufficient statistic for $(\mu, \sigma^2)$ 
