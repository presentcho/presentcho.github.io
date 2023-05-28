---
title: '[Algorithm] Time Complexity'
date: 2023-05-28 15:20:00 +0000
categories: [algorithm, timecomplexity]
math: true
---

## Helpful Resources:
Introducton to algorithms, third edition: https://mitpress.mit.edu/9780262533058/

## Time complexity 
To describe the algorithm speed, we use big-$O$ notation and it can be used to compare the spped of two algorithms. 


**Definition of Big $O$ notation**
$f(n)$ is $O(g(n))$ if there exist constants $c > 0$ and $n_0 \geq 0$ such that for all $n \geq n_0$

$$f(n) \leq cg(n)$$, 

where $n$ is the input size, $f(n)$ is the time complexity of an algorithm, and $g(n)$ is a function of $n$

The interpretation of definition?

We are interested in the compexlexity with large $n$ and $cg(n)$ is always greater equal than $f(n)$ when $n \geq n_0$

**Example**
Let $f(n) = n +10 $ and we would like to show that upper bound of $f(n)$ is $O(n)$. Let $c = 2$ and $n_0 = 10$. We can denote $f(n) = n + 10$ and $cg(n) = 2n$. 

By the definition, we satisfy $n + 10 \leq 2n$ when $n \geq 10$. 

Thus, we can conclude that $O(n)$ is an upper bound of $f(n)$ and $f(n) = O(n)$

common families of complexity (ascending order of the complexity)
- constant: $O(1)$
- logarithmic: $O(\log n)$
- linear: $O(n)$
- log linear: $O(n \log n)$
- polynomial: $O(n^c)$
- exponential: $O(c^n)$ - unscalable algorithm 
- factorial: $O(n!)$ - unscalable algorithm 

$n$ is the number of sample size in the output. 


Constant time complexity $O(1)$
```
def constant(n):
	print(n)
```

Linear time complexity $O(n)$
```
def linear(n):
	for x in range(n+1):
		print(x)
```

Polynomial time complexity $O(n^2)$
```
def polynomial(n):
	for x in range(n+1):
		for y in range(x+1):
			print(y)
```

**Example bubble sort $O(n^2)$**

Bubble sort is a simple sorting algorithm that works by repeatedly swapping adjacent elements if they are in the wrong order. It gets its name because during each pass, the largest (or smallest, depending on the sorting order) element "bubbles" up to its correct position.

Let's say we have an array 1 9 4 6 11 10 3 15 2 13
```
x = [1, 9, 4, 6, 11, 10, 3, 15, 2, 3]
def bubble_sort(arr):
    # Traverse through all array elements
    for i in range(len(arr)):
        # Last i elements are already in place
        for j in range(len(arr) - 1 - i):
            print(j)
            # Swap if the element found is greater than the next element
            if arr[j] > arr[j + 1]:
                    arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
print(bubble_sort(x))
```

