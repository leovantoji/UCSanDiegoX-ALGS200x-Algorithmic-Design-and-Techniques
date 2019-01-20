## Programming Assignment 3: Greedy Algorithms
### 3.1. Changing Money
**Task:** The goal in this problem is to find the minimum number of coins needed to change the input value (an integer) into coins with denominations 1, 5, and 10 cents.\
**Input Format:** The input consists of a single integer *m*.\
**Constraints:** *0 ≤ m ≤ 10<sup>3</sup>*.\
**Output Format:** Output the minimum number of coins with denominations 1, 5, 10 that changes *m*.

```python
def get_change(m):
    coins = 0

    while m > 0:
        if m >= 10:
            additional_coins = m // 10
            coins += additional_coins
            m -= additional_coins * 10
        elif m >= 5:
            additional_coins = m // 5
            coins += additional_coins
            m -= additional_coins * 5
        else:
            coins += m
            m = 0

    return coins
```

### 3.2. Maximizing the Value of a Loot
**Task:** The goal of this code problem is to implement an algorithm for the fractional knapsack problem.\
**Input Format:** The first line of the input contains the number of *n* items and the capacity *W* of a knapsack. The next *n* lines define the values and weights of the items. The *i<sup>th</sup>* line contains integers *v<sub>i</sub>* and *w<sub>i</sub>* - the value and the weight of the *i<sup>th</sup>* item respectively.\
**Constraints:** *0 ≤ n ≤ 10<sup>3</sup>, 0 ≤ W ≤ 2 x 10<sup>6</sup>, 0 ≤ v<sub>i</sub> ≤ 2 x 10<sup>6</sup>, 0 ≤ w<sub>i</sub> ≤ 2 x 10<sup>6</sup>* for all *0 ≤ i ≤ n.* All the numbers are integers.\
**Output Format:** Output the maximal value of fractions of items that fit into the knapsack. The absolute value of the difference between the answer of your program and the optimal value should be at most *10<sup>-3</sup>*. To ensure this, out put your answer with at least four digits after the decimal points. Otherwise, your answer, while being computed correctly, can turn out to be wrong because of rounding issues.

```python
def get_optimal_value(capacity, weights, values):
    value = 0
    #calculate the value per weight unit
    vpw = [v/w for w, v in list(zip(weights, values))]
    
    items = list(zip(vpw, weights, values))
    #sort items in descending order of value per weight unit
    items.sort(reverse = True)
    
    #append items back to list in descending order of value per weight unit
    vpw = []
    weights = []
    values = []
    
    for i in range(len(items)):
        vpw.append(items[i][0])
        weights.append(items[i][1])
        values.append(items[i][2])
    
    #add fractions of items with highest value per weight unit until the knapsack is filled
    #start with the highest value per weight unit item
    i = 0
    
    while capacity > 0 and i < len(items):
        if capacity < weights[i]:
            value += capacity * vpw[i]
            capacity = 0
        else:
            value += values[i]
            capacity -= weights[i]
            i += 1
    
    return value
```

### 3.3. Maximizing Revenue in Online Ad Placement
**Task:** Given two sequences *a<sub>1</sub>, a<sub>2</sub> ... a<sub>n</sub>* (*a<sub>i</sub>* is the profit per click of the *i<sup>th</sup>* ad) and *b<sub>1</sub>, b<sub>2</sub> ... b<sub>n</sub>* (*b<sub>i</sub>* is the average number of clicks per day of the *i<sup>th</sup>* slot), we need to partition them into *n* pairs (*a<sub>i</sub>, b<sub>j</sub>*) such that the sum of their products is maximized.\
**Input Format:** The first line contains an integer *n*. The second one contains a sequence of integers *a<sub>1</sub>, a<sub>2</sub> ... a<sub>n</sub>*. The third one contains a sequence of integers *b<sub>1</sub>, b<sub>2</sub> ... b<sub>n</sub>*.\
**Constraints:** *0 ≤ n ≤ 10<sup>3</sup>, -10<sup>5</sup> ≤ a<sub>i</sub>, b<sub>i</sub> ≤ 10<sup>5</sup>* for all *1 ≤ i ≤ n*.\
**Output Format:** Output the maximum value of *Σ︀a<sub>i</sub>c<sub>i</sub>* where *c<sub>1</sub>, c<sub>2</sub> ... c<sub>n</sub>* is a permutation of *b<sub>1</sub>, b<sub>2</sub> ... b<sub>n</sub>*.

```python
# leveraging built-in sort() method
def max_dot_product(a, b):
    res = 0
    a.sort()
    b.sort()
    for i in range(len(a)):
        res += a[i] * b[i]
    return res

# without sort() method
import math

def find_max(a):
    max_value = -math.inf
    max_index = 0
    for i in range(len(a)):
        if a[i] > max_value:
            max_value = a[i]
            max_index = i

    return max_index

def max_dot_product(a, b):
    res = 0

    while len(a) > 0:
        max_a = find_max(a)
        max_b = find_max(b)
        res += a[max_a] * b[max_b]
        a.pop(max_a)
        b.pop(max_b)

    return res
```

### 3.4. Collecting Signatures
**Task:** Given a set of *n* of segments *{[a<sub>0</sub>, b<sub>0</sub>], [a<sub>1</sub>, b<sub>1</sub>] ... [a<sub>n-1</sub>, b<sub>n-1</sub>]}* with integer coordinates on a line, find the minimum number *m* of points such that each segment contains at least one point. That is, find a set of integers *X* of the minimum size such that for any segment *[a<sub>i</sub>, b<sub>i</sub>]* there is a point *x ∈ X* such that *a<sub>i</sub> ≤ x ≤ b<sub>i</sub>*.\
**Input Format:** The first line contains the number *n* of segments. Each of the following *n* lines contains two integers *a<sub>i</sub>* and *b<sub>i</sub>* (separated by a space) defining the coordinates of endpoints of the *i<sup>th</sup>* segment.\
**Constraints:** *0 ≤ n ≤ 100, 0 ≤ a<sub>i</sub> ≤ b<sub>i</sub> ≤ 10<sup>9</sup>* for all *0 ≤ i ≤ n*.\
**Output Format:** Output the minimum number of *m* points on the first line and the integer coordinates of *m* points (separated by spaces) on the second line. You can output the points in any order. If there are many such sets of points, you can output any set. (It is not difficult to see that there always exists a set of points of the minimum size such that all the coordinates of the points are integers).

```python
import math

def find_best_point(segments):
    best_point = -math.inf

    for s in segments:
        if s.start > best_point:
            best_point = s.start

    checked_segments = [s for s in segments if (best_point >= s.start and best_point <= s.end)]

    for s in checked_segments:
        segments.remove(s)

    return best_point, segments

def optimal_points(segments):
    points = []

    while (len(segments) > 0):
        best_point, segments = find_best_point(segments)
        points.append(best_point)

    return points
```

### 3.5. Maximizing the Number of Prize Places in a Competition
**Task:** The goal of this problem is to represent a given positive integer *n* as a sum of as many pairwise distinct positive integers as possible. That is, to find the maximum *k* such that *n* can be written as *a<sub>1</sub> + a<sub>2</sub> + ... + a<sub>k</sub>* where *a<sub>1</sub>, a<sub>2</sub> ... a<sub>k</sub>* are positive integers and *a<sub>i</sub> != a<sub>j</sub>* for all *1 ≤ i < j ≤ k*.\
**Input Format:** The input contains a single integer *n*.\
**Constraints:** *1 ≤ n ≤ 10<sup>9</sup>*.\
**Output Format:** In the first line, output the maximum number *k* such that *n* can be represented as a sum of *k* pairwise distinct positive integers. In the second line, output *k* pairwise distinct positive integers that sum up to *n* (if there are many such representations, output any of them).

```python
def optimal_summands(n):
    summands = []

    k = 1
    while n > 0:
        if (n - k) > k  or (n == k):
            summands.append(k)
            n -= k
        k += 1

    return summands
```

### 3.6. Maximizing Your Salary 
**Task:** Compose the largest number out of a set of integers.\
**Input Format:** The first line contains an integer *n*. The second one contains *n* integers *a<sub>1</sub>, a<sub>2</sub> ... a<sub>n</sub>*.\
**Constraints:** *1 ≤ n ≤ 100, 1 ≤ a<sub>i</sub> ≤ 10<sup>3</sup>* for all *1 ≤ i ≤ n*.\
**Output Format:** Output the largest number that can be composed out of *a<sub>1</sub>, a<sub>2</sub> ... a<sub>n</sub>*.

```python
def is_greater_or_equal(number, maxNumber):    
    combo_one = str(number) + str(maxNumber)
    combo_two = str(maxNumber) + str(number)
    return int(combo_one) >= int(combo_two)

def largest_number(a):
    res = ''
    
    while len(a) > 0:
        maxNumber = a[0]
        for number in a:
            if is_greater_or_equal(number, maxNumber):
                maxNumber = number
        
        res += maxNumber
        a.remove(maxNumber)
        
    return res
```
