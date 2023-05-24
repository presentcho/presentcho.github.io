---
title: '[Inference] 01. Sufficiency'
date: 2023-05-22 17:33:00 +0000
categories: [Inference, Sufficiency]
tags: [sufficiency]
---

# Sufficiency

A statistic $T$ is sufficient for $\theta$ if the conditional distribution $x|T$ does not involve $\theta$


## How to find sufficient statistic? 
### 1. Factorization Theorem

A statistic $T(X)$ is a sufficienct statistic for $theta$ if and only if the likelihood can be written as:
$$L(\theta|x) = f(x;\theta) = g(T(x);\theta)h(x)$$
