## Complexity

![](/notes/images/complexity.jpg)

Assymptotic analysis - describing limiting behavior. F.e. `f(n) = n^2 + 3n`, when n becomes very large, the term 3n becomes insignificant compared to n^2 and we say - `f(n)` asymptotically equal `n^2`.

Complexity is time function versus input size n.  

#### Big-O  
`f(n) = O(g(n))` , when  `c > 0` and `n0 > 0`  
such that `f(n) ≤ c * g(n)`, for all `n ≥ n0`  

It means f(n) grow faster than g(n).  
Or g(n) is upper bound for f(n) for all sufficiently large n → ∞


> 1 = O(n)  
  n = O(n^2)  
  log(n) = O(n)  
  2n + 1 = O(n)   


#### Big-Ω
`f(n) = Ω(g(n))` when there exist constant c that `f(n) ≥ c*g(n)` for for all sufficiently large n.

Lower bound for f(n).  

> n = Ω(1)  
  n^2 = Ω(n)  
  n^2 = Ω(n log(n))  
  2 n + 1 = O(n)

#### Big-Θ
`f(n) = Θ(g(n))` if and only `f(n) = O(g(n))` and `f(n) = Ω(g(n))`  

The upper and lower bounds for f(n).

> 2n = Θ(n)  
  n^2 + 2n + 1 = Θ(n^2)
