# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

## Course Summary
- Big-O, Omega, Theta Notation
- Greedy Algorithms:
  - A choice is called safe when there's an optimal solution consistent with this first choice
  - Not all first choices are safe
  - Greedy choices are often unsafe
- Master Theorem: If *T(n) = aT(nb<sup>-1</sup>) + O(n<sup>d</sup>)* for constants *a > 0, b > 1, d ≥ 0)*, then: 
  - *T(n) = O(n<sup>d</sup>)* if *d > log<sub>b</sub>a*
  - *T(n) = O(n<sup>d</sup>* log*n*) if *d = log<sub>b</sub>a*
  - *T(n) = O(n<sup>log<sub>b</sub>a</sup>)* if *d < log<sub>b</sub>a*  
- Divide and Conquer:
  - The run time of linear search is θ(*n*), while the run time of binary search is θ(log *n*)
  - Polynomial Multiplication:
    - Naive: *O(n<sup>2</sup>)*
    - Faster: *O(n<sup>log<sub>2</sub>3</sup>)*
  - Selection Sort: *O(n<sup>2</sup>)*
  - Merge Sort: *O(n*log*n)*. Merge sort is asymptotically optimal. Any comparison-based sorting algorithms needs to make at least *n*log*n* operations.
  - Quick Sort: Assume that all the elements of *A[1 ... n]* are pairwise different. Then the average running time of Randomized Quick Sort is *O(n*log*n)*, while the worst case running time is *O(n<sup>2</sup>)*.
  - Insertion Sort: 
  - Bubble Sort:
  - Shell Sort: 
