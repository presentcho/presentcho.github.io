---
title: '[Survival Analysis] Intro and Survival Functions'
date: 2023-11-08 14:33:00 +0000
categories: [Survival Analysis, Survival Function]
math: true
---

## Survival Analysis 

### Introduction
 Assumptions: the essential assumption is independent censoring. Note that multivariate/clustered survival data usually violate independence assumption

**Survival Function**
$$S(x) = P(X > x)  = 1 - F(x)$$
where $F$ is the cumulative distribution function of $X$.

*Properties*
1. Non-increasing: For $0 \leq x \leq x'$, $S(x) \geq S(x')$. 
2. $S(0) = 1$
3. $\lim_{x \rightarrow \infty}S(x) = 0$

**Hazard Function**
$$h(x) = \lim_{\delta \rightarrow 0}\frac{P(x \leq X \leq x + \delta | X \geq x)}{\delta} = \lim_{\delta \rightarrow 0}\frac{P(x \leq X \leq x + \delta)}{\delta P(X \leq x)} = \frac{f(x)}{S(x)}$$

- $h(x)$ is the intantaneous death rate at time $x$
- $h(x)\delta$ approixmate probability of dying in the next $\delta$ units of time given survival to time $x$
- $h(x) = \frac{f(x)}{S(x)} = -\frac{dlog[S(x)]}{dx}$

**Cumulative Hazard Function**

$$H(x) = \int_{0}^{x} h(u) du$$

- $H(x) = -log[S(x)]$
- $S(x) = exp\{-H(x)\} = exp \{ - \int_{0}^{x}h(u) du\}$

*Properties*
1. $H(x) \geq 0$
2. $\lim_{x \rightarrow \infty} H(x) = \infty$
3. $H(0) = 0$

## Summary
**Summary of Functions**

Survival function and hazard function have relationships

- $F(x) = 1 - S(x)$ 
- $S(x) = \frac{f(x)}{h(x)} = \exp\{-H(x)\}$
- $h(x) = \frac{f(x)}{S(x)} = \frac{dF(x)/dx}{S(x)}$
- $H(x) = -log\{S(x)\}$
- $f(x) = -\frac{dS(x)}{dx} = S(x)h(x)$

## Distributions 
**Exponential Distribution**
$$f(x) = \lambda e^{-\lambda x}$$

- $x \geq 0$; parameter: $\lambda > 0$.
- Survival function $S(x) = e^{\lambda x}$ and hazard function $h(x)=  \lambda$
- Exponential distribution is often used to plan clinical trials with survival endpoints
- Since the survival distribution can only be approximated before the study, the analytical tractability of the exponential distribution allows us to find :
	- the expected number of deaths
	- power for hypothesis teting

**Weibull Distirubtion**
$$f(x) = \alpha \lambda x^{\alpha-1}e^{-\lambda x^{\alpha}}$$

- $x \geq 0$; parameter: $\lambda >0)$ (scale), $\alpha > 0$ (shape)
- Survival function $S(x) = e^{-\lambda x^{\alpha}}$ and hazard function $h(x) = \lambda \alpha x^{\alpha -1}$
- Weibull distribution is ore flexible than the constant hazard of the exponential function

*Features*
- A generalization of the exponential distribution $\alpha = 1$
- monotone decreasing hazards $(\alpha <1)$
- monotone increasing hazards $(\alpha >1)$
- constant hazard $(\alpha = 1)$

**Log-logistic Distribution**
$$f(x) = \frac{\alpha x^{\alpha-1} \lambda}{(1 + \lambda x^{\alpha})^2}$$
- $x \geq 0$; parameter: $\lambda >0)$, $\alpha > 0$
- Survival function $S(x) = \frac{1}{1 + \lambda x^\alpha}$ and hazard function is $h(x) = \frac{\lambda \alpha x^{\alpha-1}}{1 + \lambda x^\alpha}$, where numerator of hazard function is the same as Weibull
- If $\alpha \leq 1$, $h(x)$ i monotone decreasing
- If $\alpha >1$, $h(x)$ increases to a maximum then decrease to 0 as $x \rightarrow \infty$
