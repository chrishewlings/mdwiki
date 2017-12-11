# COMP 352 - Sorting

[gimmick: math]()

## Selection Sort

- **Time complexity** : \\( O(n^2) \\)
- In-place


1. Find the minimum value.
2. Swap it with the value in the first position.
3. Repeat the steps starting from the second position.

```java
int[] a = {3,6,1,10,22};

for(int i = 0; i < a.length - 1; i++) {
    int minIndex = i;
    for(int j = i+1; j < a.length - 1; j++) {
        if(a[j] < a[minIndex])
            minIndex = j;
    }
    if(minIndex != i) {
        int temp = a[i];
        a[i] = a[minIndex];
        a[minIndex] = temp;
    }
```

## Insertion Sort

- **Time complexity**: \\( O(n^2) \\)
- If data is already sorted: \\( O(n) \\)
- In-place

1. Remove an element from the input data
2. Insert the element in the correct position in the already-sorted list
3. Repeat until no input elements remain.

```java
int[] a = {3,6,1,10,22};

int i,j,temp;

for(i = 1; i < a.length; i++) {
    temp = a[i];
    j = i-1;
    while(j >= 0 && a[j] > temp){
        a[j+1] = a[j];
        j = j-1;
    }
    a[j+1] = temp;
}
```

## Heap sort

- **Time complexity **: \\( O(nlog(n) \\)
- In-place

## Bucket sort

- Takes O(n+N) time

Warning: Bucket sort is sensitive to the distribution of input values, so if they are tightly clustered then it will not work well.

- Let `S` be a sequence of `n` key value pairs, with keys in \\( [0, N-1] \\)
- Use the keys as indices into an auxiliary array `B` of sequences.
	- Empty sequence `S` by moving each entry into a bucket `B[k]`.
	- for \\( i \rightarrow n-1 \\), move the entries of `B[i]` to the end of `S`.

```java

for( entry e : S ) {
	k = e.key;
	S.remove(e);
	B[k].append(e);
}

for(int i = 0; i < N-1; i++) {
	for( entry e : B[i] ) {
		B[i].remove(e);
		S.append(e);
	}
}
```

- Integer keys in range [a,b]:
	- put entry (k,v) into bucket `B[k-a]`

- String keys from set `D` of possible strings:
	- 	Sort `D` and compute rank `r` of each string `k` of `D`
	-  put entry `k,v` into bucket `B[r(k)]`

## Lexicographic sort

- Given tuples \\( x,y \\) of length `i`:
	- \\( (x_1 < y_1 \lor x_1 = y_1) \land (x_2 < y_1 \lor x_1 = y_1) .... \land (x_n < y_n \lor x_n = y_n) \\)

- In principle, sort tuples by first dimension, then second, etc...
	
## Radix-sort

- Uses lexicographic sorting using bucket-sort as the stable sorting algorithm in each dimension.
- Radix-sort is applicable to tuples where the keys in each dimension \\( i \in [0,N-1] \\)
- Radix-sort runs in O(d(n+N))
- Radix-sort can be used to sort a sequence of bitwise integers in linear time.

## Merge sort

- Time complexity: \\( O(n log(n)) \\)
- Height: \\( O(log(n)) \\)

### Implementation

- Given a sequence S with n elements:
1. **Divide** : partition \\(S\\) into \\(S_1, S_2, \text{ with } n/2 \\) elements.
2. **Recur** : Recursively sort \\(S_1,S_2\\)
3. **Merge** : Merge \\(S_1,S_2\\) into a unique sorted sequence.

```java
mergeSort(S) {
	if(S.size() > 1) {
		S1 = leftHalf(S);
		S2 = rightHalf(S);
		mergeSort(S1);
		mergeSort(S2);
	out = merge(S1,S2);
	}
}

merge(S1,S2) {

	S = new Sequence();
	while( !S1.isEmpty() && !S2.isEmpty() ) {
		if (S1.first() < S2.first())
			S.addLast(S1.remove(S1.first()));
		else
			S.addLast(S2.remove(S2.first()));
	}

	while(!S1.isEmpty()) 
		S.addLast(S1.remove(S1.first()));
	
	while(!S2.isEmpty())
		S.addLast(S2.remove(S2.first()));
		
	return S;			

```

## Quicksort

- **Average time complexity**: \\( O(nlog(n))  \\)
- **Worst case**: \\( O(n^2) \\)
	- This occurs if pivot is poorly chosen, i.e. the largest or smallest element of the given subsequence
	- Still, usually preferred to merge sort because little additional space is required, and has good cache locality

Given a sequence `S`:

1. Pick a random element `p` from `S` as a pivot
2. Partition `S` into 
	- `L`: elements less than pivot
	- `R`: elements greater than pivor
3. Recursively sort `L`,`R`
4. Combine `L`,`R`

### Sort with external lists

```java

partition(S,p) {

	Sequence l,r = new Sequence();
	
	x = S.remove(p);
	while(!S.isEmpty()) {
		y = S.remove(S.first());
		if(y < x)
			l.addLast(y);
		else
			r.addLast(y);
			
	}
	return l,r;
}
```	

### Sort in-place


```java

inPlaceQuickSort(S,l,r) {
	if l >= r
		return;
	i = Rand.nextInt(l,r);
	x = S[i];
	
	(h,k) = inPlacePartition(x);
	
	inPlaceQuickSort(S,l,h-1);
	inPlaceQuickSort(S,k+1,r);
}
	