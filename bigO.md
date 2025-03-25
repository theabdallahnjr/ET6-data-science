## Introduction

Big O notation describes the upper bound of an algorithm's time complexity in the worst-case scenario. It answers the question: "How does the runtime grow as the input size grows?"

**Key concepts:**
* We focus on dominant terms and ignore constants
* We care about growth rate, not actual time in seconds
* We typically analyze worst-case scenarios
* **We compare the output in terms of the input.**

## Common orders of growth (Time complexities) 

### Constant Time Complexity O(1) Algorithms

These are the algorithms that execute in the same amount of time regardless of the input size. In other words, the time taken to complete the task remains constant even as the input grows.

```python
def access_element(arr: list, index):
    return arr[index]  # Accessing by index is O(1)

# Usage example
test_list = [8, 47, 12, 14, 52]
print(access_element(test_list, 2))  # Returns 12
```
```python
def check_first_element(arr: list):
    if len(arr) > 0:
        return arr[0]  # First element access is O(1)
    return None
  
# Usage example
test_list = [8, 47, 12, 14, 52]
print(check_first_element(test_list))  # Returns 8
```
In both examples, the return value is not dependent on the size of the input. Therefore, execution time remains consistent for lists of 10 or 10,000 elements. So the relationship between input size and output is constant, and the time complexity is O(1).

**Common O(1) Operations: List indexing, accessing dictionary, getting the length of a list or a string.**

### Logarithmic Time Complexity O(log n) Algorithms

In this case, the runtime increases logarithmically with the size of the input, usually by repeatedly dividing the input into smaller parts. Any algorithm that splits the input into multiple sections generally exhibits a time complexity of O(log n). A common example of an O(log n) algorithm is the binary search.

```python
def binary_search(arr: list, target: int):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

# Usage example
test_list = [4, 8, 10, 14, 27, 31, 46, 52]
print(binary_search(test_list, 31))  # Returns 5
```
**Binary search is O(log n) because each step eliminates half of the remaining elements.**

```python
def gcd_euclidean(a, b):
    while b:
        a, b = b, a % b
    return a

# Usage example
print(gcd_euclidean(48, 18))  # Returns 6
```
This algorithm has O(log n) complexity, where n is the smaller of the two input integers. This is because the Euclidean algorithm reduces the size of the problem by a factor of at least 2 in each iteration.

```python
def binary_exponentiation(base, exponent):
    if exponent == 0:
        return 1
    
    # Calculate half of the work
    half = binary_exponentiation(base, exponent // 2)
    
    # If exponent is even
    if exponent % 2 == 0:
        return half * half
    else:
        return base * half * half

# Usage example
print(binary_exponentiation(2, 10))  # Returns 1024
```
```python
def bisect_search2(L, e):
    def bisect_search_helper(L, e, low, high):
        if high == low:
            return L[low] == e
        mid = (low + high)//2
        if L[mid] == e:
            return True
        elif L[mid] > e:
            if low == mid: #nothing left to search
            return False
            else:
            return bisect_search_helper(L, e, low, mid - 1)
        else:
            return bisect_search_helper(L, e, mid + 1, high)
    if len(L) == 0:
        return False
    else:
        return bisect_search_helper(L, e, 0, len(L) - 1)

```
The algorithm divides the search space in half with each recursive call (mid = (low + high) // 2). 

* When L[mid] > e, it searches the left half (low to mid-1).
* When L[mid] < e, it searches the right half (mid+1 to high).
* This division continues until the search space is reduced to a single element (high == low).

For a list of size 1000, approximately 10 recursive calls are needed (log₂(1000) ≈ 9.97). Because of the repeated division, this algorithm has a time complexity of O(log n).
