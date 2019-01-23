## Programming Assignment 4: Divide and Conquer
### 4.1. Binary Search
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

### 4.2. Majority Element
**Task:** The goal in this code problem is to check whether an input sequence contains a majority element.\
**Input Format:** The first line of the input contains an integer *n* and a sequence of *n* non-negative integers *a<sub>0</sub>, a<sub>1</sub>, ..., a<sub>n-1</sub>*.\
**Constraints:** *1 ≤ n ≤ 10<sup>5</sup>*; *0 ≤ a<sub>i</sub> ≤ 10<sup>9</sup>* for all *0 ≤ i < n*.\
**Output Format:** Output 1 if the sequence contains an element that appears strictly more than *n/2* times, and 0 otherwise.

```python
def get_majority_element(a, left, right):
    if left == right:
        return -1
    if left + 1 == right:
        return a[left]
    
    mid = (left + right - 1) // 2 + 1
    me_left = get_majority_element(a, left, mid)
    me_right = get_majority_element(a, mid, right)

    count_left = 0
    count_right = 0
    for i in range(left, right):
        if a[i] == me_left:
            count_left += 1
        elif a[i] == me_right:
            count_right += 1
    
    n = (right - left) // 2
    if count_left > n:
        return me_left
    elif count_right > n:
        return me_right
    
    return -1
```

### 4.3. Improving Quick Sort
**Task:** To force the given implementation of the quick sort algorithm to efficiently process sequences with few unique elements, your goal is replace a 2-way partition with a 3-way partition. That is, your new partition procedure should partition the array into 3 parts: *< x* part, *= x* part, and *> x* part.\
**Input Format:** The first line of the input contains an integer *n* and a sequence of *n* integers *a<sub>0</sub>, a<sub>1</sub>, ..., a<sub>n-1</sub>*.\
**Constraints:** *1 ≤ n ≤ 10<sup>5</sup>*; *0 ≤ a<sub>i</sub> ≤ 10<sup>9</sup>* for all *0 ≤ i < n*.\
**Output Format:** Output this sequence sorted in non-decreasing order

```python
```
