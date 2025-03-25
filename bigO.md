# Big O Notation Study Notes

## Introduction

Big O notation describes the upper bound of an algorithm's time complexity in the worst-case scenario. It answers the question: "How does the runtime grow as the input size grows?"

**Key concepts:**
* We focus on dominant terms and ignore constants
* We care about growth rate, not actual time in seconds
* We typically analyze worst-case scenarios
* **We compare the output in terms of the input**

## Common Orders of Growth (Time Complexities)

### Constant Time Complexity O(1) Algorithms

These are algorithms that execute in the same amount of time regardless of the input size. In other words, the time taken to complete the task remains constant even as the input grows.

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
In both examples, the return value is not dependent on the size of the input. Therefore, execution time remains consistent for lists of 10 or 10,000 elements. The relationship between input size and output is constant, and the time complexity is O(1).

**Common O(1) Operations:** List indexing, accessing dictionary items, getting the length of a list or a string, inserting at the beginning of a linked list.

**Additional Example:**
```python
def check_if_empty(container):
    return len(container) == 0  # O(1) operation

# Dictionary lookup
def get_value(dictionary, key):
    if key in dictionary:  # table lookup is O(1)
        return dictionary[key]
    return None
```

### Logarithmic Time Complexity O(log n) Algorithms

In this case, the runtime increases logarithmically with the size of the input, usually by repeatedly dividing the input into smaller parts. **Any algorithm that splits the input into multiple sections generally exhibits a time complexity of O(log n).** A common example of an O(log n) algorithm is the binary search.

```python
def binary_search(arr: list, target: int):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2 #notice the division here!
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
    half = binary_exponentiation(base, exponent // 2)  # Notice the division here!
    
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
        mid = (low + high)//2  # Notice the division here!
        if L[mid] == e:
            return True
        elif L[mid] > e:
            if low == mid:  # Nothing left to search
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

```python
def program2(x):
    total = 0
    for i in range(1000):
        total = i

    while x > 0:
        x = x//2  # Notice the division here!
        total += x

    return total
```
This algorithm has a time complexity of O(log n) because the while block continues to execute until x reaches zero.
However, x doesn't change linearly here; x gets divided by 2 each iteration, so this algorithm has a logarithmic time complexity instead of a linear time complexity.

### Linear Time Complexity O(n) Algorithms

Runtime grows linearly with input size.

```python 
def program1(x):
    total = 0
    for i in range(1000):
        total += i

    while x > 0:
        x -= 1
        total += x

    return total
```
Notice that this program is similar to the last example of logarithmic complexity examples. However, the main difference here is that the code inside the `while` block changes linearly, by 1 each iteration. Unlike the logarithmic complexity example in which x was divided in each iteration. This distinction makes this example have a linear time complexity O(n).

```python
def find_maximum(arr):
    if not arr:
        return None
    
    max_value = arr[0]
    for element in arr:  # Single loop through n elements
        if element > max_value:
            max_value = element
    
    return max_value
```

**Additional Examples:**
```python
def sum_elements(arr):
    """Calculate the sum of all elements in an array."""
    sum_total = 0
    for element in arr:  # O(n) - we must visit each element
        sum_total += element
    return sum_total

def contains_duplicate(arr):
    """Check if array contains any duplicate value."""
    seen = set()
    for element in arr:  # O(n) - we must check each element
        if element in seen:  # O(1) for set lookup
            return True
        seen.add(element)  # O(1) for set insertion
    return False
```

## Additional Time Complexities

### O(n log n) Algorithms

These typically involve dividing a problem into subproblems, solving them, and combining results. Common in efficient sorting algorithms.

```python
def merge_sort(arr):
    if len(arr)  arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr
```

### Exponential O(2ⁿ) Algorithms

These typically increase the number of operations exponentially with input size, often seen in recursive algorithms without memoization.

```python
def fibonacci_recursive(n):
    if n <= 1:
        return n
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2) # O(2^n) due to repeated calls
```

```python
def generate_subsets(nums):
    result = [[]]
    for num in nums:
        result += [subset + [num] for subset in result]
    return result
```
