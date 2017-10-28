# Analysis of Algorithms

## Runtime Complexity

Efficiency of run-time algorithms (ordered from fastest to slowest):

|Name|Function|Example|
|----|--------|-------|
|Constant|$1$| `print` |
|Logarithmic|$log(n)$| binary search
|Linear|$n$| Single for/while loop|
|Linear-Logarithmic|$n*log(n)$| Splitting in half within a loop |
|Quadratic|$n^2$| for loop nested inside a for loop |
|Cubic|$n^3$|Three nested loops|
|Exponential|$2^n$|
|Factorial|$n!$|

### Estimating Running times

Notations:

|Name|Notation|Bounds?|Specific Definition|
|-----|--------|-------|------------------|
|Big-O| $O(n)$ | Upper bound| $ f(n) \leq cg(n) \text{ for } n \geq n_0 $
|Big-$\Omega$ | $\Omega(n)$ | Lower bound| $ f(n) \geq cg(n) \text{ for } n \geq n_0 $|
|Big-$\Theta$ | $\Theta(n)$ | Both lower and upper bounds| $ c_1g(n) \leq f(n) \leq c_2g(n) \text{ for } n \geq n_0 $|

### Limit method (domination)

If you have $f(n)$ and want to see if it's $O(g(n))$:

- Take the limit $L = \frac{f(n)}{g(n)} , n\rightarrow \infty$ 
- If $L = 0 \rightarrow$, $f(n)$ is $O(g(n))$.
- If $L = \infty \rightarrow$, $f(n)$ is $\Omega(g(n))$.
- If $L = \text{ constant }  \rightarrow$$f(n)$ *may* be $\Theta(g(n))$.

### Finding $n_0$ and $c$

$$f(n) = 3n^3 + 20n^2 + 5$$

Ex. Method 1:

$$ 3n^3 \leq 3n^3 , \forall n \geq 1 $$
$$ 20n^2 \leq 20n^3 , \forall n \geq 1 $$
$$ 5n \leq 5n^3 , \forall n \geq 1 $$
$$ (3+ 20 + 5)n^3 = 28n^3$$
$$ 3n^3 + 20n^2 + 5 \leq 28n^3 \rightarrow \boxed{c = 28, n_0 = 1 }$$

Ex. Method 2:

$$ 3n^3 + 20n^2 + 5 \leq cn^3 $$
$$ 20n^2 + 5 \leq cn^3 -3n^3 $$
$$ 20n^2 + 5 \leq n^3(c -3) $$
$$ \frac{20}{n} + \frac{5}{n^3} <= c-3$$
$$ \therefore \frac{20}{n} + \frac{5}{n^3} + 3 <= c $$
$$ \text{Taking } n_0 = 1 \rightarrow \frac{20}{1} + \frac{5}{1} + 3 \leq c = \boxed{28}$$

