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
**Output Format:** Output this sequence sorted in non-decreasing order.

```python
def partition3(a, l, r):
    x = a[l]
    j = l # < x starting pos
    k = l # = x starting pos
    for i in range(l + 1, r + 1):
        if a[i] < x:
            j += 1
            k += 1
            a[i], a[k] = a[k], a[i]
            a[j], a[k] = a[k], a[j]
        elif a[i] == x:
            k += 1
            a[i], a[k] = a[k], a[i]
    a[l], a[j] = a[j], a[l]
    return j, k

def randomized_quick_sort(a, l, r):
    if l >= r:
        return a
    k = random.randint(l, r)
    a[l], a[k] = a[k], a[l]
    m1, m2 = partition3(a, l, r)
    randomized_quick_sort(a, l, m1 - 1)
    randomized_quick_sort(a, m2 + 1, r)
    return a
```

### 4.4. Number of Inversions
**Task:** The goal in this problem is to count the number of inversions of a given sequence.\
**Input Format:** The first line of the input contains an integer *n* and a sequence of *n* integers *a<sub>0</sub>, a<sub>1</sub>, ..., a<sub>n-1</sub>*.\
**Constraints:** *1 ≤ n ≤ 10<sup>5</sup>*; *0 ≤ a<sub>i</sub> ≤ 10<sup>9</sup>* for all *0 ≤ i < n*.\
**Output Format:** Output the number of inversions in the sequence.

```python
def get_number_of_inversions(a, b, left, right):
    number_of_inversions = 0
    if right - left <= 1:
        return number_of_inversions
    ave = (left + right) // 2
    number_of_inversions += get_number_of_inversions(a, b, left, ave)
    number_of_inversions += get_number_of_inversions(a, b, ave, right)
    #write your code here
    number_of_inversions += merge(a, b, left, ave, right)
    return number_of_inversions

def merge(a, b, left, ave, right):
    number_of_inversions = 0
    i = k = left
    j = ave
    while i < ave and j < right:
        if a[i] <= a[j]:
            b[k] = a[i]
            i += 1
        else:
            number_of_inversions += ave - i
            b[k] = a[j]
            j += 1
        k += 1
        
    while i < ave:
        b[k] = a[i]
        k += 1
        i += 1
        
    while j < right:
        b[k] = a[j]
        k += 1
        j += 1
    
    for i in range(left, right):
        a[i] = b[i]
    
    return number_of_inversions
```

### 4.5. Organizing a Lottery
**Task:** You are given a set of points on a line and a set of segments on a line. The goal is to compute, for each point, the number of segments that contain this point.\
**Input Format:** The first line contains two non-negative integer *s* and *p* defining the number of segments and the number of points on a line, respectively. The next *s* lines contain two integers *a<sub>i</sub>, b<sub>i</sub>* defining the *i<sup>th</sup>* segment *[a<sub>i</sub>, b<sub>i</sub>]*. The next line contains *p* integers defining points *x<sub>1</sub>, x<sub>2</sub>, ... , x<sub>p</sub>*.\
**Constraints:** *1 ≤ s, p ≤ 50000*; *-10<sup>8</sup> ≤ a<sub>i</sub> ≤ b<sub>i</sub> ≤ 10<sup>8</sup>* for all *0 ≤ i < s*; *-10<sup>8</sup> ≤ x<sub>j</sub> ≤ 10<sup>8</sup>* for all *0 ≤ j < p*.\
**Output Format:** Output *p* non-negative integers *k<sub>0</sub>, k<sub>1</sub>, ... , k<sub>p-1</sub>* where *k<sub>i</sub>* is the number of segments which contain *x<sub>i</sub>*.

```python

```

### 4.6. Finding the Closest Pair of Points
**Task:** Given *n* points on a plane, find the smallest distance between a pair of two (different) points. Recall that the distance between points *(x<sub>1</sub>, y<sub>1</sub>)* and *(x<sub>2</sub>, y<sub>2</sub>)* is equal to sqrt[(*x<sub>1</sub> - x<sub>2</sub>)<sup>2</sup> + (y<sub>1</sub> - y<sub>2</sub>)<sup>2</sup>*].\
**Input Format:** The first line contains the number *n* of points. Each of the following *n* lines defines a point *(x<sub>i</sub>, y<sub>i</sub>)*.\
**Constraints:** *2 ≤ n ≤ 10<sup>5</sup>*; *-10<sup>9</sup> ≤ x<sub>i</sub>, y<sub>i</sub> ≤ 10<sup>9</sup>* are integers.\
**Output Format:** Output the minimum distance. The absolute value of the difference between the answer of your program and the optimal value should be at most *10<sup>-3</sup>*. To ensure this, output your answer with at least four digits after the decimal point (otherwise, your answer, while being computed correctly, can turn out to be wrong because of rounding issues).

```python

```
