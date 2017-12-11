# COMP 352 - Algorithms

## Time complexity

|Syntax|Meaning|
|------|-------|
|\\( f(n) = O(g(n)) \\) |- g(n) is an **upper bound** of \\( f(n) \\) <br/>  - \\( f(n) \leq cg(n), n\geq n_0  \\)|
|\\( f(n) = \Omega(g(n)) \\) | - g(n) is a **lower bound** of \\( f(n) \\) <br/>  - \\( f(n) \geq cg(n), n\geq n_0  \\)|
|\\( f(n) = \Theta(g(n)) \\) | - g(n) is **bound on both sides** by \\( f(n) \\) <br/>  - \\( c_1g(n) \leq f(n) \leq c_2g(n), n\geq n_0  \\) <br/> - If \\(f(n) = \Theta(g(n)), \longrightarrow f(n) = O(g(n)) \land f(n) = \Omega(g(n))\\).|

|Time complexity name|Mathematical Representation|Examples|
|--------------------|---------------------------|--------|
|Constant|\\(1\\)| Variable assignment|
|Logarithmic|\\(log_n\\)| Splitting data into halves: merge sort, quick sort.|
|Linear|\\(n\\)| Single loop, dependent on \\(n\\).|
|Linear-Logarithmic|\\(nlog_n\\)|Double loop, with the inner loop splitting data into halves.|
|Quadratic|\\(n^2\\)|Two nested loops: Bubble sort, selection sort, insertion sort.|
|Cubic|\\(n^3\\)| Three nested loops | 
|Exponential|\\(2^n\\)| Binary/Multiple recursion|
|Factorial|\\(n!\\)|

### Limit Method (domination)

If you have \\(f(n)\\) and want to see if it's \\(O(g(n))\\):

- Take the limit \\(L = \frac{f(n)}{g(n)} , n\rightarrow \infty\\) 
- If \\(L = 0 \rightarrow\\), \\(f(n)\\) is \\(O(g(n))\\).
- If \\(L = \infty \rightarrow\\), \\(f(n)\\) is \\(\Omega(g(n))\\).
- If \\(L = \text{ constant }  \rightarrow\\)\\(f(n)\\) *may* be \\(\Theta(g(n))\\).

#### Finding \\(n_0\\) and \\(c\\)

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

## Recursion

- Some common uses of recursion:
	- Any logarithmic time sort (mergesort,quicksort,etc.)
	- Tree traversals
	- XML/HTML parsing
	- Graphs

### Evaluating Big-O of recursion

#### Linear recursion

- A method making **at most** one recursive call each time it is invoked.
- Very useful when a problem can be seen as many subsets of the same basic relation or problem, much like an inductive proof.

##### Examples of Implementation

###### Summing an array

```java

int linSum(int[] A, int n) {
	// base case
	if(n == 1) 
		return A[0];
	else
		return linSum(A,n-1) + A[n-1];
}
```

###### Reversing an array

- Reverses elements from i to j.

```java

int linRev(int[] A, int i, int j) {
	// base case
	if(i < j) {
		temp = A[j];
		A[j] = A[i];
		A[i] = temp;
		linRev(A,i++,j--);
	}
}
```

###### Computing powers (log_n)

```java

int pow(x,n) {
	if(n == 0)
		return 1;
	else if (n % 2 == 1) {
		int y = pow(x,(n-1)/2);
		return (x * y * y);
	} else {
		y = pow(x, n/2);
		return (y*y);
	}
}
```

###### Fibonacci numbers


```java
// Makes `n` total calls.

int[] linFib(n) {
	if (n=1) {
		return {n,0};
	} else {
		int i,j;
		[i,j] = linFib(n-1);
		return {i+j,i};
	}
}
```

#### Binary recursion

- Occurs when there are **two and exactly two** recursive calls for each non-base case.
	
###### Summing an array

```java

// Summing n consecutive elements of an array, from index i on,
// by splitting it into halves. This is still O(n) but minimizes memory usage.

int binSum(int[] A,int i,int n) {
	if(n == 1) 
		return A[i];
	else
		return binSum(A,i, n/2) + binSum(A,i+n/2,n/2);
}
```

###### Fibonacci numbers

// Naive implementation uses F(n) = F(n-1) + F(n-2) = (F(n-2) + F(n-3)) + (F(n-3) + F(n-4)), etc... which is O(2^n) complexity.


#### Tail Recursion

- Occurs when the very last step of the method is the recursive call. 
- This allows a smart compiler/interpreter to perform **Tail Call Optimization** (TCO) which allows the stack to only grow by one frame total instead one for each recursive call.

## Java Specific implementation

### Java Stack
- Java maintains a stack for the execution of methods.

- When a method is executed:
	- JVM pushes a frame onto the method stack containing:
		- Local variables
		- Return value
		- Program counter

- When a method end:
	- JVM pops the frame and passes control to the method on top of the stack.

### Java Heap
- Java maintains a memory heap for the creation of objects.
- Minimizing heap fragmentation:

|Algorithm|Result|
|---------|------|
|Best-fit| Searches the entire free list to find a hole with size closest to the amount of request memory|
|First-fit|Searches from the beginning for the first hole that is large enough to accomodate the request|
|Next-fit| Like First-Fit, but begins search from where it left off instead of beginning|
|Worst-fit| Searches for the largest hole of available memory|

### Garbage collection

- Mark-sweep GC associates a **mark bit** to objects that are live (i.e. have references pointing to them, directly or indirectly).
- To do this efficiently, a DFS is performed.

### Collections framework

- Every Collection has an `iterator`

- Collections:
	- `Set` - if collection can't have duplicates 
		- `HashSet` 
		- `TreeSet` - sorted
	- `List` - if collection can have duplicates
		- `ArrayList` - Efficient random access
		- `Vector` - *deprecated*
		- `LinkedList` - Doubly linked, efficient sequential access
	- `Map`
		- `HashMap`
		- `HashTable`
		- `TreeMap` - sorted balanced binary tree