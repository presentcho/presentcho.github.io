---
title: '[Algorithm] Time Complexity'
date: 2023-05-28 15:20:00 +0000
categories: [algorithm, timecomplexity]
math: true
---

## Helpful Resources:
Introduction to algorithms, third edition: https://mitpress.mit.edu/9780262533058/

## Time complexity 
To describe the algorithm speed, we use big-$O$ notation and it can be used to compare the speed of two algorithms. 


**Definition of Big $O$ notation**
$f(n)$ is $O(g(n))$ if there exist constants $c > 0$ and $n_0 \geq 0$ such that for all $n \geq n_0$

$$f(n) \leq cg(n)$$, 

where $n$ is the input size, $f(n)$ is the time complexity of an algorithm, and $g(n)$ is a function of $n$

The interpretation of the definition?

We are interested in the complexity with large $n$ and $cg(n)$ is always greater equal than $f(n)$ when $n \geq n_0$

**Example**
Let $f(n) = n +10 $ and we would like to show that the upper bound of $f(n)$ is $O(n)$. Let $c = 2$ and $n_0 = 10$. We can denote $f(n) = n + 10$ and $cg(n) = 2n$. 

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


**Example 2** Fibonacci Sequence
The Fibonacci sequence is the series of the numbers: 0, 1, 1, 2, 3, 5, 8, 13, 21, ...

Let $S_0=0$ and $S_1 = 1$
$S_2 = S_1 + S_0 = 1 + 0 = 1$
$S_3 = S_2 + S_1 = 1 + 1 = 2$
...


Pseudo Code
>Initialize values $S_0 = 0$ and $S_1 = 1$
>> for i in range(2, n+1): # n is the number of array
>>> $S_n$ = $S_{n-1}$ + $S_{n-2}$
>>>> return $S_n$

```
def fibonacci(n):
	if n <= 1:
		return n
	S = [0, 1]
	for i in range(2, n+1):
		Sn = S[i-1] + S[i-2]
		S.append(Sn)
	return S
```

```
def fibonacci(n):
	if n <= 1:
		return n
	a, b = 0, 1
	for i in range(2, n+1):
		c = a + b
		a = b
		b = c
	return c
```

**Example 3** Find the largest number in the array using the loop 

arr = [2, 3, 5, -4, 9, 10, 20, 11]

```
def find_large(arr):
	# set the initial value
    max_ = arr[0]
    for i in range(len(arr)):
	    # compare the values in the array and update the max_
        if arr[i] > max_:
            max_ = arr[i]
    return max_
```

**Example 4** Find the largest sum across all the contiguous subarrays of the input array using the complexity $O(n)$

Pseudo code
> Initialize the sum of the array as **sum_** 
>> **if** the value in the array (**arr**) is positive, update  **sum_[i]** by adding **sum_[i-1]**  and **arr[i]**
>> **else** replace **sum_[i]** with **arr[i]**
```
arr = [2, 3, 5, -4, 9, 10, 20, 11]
def large_sum(arr):
	sum_ = [0] * len(arr)
	for i in range(1, len(arr)):
		if sum_[i-1] > 0:
			sum_[i] = sum_[i-1] + arr[i]
		else:
			sum_[i] = arr[i]
	return max(sum_)
```

**Example 5** Find whether parentheses in the input string are valid.

For example, 
s_1 = "()" -> return **True**
s_2 = "(" -> return **False**
s_3 = ")" -> return **False**
s_4 = ")(" -> return **False**
s_5 = "()()" -> return **True**
s_6 = "))((" -> return **False**

Pseudo code
> for i in range(len(arr)-1):
>> if arr[i] == '(' and arr[i+1] == ')'
>>> return True
>
>> else:
> >>return False

```
if len(arr) == 1:	
	return False
for i in range(len(arr)-1):
	if arr[i] == '(' and arr[i+1] == ')':
		return True
	else:
		return False
```

**Example 5-1** Find whether parentheses in the input string are valid using append and pop 

```
def example5(a):
	 a = []
	for i in a:
		 if i == ')':
			if (len(a) == 0) or ('(' != stack.pop()):
				return False
			else:
				a.append(i)
		return True if len(a) == 0 else False
```

**Example 5-2** Find whether parentheses in the input string are valid by counting '(' as 1 and ')' as -1. Thus, if the sum of the count is 0, it returns true.

```
def example5_1(a):
	count = 0
	for i in a:
		if i == '(':
			count += 1
		else:
			count -= 1
	return True if count = 0 else False
```

**Advanced** Let's say we would like to find () {} []. 



