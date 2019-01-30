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

```
