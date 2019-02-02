## Programming Assignment 6: Dynamic Programming 2
### 6.1. Maximum Amount of Gold
**Task:** Given *n* gold bars, find the maximum weight of gold that fits into a bag of capacity *W*.\
**Input Format:** The first line of the input contains the capacity *W* of a knapsack and the number *n* of bars of gold. The next line contains *n* integers *w<sub>0</sub>, w<sub>1</sub>, ..., w<sub>n-1</sub>* defining the weights of the bars of gold.\
**Constraints:** *1 ≤ W ≤ 10<sup>4</sup>*; *1 ≤ n ≤ 300*; *0 ≤ w<sub>0</sub>, ..., w<sub>n-1</sub> ≤ 10<sup>5</sup>*.\
**Output Format:** Output the maximum weight of gold that fits into a knapsack of capacity *W*.

```python
def optimal_weight(W, w):
    n = len(w)
    # initiate matrix
    d = [[0 for j in range(W+1)] for i in range(n+1)]
    
    # calculate optimal weight
    for i in range(1,n+1):
        for j in range(1,W+1):
            d[i][j] = d[i-1][j]         
            if w[i-1] <= j:
                weight = d[i-1][j - w[i-1]] + w[i-1]
                if weight > d[i][j]:
                    d[i][j] = weight
    
    return d[n][W]
```

### 6.2. Partitioning Souvenirs
**Task:** The first line contains an integer *n*. The second line contains integers *v<sub>1</sub>, v<sub>2</sub>, ..., v<sub>n</sub>* separated by spaces.\
**Constraints:** *1 ≤ n ≤ 20*; *1 ≤ v<sub>i</sub> ≤ 30* for all *i*.\
**Output Format:** Output *1*, if it possible to partition *v<sub>1</sub>, v<sub>2</sub>, ..., v<sub>n</sub>* into three subsets with equal sums, and *0* otherwise.

```python
# Dynamic Programming
def partition3(A):
    n = len(A)
    sum = 0
    
    for i in range(n): 
        sum += A[i]
    
    if sum % 3 != 0: 
        return 0
      
    part = [[1 for j in range(n + 1)] for i in range(sum // 3 + 1)] 

    for i in range(0, n + 1): 
        part[0][i] = 1

    for i in range(1, sum // 3 + 1): 
        part[i][0] = 0
    
    for i in range(1, sum // 3 + 1):     
        for j in range(1, n + 1): 
            part[i][j] = part[i][j - 1]          
            if i >= A[j - 1]: 
                part[i][j] = max(part[i][j], part[i - A[j - 1]][j - 1]) 
    
    return part[sum // 3][n]

# Brute force
import itertools

def partition3(A):
    for c in itertools.product(range(3), repeat=len(A)):
        sums = [None] * 3
        for i in range(3):
            sums[i] = sum(A[k] for k in range(len(A)) if c[k] == i)

        if sums[0] == sums[1] == sums[2]:
            return 1

    return 0
```

### 6.3. Maximizing the Value of an Arithmetic Expression
**Task:** Find the maximum value of an arithmetic expression by specifying the order of applying its arithmetic operations using additional parentheses.\
**Input Format:** The only line of the input contains a string *s* of length 2*n* + 1 for some *n*, with symbol s<sub>0</sub>, s<sub>1</sub>, ..., s<sub>2n</sub>. Each symbol at an even position of *s* is a digit (that is, an integer from 0 to 9) while each symbol at an odd position is one of three operations from {+,-,\*}.\
**Constraints:** *1 ≤ n ≤ 14* (hence the string contains at most *29* symbols).\
**Output Format:** Output the maximum possible value of the given arithmetic expression among different orders of applying arithmetic operations.

```python
import math

def evalt(a, b, op):
    if op == '+':
        return a + b
    elif op == '-':
        return a - b
    elif op == '*':
        return a * b
    else:
        assert False

def get_maximum_value(dataset):
    n = (len(dataset) - 1) // 2
    m = [[math.inf for j in range(n+1)] for i in range(n+1)]
    M = [[-math.inf for j in range(n+1)] for i in range(n+1)]
    
    for i in range(n+1):
        m[i][i] = M[i][i] = int(dataset[i*2])
    
    def min_max(i,j):
        minimum = math.inf
        maximum = -math.inf

        for k in range(i,j):
            a = evalt(M[i][k],M[k+1][j],dataset[2*k+1])
            b = evalt(M[i][k],m[k+1][j],dataset[2*k+1])
            c = evalt(m[i][k],M[k+1][j],dataset[2*k+1])
            d = evalt(m[i][k],m[k+1][j],dataset[2*k+1])
            minimum = min(minimum,a,b,c,d)
            maximum = max(maximum,a,b,c,d)
    
        return minimum, maximum
    
    for s in range(1,n+1):
        for i in range(0,n-s+1):
            j = i + s
            m[i][j], M[i][j] = min_max(i,j)
    
    return M[0][n]
```
