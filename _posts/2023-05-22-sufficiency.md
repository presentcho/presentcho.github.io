---
title: '[Inference] 01. Sufficiency and Rao-Blackwell'
date: 2023-05-22 17:33:00 +0000
categories: [Inference, Sufficiency]
tags: [sufficiency]
math: true
---

## Sufficiency

**Definition: A statistic $T$ is sufficient for $\theta$ if the conditional distribution $x\|T$ does not involve $\theta$**

What does the definition mean?

The sufficient statistic is a reduction of the data that contains all the evidence of the parameter $\theta$, and $x\|T$ does not depend on $\theta$.

### How to find sufficient statistic? 
#### 1. Factorization Theorem

A statistic $T(X)$ is a sufficienct statistic for $\theta$ if and only if the likelihood can be written as:
$$L(\theta|x) = f(x;\theta) = g(T(x);\theta)h(x)$$


*Example 1: Normal Distribution*

What is the sufficient statistic for unknown parameter $(\mu, \sigma^2)$ when the random variables $X_1, ..., X_n$ i.i.d $N(\mu, \sigma^2)$?

*Solution:*

$L_X(\mu, \sigma^2) = f(x_1,..,x_n; \mu, \sigma^2) \approx (\sigma^2)^{-n/2}exp[-\sum_{i=1}^{n}(x_i -\mu)^{2}/2\sigma^2] = (\sigma^2)^{-n/2}exp(-\frac{\sum_{i=1}^{n}(x_i-\bar{x})^{2} + n(\bar{x}-\mu)^{2}}{2\sigma^2})$

The sample mean and sample variance $(\bar{X}, \sum_{i=1}^{n}(X_i-\bar{X})^{2}/(n-1))$ is the sufficient statistic for $(\mu, \sigma^2)$ 

*Example 2: Uniform distribution*

What is the sufficient statistic for unknown parameter $(\theta_1, \theta_2)$ given observations $(x_1, ... x_n)$ are i.i.d $Unif(\theta_1, \theta_2)$?


*Solution:*

$f(x; \theta_1, \theta_2) = \frac{1}{\theta_2 - \theta_1}I_{\theta_1 \leq x \leq \theta_2}$

$L_X(\theta_1, \theta_2) = \frac{1}{(\theta_2 - \theta_1)^{n}}\prod_{i=1}^{n}I_{\theta_1 \leq x \leq \theta_2} = \frac{1}{(\theta_2 - \theta_1)^{n}}I_{\theta_1 \leq x_{(1)}}I_{\theta_2 \geq x_{(n)}}$ 

$(X_{(1)}, X_{(n)})$ is the sufficient statistic for $(\theta_1, \theta_2)$ where $X_{(1)}$ is $min(X_1, X_2, ..., X_n)$ and $X_{(n)}$ is $max(X_1, X_2, ..., X_n)$


## Rao-Blackwell Theorem 

**Definition: Suppose that $T$ is an estimator of $\theta$, and $S$ is sufficient statistic, then $U = E(T\|S)$ is a better estimator because $E(U-\theta)^{2} \leq E(T-\theta)^{2}$ for all $\theta$**

What does the definition mean? 

By conditioning sufficient statistic will reduce the variance (reduce mean square error (MSE)) without having any effect on bias and improve any estimator. 

*Proof)* 

$E(U - \theta)^{2} = E[E(T\|S)-\theta]^{2} = Var[E(T\|S)] + [E(E(T\|S))-\theta]^{2}$

$E(U - \theta)^{2} \leq Var(T) + [E(T)-\theta]^{2} = E(T - \theta)^{2}$

Note that $[E(E(T\|S)) - \theta]^{2} = [E(T)-\theta]^{2}$

$Var[E(T\|S)] = Var(T) - E[Var(T\|S)] \leq Var(T)Var(T\|S)$










