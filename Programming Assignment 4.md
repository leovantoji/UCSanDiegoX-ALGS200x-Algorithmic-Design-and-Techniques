## Programming Assignment 4: Divide and Conquer
### 4.1. Changing Money
**Task:** The goal of this code problem is to implement the binary search algorithm.\
**Input Format:** The first line of the input contains an integer *n* and a sequence *a<sub>0</sub> < a<sub>1</sub> < ... < a<sub>n-1</sub>* of *n* pairwise distinct positive integers in increasing order. The next line contains an integer *k* and *k* positive integers *b<sub>0</sub>, b<sub>1</sub>, ... , b<sub>k-1</sub>*.\
**Constraints:** *1 ≤ n,k ≤ 10<sup>4</sup>*; *1 ≤ a<sub>i</sub> ≤ 10<sup>9</sup>* for all *0 ≤ i < n*; *1 ≤ b<sub>j</sub> ≤ 10<sup>9</sup>* for all *0 ≤ j < k*.\
**Output Format:** For all *i* from 0 to *k-1*, output an index *0 ≤ j < n-1* such that *a<sub>j</sub> = b<sub>i</sub>* or -1 if there is no such index.

```python
def binary_search(a, x):
    left, right = 0, len(a) - 1
    while left <= right:
        mid = (left + right) // 2
        if a[mid] == x:
            return mid
        elif a[mid] > x:
            right = mid - 1
        else:
            left = mid + 1
    return -1
```
