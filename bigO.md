## Introduction
Time complexity is a fundamental concept in computer science that helps us understand how the runtime of an algorithm grows as the input size increases.

Big O notation describes the upper bound of an algorithm's time complexity in the worst-case scenario. It answers the question: "How does the runtime grow as the input size grows?"

**Key concepts:**
* We focus on dominant terms and ignore constants
* We care about growth rate, not actual time in seconds
* We typically analyze worst-case scenarios
* **We compare the output in terms of the input.**

## Common orders of growth (Time complexities) 

### O(1) - Constant Time Complexity (O(1)) Algorithims

These are the algorithims that execute in the same amount of time regardless of the input size. In other words, the time taken to complete the task remains constant even as the input grows.

#### Implementation Examples

```python
def access_element(arr, index):
    return arr[index]  # Accessing by index is O(1)

def check_first_element(arr):
    if len(arr) > 0:
        return arr[0]  # First element access is O(1)
    return None
```
In both examples, the return value is not dependent on the size of the input. Therefore, execution time remains consistent for lists of 10 or 10,000 elements. So the relationship between input size and output is constant, and the time complexity is O(1).

**Common O(1) Operations: List indexing, accessing dictionary, getting the length of a list or a string.**
