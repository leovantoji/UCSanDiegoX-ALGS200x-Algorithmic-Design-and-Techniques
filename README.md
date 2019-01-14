# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

## Programming Assignment 2
### 1. Fibonacci Numbers
Fibonacci sequence: *F<sub>0</sub> = 0*, *F<sub>1</sub> = 1*, and *F<sub>i</sub> = F<sub>i-1</sub> + F<sub>i-2</sub>* for *i >= 2*.

**Task:** Given an integer *n*, find the *n<sup>th</sup>* Fibonacci number *F<sub>n</sub>*

**Input Format:** The input consists of a single integer *n*

**Constraints:** *0 ≤ n ≤ 45*

**Output Format:** Output *F<sub>n</sub>*

```python
def calc_fib(n):
     if n <= 1:
        return n
     else:
        fib = [0 for i in range(n+1)]
        fib[0] = 0
        fib[1] = 1

        for i in range(2,n+1):
        fib[i] = fib[i-1] + fib[i-2]

        return fib[n]
```

### 2. Last Digit of a Large Fibonacci Number
**Task:** Given an integer *n*, find the last digit of the *n<sup>th</sup>* Fibonacci number *F<sub>n</sub>* (that is, *F<sub>n</sub>* `mod` 10)

**Input Format:** The input consists of a single integer *n*

**Constraints:** *0 ≤ n ≤ 107*

**Output Format:** Output the last digit of *F<sub>n</sub>*

```python
def get_fibonacci_last_digit_fast(n):
    if n <= 1:
        return n

    last_digit = [0 for i in range(n+1)]
    last_digit[0] = 0
    last_digit[1] = 1

    for i in range(2,(n+1)):
        last_digit[i] = (last_digit[i-1] + last_digit[i-2]) % 10

    return last_digit[n]
```

### 3. Greatest Common Divisors
**Task:** Given two integers *a* and *b*, find their greatest common divisor

**Input Format:** The two integers *a*, *b* are given in the same line separated by space

**Constraints:** *1 ≤ a, b ≤ 2 x 10<sup>9</sup>*

**Output Format:** Output the greatest common divisor of *a* and *b*

```python
def gcd_fast(a, b):
    while min(a,b) != 0:
        if a > b:
            a %= b
        else:
            b %= a
     
    return max(a,b)
```

### 4. Least Common Multiple
**Task:** Given two integers *a* and *b*, find their least common multiple

**Input Format:** The two integers *a*, *b* are given in the same line separated by space

**Constraints:** *1 ≤ a, b ≤ 2 x 10<sup>9</sup>*

**Output Format:** Output the least common multiple of *a* and *b*

```python
def gcd_fast(a, b):
    while min(a,b) != 0:
        if a > b:
            a %= b
        else:
            b %= a
     
    return max(a,b)

def lcm_fast(a, b):
    return int(a * b // gcd(a,b))
```

### 5. Fibonacci Number Again
**Task:** Given two integers *n* and *m*, output *F<sub>n</sub>* `mod` *m* (that is, the remainder of *F<sub>n</sub>* `mod` *m*)

**Input Format:** The two integers *n*, *m* are given in the same line separated by space

**Constraints:** *1 ≤ n ≤ 10<sup>18</sup>, 2 ≤ m ≤ 10<sup>5</sup>*

**Output Format:** Output *F<sub>n</sub>* `mod` *m*

```python
def fib(n):
    if n <= 1:
        return n
    else:
        f = [0 for i in range(n+1)]
        f[0] = 0
        f[1] = 1
        
        for i in range(2,n+1):
            f[i] = f[i-1] + f[i-2]
        
        return f[n] 

def pisano_period_len(m):
    if m < 2:
        return None
    else:
        fib_last_index = 3
        fib_2nd_last = 1 #F(2) = 1
        fib_last = 2 #F(3) = 2

        while True:
            if (fib_2nd_last % m == 0) and (fib_last % m == 1):
                return (fib_last_index-1)
            else:
                temp = fib_2nd_last
                fib_2nd_last = fib_last
                fib_last += temp
                fib_last_index += 1
                
def get_fibonacci_huge_fast(n, m):
    if n <= 1:
        return n
    n %= pisano_period_len(m)
    
    return (fib(n) % m)
```

### 6. Last Digit of the Sum of Fibonacci Numbers
**Task:** Given an integer *n*, find the last digit of the sum *F<sub>0</sub> + F<sub>1</sub> + ... + F<sub>n</sub>*

**Input Format:** The input consists of a single integer *n*

**Constraints:** *0 ≤ n ≤ 10<sup>14</sup>*

**Output Format:** Output the last digit of the sum *F<sub>0</sub> + F<sub>1</sub> + ... + F<sub>n</sub>*

### 7. Last Digit of the Sum of Fibonacci Numbers Again
**Task:** Given two non-negative integers *m* and *n*, where *m ≤ n*, find the last digit of the sum *F<sub>m</sub> + F<sub>m+1</sub> + ... + F<sub>n</sub>*

**Input Format:** The two non-negative integers *m*, *n* are given in the same line separated by space

**Constraints:** *0 ≤ m ≤ n ≤ 10<sup>18</sup>*

**Output Format:** Output the last digit of the sum *F<sub>m</sub> + F<sub>m+1</sub> + ... + F<sub>n</sub>*

- Big-O, Omega-O, Theta-O Notation
- Greedy Algorithms:
  - A choice is called safe when there's an optimal solution consistent with this first choice
  - Not all first choices are safe
  - Greedy choices are often unsafe
- Divide and Conquer
