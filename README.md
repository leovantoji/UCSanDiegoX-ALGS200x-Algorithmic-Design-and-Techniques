# UCSanDiegoX-ALGS200x-Algorithmic-Design-and-Techniques

## Course Summary
- Big-O, Big-Omega, Big-Theta Notation
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
  ```python
  def mergesort(a):
    n = len(a)
    if len(a) <= 1:
        return a
    
    mid = n // 2
    b = mergesort(a[:mid])
    c = mergesort(a[mid:])
    d = merge(b,c)
    return d

  def merge(b,c):
    d = []
    i = j = 0
    while i < len(b) and j < len(c):
        if b[i] <= c[j]:
            d.append(b[i])
            i += 1
        else:
            d.append(c[j])
            j += 1
    
    while i < len(b):
        d.append(b[i])
        i += 1
    
    while j < len(c):
        d.append(c[j])
        j += 1
    
    return d
    ```
  - Quick Sort: Assume that all the elements of *A[1 ... n]* are pairwise different. Then the average running time of Randomized Quick Sort is *O(n*log*n)*, while the worst case running time is *O(n<sup>2</sup>)*. Three way partition can be used to tackle array having equal elements.
  - Insertion Sort: 
  - Bubble Sort:
  - Shell Sort: 
