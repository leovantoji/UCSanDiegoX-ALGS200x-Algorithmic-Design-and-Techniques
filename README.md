# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

## Course Summary
- Big-O, Omega, Theta Notation
- Greedy Algorithms:
  - A choice is called safe when there's an optimal solution consistent with this first choice
  - Not all first choices are safe
  - Greedy choices are often unsafe
- Divide and Conquer:
  - The run time of linear search is θ(*n*), while the run time of binary search is θ(log *n*)
  - Polynomial Multiplication:
    - Naive: *O(n<sup>2</sup>)*
    - Faster: *O(n<sup>log<sub>2</sub>3</sup>)*
- Master Theorem: If *T(n) = aT(nb<sup>-1</sup>) + O(n<sup>d</sup>)* for constants *a > 0, b > 1, d ≥ 0)*, then: 
  -*T(n) = O(n<sup>d</sup>)* if *d > log<sub>b</sub>a*
  -*T(n) = O(n<sup>d</sup>* log*n*) if *d = log<sub>b</sub>a*
  -*T(n) = O(n<sup>log<sub>b</sub>a</sup>)* if *d < log<sub>b</sub>a*
