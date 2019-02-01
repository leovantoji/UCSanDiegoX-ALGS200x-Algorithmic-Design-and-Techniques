## Programming Assignment 6: Dynamic Programming 2
### 6.1. Maximum Amount of Gold
**Task:** Given *n* gold bars, find the maximum weight of gold that fits into a bag of capacity *W*.\
**Input Format:** The first line of the input contains the capacity *W* of a knapsack and the number *n* of bars of gold. The next line contains *n* integers *w<sub>0</sub>, w<sub>1</sub>, ..., w<sub>n-1</sub>* defining the weights of the bars of gold.\
**Constraints:** *1 ≤ W ≤ 10<sup>4</sup>*; *1 ≤ n ≤ 300*; *0 ≤ w<sub>0</sub>, ..., w<sub>n-1</sub> ≤ 10<sup>5</sup>*\.
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
**Constraints:** *1 ≤ n ≤ 20*; *1 ≤ v<sub>i</sub> ≤ 30* for all *i*\.
**Output Format:** Output *1*, if it possible to partition *v<sub>1</sub>, v<sub>2</sub>, ..., v<sub>n</sub>* into three subsets with equal sums, and 0 otherwise.

```python

```
