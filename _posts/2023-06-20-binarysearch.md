---
title: '[Algorithm] Binary Search'
date: 2023-06-21 15:20:00 +0000
categories: [algorithm, BinarySearch]
math: true
---

# Warm-up Questions $O(n)$ complexity
## How to count the number of array matching with the target?
```
def ex1(arr, target):
	count = 0
	for i in range(len(arr)):
		arr[i] == target
		count += 1
	return count 
Result:
print(ex2([2,7,9,3,5], 5))
1
```

## How to find the index of array that matches with the target? 
```
def ex2(arr, target):
	idx = None
	for i in range(len(arr)):
		arr[i] == target
		idx = i
	return idx


Result:
print(ex2([2,7,9,3,5], 5))
4
```

**Another approach (Simpler method)** 
```
def ex3(arr, target):
	for i in range(len(arr)):
		arr[i] == target
		return i


Result:
print(ex2([2,7,9,3,5], 5))
4
```

## How to find the target is a square value?
```
def fun_37(target):
    for i in range(1, target+1):
        if i == target / i:
            return True
    return False
```


# Binary Search

Binary search is an efficient algorithm used to search for a specific element in a sorted list or array. It follows a divide-and-conquer strategy by repeatedly dividing the search space in half until the desired element is found or it determines that the element does not exist in the list.

## Binary Search Algorithm 
1. Start with a sorted list or array of elements.

2. Set two pointers, one at the beginning (left) and one at the end (right) of the search space.

3. Calculate the middle element by taking the average of the left and right pointers.

4. Compare the middle element with the desired element.
- If they are equal, the element is found at the middle index, and the search is complete.
- If the middle element is greater than the desired element, discard the right half of the search space by moving the right pointer to the middle - 1.
- If the middle element is less than the desired element, discard the left half of the search space by moving the left pointer to the middle + 1.

5. Repeat steps 3 and 4 until the desired element is found or the search space is empty (left pointer exceeds right pointer).


```
def binary_search(arr, target):
	# define the index of left and right 
    left, right = 0, len(arr)-1
    # while the subarray is empty 
    while (left <= right): 
    	# find the middle point 
        mid = (left + right) // 2
        # condition for target serach
        if arr[mid] == target:
            return mid
        elif arr[mid] > target:
            right = mid - 1
        else:
            left = mid + 1

 Result
print(binary_serach([2,3,6,8,9], 3))
1
```

Note that the complexity of binary serach is $O(log(n))$


## When the target is not in the input array and return the index where the target should be inserted
```
def binary_search2(arr, target):
	# define the index of left and right 
    left, right = 0, len(arr)-1
    # while the subarray is empty 
    while (left <= right): 
    	# find the middle point 
        mid = (left + right) // 2
        # condition for target serach
        if arr[mid] == target:
            return mid
        elif arr[mid] > target:
            right = mid - 1
        else:
            left = mid + 1
    return left
Result
print(binary_serach2([2,3,6,8,9], 1))
0
```

## How to find the target is a square value with binary search?
```
def square_binary_serach(arr, target):
    left, right = 1, target
    while left <= right:
        mid = (right + left) // 2
        div = target / mid
        if mid == div:
            return True
        elif mid > div:
            right = mid - 1
        else: 
            left = mid + 1
    return False
```

## Find the number of negative values in the matrix 
**Time complexity $O(n log_2 m)$ and space complexity $O(1)$**

```
class matrix:
	def negatives_count(self, matrix: List[List[int]]) -> int:
		return sum(map(self.binary_search, matrix))
	def binary_search(arr:list) -> int:
		left, right = 0, len(arr) -1
		while left <= right:
			mid = (left + right) // 2
			if arr[mid] < 0:
				right = mid - 1
			else:
				left = mid + 1
		return len(arr) - left 
```

**Time complexity $O(n+m)$ and space complexity $O(1)$**
```
def negatives_count(matrix):
	i,j = len(matrix) - 1,0
	count = 0
	while i >= 0 and j < len(matrix[0]):
	    print(i,j)
	    if matrix[i][j] < 0:
	        count += len(matrix[0]) -j
	        print(count)
	        i -= 1
	    else:
	        j += 1
```


