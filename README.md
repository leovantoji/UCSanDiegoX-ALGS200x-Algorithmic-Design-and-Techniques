# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

Fibonacci Numbers
Recall the definition of Fibonacci sequence: 
```math
F_0 = 0`$
```

$`𝐹_1 = 1`$, and $`𝐹_𝑖 = 𝐹_(𝑖−1) +𝐹_𝑖−2`$ for 
$`𝑖 ≥ 2`$. Your goal in this problem is to implement an efficient algorithm for computing
Fibonacci numbers.

```
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

Greatest Common Divisors

- Big-O, Omega-O, Theta-O Notation
- Greedy Algorithms:
  - A choice is called safe when there's an optimal solution consistent with this first choice
  - Not all first choices are safe
  - Greedy choices are often unsafe
- Divide and Conquer
