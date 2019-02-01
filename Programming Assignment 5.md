## Programming Assignment 5: Dynamic Programming 1
### 5.1. Money Change Again
**Task:** Integer *money*.\
**Input Format:** The minimum number of coins with denominations *1, 3, 4* that changes *money*.\
**Constraints:** *1 ≤ money ≤ 10<sup>3</sup>*.

```python
import math

def get_change(m):
    min_coins = [0 for i in range(m+1)]
    min_coins[0] = 0
    
    for money in range(1,m+1):
        min_coins[money] = math.inf
        for c in [1,3,4]:
            if money >= c:
                numCoins = min_coins[money-c] + 1
                if numCoins < min_coins[money]:
                    min_coins[money] = numCoins
    
    return min_coins[m]
```

### 5.2. Primitive Calculator
**Task:** Given an integer *n*, compute the minimum number of operations needed to obtain the number n starting from the number 1.\
**Input Format:** The input consists of a single integer *1 ≤ n ≤ 10<sup>6</sup>*.\
**Output Format:** In the first line, output the minimum number *k* operations needed to get *n* from 1. In the second line output a sequence of intermediate numbers. That is, the second line should contain positive integers *a<sub>0</sub>, a<sub>1</sub>, ..., a<sub>k-1</sub>* such that *a<sub>0</sub> = 1, a<sub>k-1</sub> = n* and for all *0 ≤ i ≤ k-1, a<sub>i+1</sub>* is equal to either *a<sub>i</sub> + 1, 2a<sub>i</sub>* or *3a<sub>i</sub>*. If there are many such sequences, output any one of them.

```python
import math

def optimal_sequence(n):
    min_operations = [[0,[]] for i in range(n+1)]
    min_operations[1][1].append(1)
    
    for number in range(2,n+1):
        min_operations[number][0] = math.inf
        
        operations = [1]
        if number % 2 == 0:
            operations.append(number // 2)
        
        if number % 3 == 0:
            operations.append(2 * (number // 3))
        
        for o in operations:
            if number >= o:
                numOperations = min_operations[number-o][0] + 1
                sequence = [i for i in min_operations[number-o][1]]
                sequence.append(number)
                                
                if numOperations < min_operations[number][0]:
                    min_operations[number][0] = numOperations
                    min_operations[number][1] = sequence
                    
    return min_operations[n][1]
```

### 5.3. Computing The Edit Distance Between Two Strings
**Task:** The goal of this problem is to implement the algorithm for computing the edit distance between twostrings.\
**Input Format:** Each of the two lines of the input contains a string consisting of lower case latin letters.\
**Contraints:** The length of both strings is at least *1* and at most *100*.\
**Output Format:** Output the edit distance between the given two strings.

```python
def edit_distance(s, t):
    m = len(s)
    n = len(t)
    
    # initiate distance matrix
    d = [[0 for j in range(n+1)] for i in range(m+1)]
    for i in range(m+1):
        d[i][0] = i
        
    for j in range(n+1):
        d[0][j] = j
    
    # calculate distance matrix
    for i in range(1,m+1):
        for j in range(1,n+1):
            D1 = d[i-1][j] + 1 #insertion
            D2 = d[i][j-1] + 1 #deletion
            D3 = d[i-1][j-1] #match
            
            if s[i-1] != t[j-1]:
                D3 = d[i-1][j-1] + 1 #mismatch
            d[i][j] = min(D1,D2,D3)
    
    return d[m][n]
```

### 5.4. Longest Common Subsequence of Two Sequences
**Task:** Given two sequences *A = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>)* and *B = (b<sub>1</sub>, b<sub>2</sub>, ..., b<sub>m</sub>)*, find the length of their longest common subsequence, i.e., the largest non-negative integer *p* such that there exist indices *1 ≤ i<sub>1</sub> < i<sub>2</sub> < ··· < i<sub>p</sub> ≤ n* and *1 ≤ j<sub>1</sub> < j<sub>2</sub> < ··· < j<sub>p</sub> ≤ m*, such that *a<sub>i<sub>1</sub></sub> = b<sub>j<sub>1</sub></sub>, ..., a<sub>i<sub>p</sub></sub> = b<sub>j<sub>p</sub></sub>*.\
**Input Format:** First line: *n*. Second line: *a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>*. Third line: *m*. Fourth line: *b<sub>1</sub>, b<sub>2</sub>, ..., b<sub>m</sub>*.\
**Contraints:** *1 ≤ n, m ≤ 100*; *−10<sup>9</sup> < a<sub>i</sub>, b<sub>i</sub> <10<sup>9</sup>*.\
**Output Format:** Output *p*.

```python
def lcs2(a, b):
    m = len(a)
    n = len(b)
    
    # initiate distance matrix
    d = [[0 for j in range(n+1)] for i in range(m+1)]
    
    # calculate distance matrix
    for i in range(1,m+1):
        for j in range(1,n+1):
            D1 = d[i-1][j] #insertion
            D2 = d[i][j-1] #deletion
            D3 = d[i-1][j-1] + 1 #match
            
            if a[i-1] != b[j-1]:
                D3 = d[i-1][j-1] #mismatch
            d[i][j] = max(D1,D2,D3)
    
    return d[m][n]
```

### 5.5. Longest Common Subsequence of Three Sequences
**Task:** Given two sequences *A = (a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>), B = (b<sub>1</sub>, b<sub>2</sub>, ..., b<sub>m</sub>)* and C = (c<sub>1</sub>, c<sub>2</sub>, ..., c<sub>l</sub>)*, find the length of their longest common subsequence, i.e., the largest non-negative integer *p* such that there exist indices *1 ≤ i<sub>1</sub> < i<sub>2</sub> < ··· < i<sub>p</sub> ≤ n, 1 ≤ j<sub>1</sub> < j<sub>2</sub> < ··· < j<sub>p</sub> ≤ m* and *1 ≤ k<sub>1</sub> < k<sub>2</sub> < ··· < k<sub>p</sub> ≤ l*, such that *a<sub>i<sub>1</sub></sub> = b<sub>j<sub>1</sub></sub> = c<sub>k<sub>1</sub></sub>, ..., a<sub>i<sub>p</sub></sub> = b<sub>j<sub>p</sub></sub> = c<sub>k<sub>p</sub></sub>*.\
**Input Format:** First line: *n*. Second line: *a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub>*. Third line: *m*. Fourth line: *b<sub>1</sub>, b<sub>2</sub>, ..., b<sub>m</sub>*. Fifth line: *l*. Sixth line: *c<sub>1</sub>, c<sub>2</sub>, ..., c<sub>l</sub>*.\
**Contraints:** *1 ≤ n, m, l ≤ 100*; *−10<sup>9</sup> < a<sub>i</sub>, b<sub>i</sub>, c<sub>i</sub> <10<sup>9</sup>*.\
**Output Format:** Output *p*.

```python

```
