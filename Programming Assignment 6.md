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
