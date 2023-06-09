---
title: '[Algorithm] Big O and Small O calculation'
date: 2023-06-09 10:20:00 +0000
categories: [algorithm, timecomplexity]
math: true
---

## Big $O_p$

The notation $X_n = O_p(a_n)$ means that the set of values $X_n/a_n$ is stochastically bounded. For any $\varepsilon > 0$, there exists a finite $M >0$ such that $$P[\|X_n / a_n\| \geq M] < \varepsilon, \forall n$$


## Little $o_p$

The notation $X_n = o_p(a_n)$ means that the set of values $X_n/a_n$ converges to zero in probability as $n$ approaches an appropriate limit. $X_n = o_p(a_n)$ can be written as $X_n/a_n = o_p(1), where $X_n = o_p(1)$ can be denoted as $$lim_{n \rightarrow \infty} P[\|X_n\| \geq \varepsilon] = 0$$

## Calculations

- $o_p(1) + o_p(1) = o_p(1)$
- $o_p(1) + O_p(1) = O_p(1)$
- $O_p(1) o_p(1) = o_p(1)$
- $\frac{1}{(1 + o_p(1))}= O_p(1)$
- $o_p(R_n) = R_no_p(1)$
- $O_p(R_n) = R_nO_p(1)$
- $o_p(O_p(1)) = o_p(1)$
