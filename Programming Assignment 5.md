## Programming Assignment 5: Dynamic Programming 1
### 5.1. Money Change Again
**Task:** Integer *money*.\
**Input Format:** The minimum number of coins with denominations 1, 3, 4 that changes *money*.\
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
